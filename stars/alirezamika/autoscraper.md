---
project: autoscraper
stars: 7073
description: A Smart, Automatic, Fast and Lightweight Web Scraper for Python
url: https://github.com/alirezamika/autoscraper
---

AutoScraper: A Smart, Automatic, Fast and Lightweight Web Scraper for Python
============================================================================

This project is made for automatic web scraping to make scraping easy. It gets a url or the html content of a web page and a list of sample data which we want to scrape from that page. **This data can be text, url or any html tag value of that page.** It learns the scraping rules and returns the similar elements. Then you can use this learned object with new urls to get similar content or the exact same element of those new pages.

Installation
------------

It's compatible with python 3.

-   Install latest version from git repository using pip:

$ pip install git+https://github.com/alirezamika/autoscraper.git

-   Install from PyPI:

$ pip install autoscraper

-   Install from source:

$ python setup.py install

How to use
----------

### Getting similar results

Say we want to fetch all related post titles in a stackoverflow page:

from autoscraper import AutoScraper

url \= 'https://stackoverflow.com/questions/2081586/web-scraping-with-python'

\# We can add one or multiple candidates here.
\# You can also put urls here to retrieve urls.
wanted\_list \= \["What are metaclasses in Python?"\]

scraper \= AutoScraper()
result \= scraper.build(url, wanted\_list)
print(result)

Here's the output:

\[
    'How do I merge two dictionaries in a single expression in Python (taking union of dictionaries)?', 
    'How to call an external command?', 
    'What are metaclasses in Python?', 
    'Does Python have a ternary conditional operator?', 
    'How do you remove duplicates from a list whilst preserving order?', 
    'Convert bytes to a string', 
    'How to get line count of a large file cheaply in Python?', 
    "Does Python have a string 'contains' substring method?", 
    'Why is “1000000000000000 in range(1000000000000001)” so fast in Python 3?'
\]

Now you can use the `scraper` object to get related topics of any stackoverflow page:

scraper.get\_result\_similar('https://stackoverflow.com/questions/606191/convert-bytes-to-a-string')

### Getting exact result

Say we want to scrape live stock prices from yahoo finance:

from autoscraper import AutoScraper

url \= 'https://finance.yahoo.com/quote/AAPL/'

wanted\_list \= \["124.81"\]

scraper \= AutoScraper()

\# Here we can also pass html content via the html parameter instead of the url (html=html\_content)
result \= scraper.build(url, wanted\_list)
print(result)

Note that you should update the `wanted_list` if you want to copy this code, as the content of the page dynamically changes.

You can also pass any custom `requests` module parameter. for example you may want to use proxies or custom headers:

proxies \= {
    "http": 'http://127.0.0.1:8001',
    "https": 'https://127.0.0.1:8001',
}

result \= scraper.build(url, wanted\_list, request\_args\=dict(proxies\=proxies))

Now we can get the price of any symbol:

scraper.get\_result\_exact('https://finance.yahoo.com/quote/MSFT/')

**You may want to get other info as well.** For example if you want to get market cap too, you can just append it to the wanted list. By using the `get_result_exact` method, it will retrieve the data as the same exact order in the wanted list.

**Another example:** Say we want to scrape the about text, number of stars and the link to issues of Github repo pages:

from autoscraper import AutoScraper

url \= 'https://github.com/alirezamika/autoscraper'

wanted\_list \= \['A Smart, Automatic, Fast and Lightweight Web Scraper for Python', '6.2k', 'https://github.com/alirezamika/autoscraper/issues'\]

scraper \= AutoScraper()
scraper.build(url, wanted\_list)

Simple, right?

### Saving the model

We can now save the built model to use it later. To save:

\# Give it a file path
scraper.save('yahoo-finance')

And to load:

scraper.load('yahoo-finance')

Tutorials
---------

-   See this gist for more advanced usages.
-   AutoScraper and Flask: Create an API From Any Website in Less Than 5 Minutes

Issues
------

Feel free to open an issue if you have any problem using the module.

Support the project
-------------------

#### Happy Coding ♥️
