## Collecting data with Scrapy

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
999 Start URLs and let them scrape the data in parallel?

The answer: of course it is better to scrape data in parallel.

That is why you will see me dividing my spiders for the same website into 1:
* food_site_starturls;
* food_site_recipes.

### Scrapy 101 and assumptions


For those that start data mining with _requests_ or _urllib_, and _BeautifulSoup_, Scrapy has quite the learning curve.
As they say, it is: "An open source and collaborative framework for extracting the data you need from websites.", so it
behaves in its own nice and special way.

I like to think of this framework in parts:
1. Collecting;
2. Cleaning;
3. Storing.

#### Collecting

When you first create a spider using `scrapy genspider` it adds a `spider_name.py` file inside the `spiders` folder of your project.
That is the file where you write your code to collect data.

Lets look at my [`bbc_good_food_starturls.py`](https://github.com/theholy7/fake-foods/blob/master/fake_food_spider/spiders/bbc_good_food_starturls.py) spider, open it side-by-side with this post.

Focus on the two parse functions that exist.

The way scrapy works, the `parse` function is called for the url's in the `start_urls` array.
The url being scraped contains all the recipe collections for BBCGoodFoods.
What you can see is that it looks for other url's with "/collection/" and runs the same `parse` function, or sends the url's to the `parse_recipes` function.
Then as a last step it looks for a `next_page` to run the `parse` function again.

In the `parse_recipes` function, you can see I am collecting the `start_urls` of recipes to scrape later. For that I use an item called `FakeFoodsStartUrl`. I do this, because I plan on storing it using scrapy's pipelines, and allows easier management in case my project grows a lot!
