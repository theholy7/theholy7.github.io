## Project Structure

The [second post](structure) explained how I structured the project, and this post will explore in
further detail how I use Scrapy, what each of the files in the project does, and my workflow.

I need to preface this post with an explanation of how I like to think about scraping data.
Kudos to the scrapy boss that taught me much of what I know.

### Start URLs: why bother?

When I first started working, I had the pleasure of learning from a senior data miner that was in our team.
When I started looking through his code, I was new to Scrapy which means that everything was very confusing.
Thankfully today, when I look at his code, things make a lot more sense!

One of the first things he taught me was to build my spiders in two steps:
1. Collect Start URLs;
2. Collect content from Start URLs.

Initially I wondered why, but after thinking about it, that makes total sense. One of our first tasks was to
scrape data from more than 30000 pages. Why should those pages be scraped one after the other, or according to the
concurrency limit you set on Scrapy? Isn't it better to just spin up several instances of the same spider, give each one
1000 Start URLs and let them scrape the data in parallel?

The answer: of course it is better to scrape data in parallel.

That is why you will see me dividing my spiders for the same website into 2:
* food_site_starturls;
* food_site_recipes.


