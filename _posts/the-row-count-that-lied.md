# The row count that lied

*1 June 2026 · Random Code*

The other day a pipeline started throwing a data-integrity error in production. We export a table from DuckDB to a CSV, load it into SQL Server with `bcp`, and then check that the number of rows in the CSV matches the number `bcp` says it inserted. In production, the two numbers disagreed. Locally, on the exact same data, they matched.

That last sentence is the trap. "Same data, different result" feels like an environment problem, so that's where I went first. Different locale? Different encoding? A different DuckDB or `bcp` version? I spun up the production container and checked all of it. `LANG` was `C.UTF-8`, the same as my laptop. DuckDB was 1.2.1 on both. Python was 3.11 on both. Every suspect had an alibi.

So I stopped guessing and ran the actual thing. I wrote a tiny CSV with a few awkward rows, exported it through DuckDB with the *exact* production COPY command, and counted it with the *exact* production function — first on my Mac, then mounted into the production image. Both undercounted, identically. The environment was innocent the whole time.

The bug was in the counter. It used Python's `csv.reader`, which is quote-aware:

```python
reader = csv.reader(csvfile, delimiter=self.delimiter)
```

But our export is *unquoted*. So when a field contained a raw `"`, `csv.reader` treated it as an opening quote and happily swallowed the following rows until it found a closing one — merging three rows into one. Meanwhile `bcp` in character mode doesn't care about quotes at all; it just splits on the delimiter and the newline. The two were reading the same bytes with completely different rules.

Then a colleague mentioned they'd had to strip `\r\n` from their text earlier. Same root cause, different flavour: `csv.reader` treats a lone `\r` as a line ending, but `bcp` only ends rows on `\n`. So a stray carriage return made the counter *over*count instead.

The fix is to count the way `bcp` actually does — bytes, not parsed CSV:

```python
with open(csv_file_path, "rb") as f:
    return max(f.read().count(b"\n") - 1, 0)  # minus the header
```

No decoding, no quote handling, no locale. It just counts newline bytes, which is precisely `bcp`'s row model. Quotes, carriage returns, weird encodings — all irrelevant.

The lesson I keep relearning: when two things are supposed to agree and don't, don't theorise about the environment. Reproduce it in the smallest possible script and watch it fail. The bug was deterministic all along — I just hadn't asked it the right question.

That's all for now!
