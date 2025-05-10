---
layout: post
title: "Python Tips: the tempfile library"
excerpt_separator:  <!--more-->
categories:
  - Random Code
tags:
  - Learning
  - Python
---

The other day I was writing a python test, and I needed a temporary directory and file.

Normally, I make these tests happen with `os` and `pathlib` libraries.
It works well enough, and therefore I never had reason to change it.
However, this time I asked Claude for a quick test that I was going to edit after, and it showed me the `tempfile`
library.

> This module creates temporary files and directories. It works on all supported platforms.
> TemporaryFile, NamedTemporaryFile, TemporaryDirectory, and SpooledTemporaryFile are high-level interfaces which provide automatic cleanup and can be used as context managers. mkstemp() and mkdtemp() are lower-level functions which require manual cleanup.

You can do things like this:

```python
with tempfile.NamedTemporaryFile(mode='w+', delete=True) as temp_file:
    # You can write data to the temporary temp_file
    # `data` can just be a string of your liking, like a fake CSV
    temp_file.write(data)
    print(f"Created temporary file: {temp_file.name}")

    # You can then process the file via it's path
    # or just process it's content
    # ...
```

So practical! Quick tip of the day! Here's a basic complete example:

```python
import pandas as pd
import tempfile
import os
import unittest


def read_csv_to_dataframe(file_path):
    if not os.path.exists(file_path):
        raise FileNotFoundError(f"File not found: {file_path}")

    return pd.read_csv(file_path)


class TestCSVReader(unittest.TestCase):
    def test_read_csv_to_dataframe(self):
        """Test that CSV data is correctly loaded into a DataFrame."""
        # Create sample CSV data
        csv_data = """name,age,city
Alice,32,Seattle
Bob,45,Portland
Charlie,28,San Francisco"""

        # Create a temporary CSV file
        with tempfile.NamedTemporaryFile(mode='w+', suffix='.csv') as temp_file:
            # Write the CSV data
            temp_file.write(csv_data)
            temp_file.flush()
            temp_path = temp_file.name

            # Test the function
            df = read_csv_to_dataframe(temp_path)

            # Verify the results
            self.assertEqual(len(df), 3)
            self.assertEqual(list(df.columns), ['name', 'age', 'city'])
            self.assertEqual(df.iloc[0]['name'], 'Alice')
            self.assertEqual(df.iloc[1]['age'], 45)
            self.assertEqual(df.iloc[2]['city'], 'San Francisco')

if __name__ == "__main__":
    unittest.main()
```
