
# Python Web Scraping: Create an API in Ten Minutes

Web scraping often begins with a question: **Does the target website provide an API?** If yes, great! But what if the website doesn’t have an API, and you still want to scrape data efficiently? Here’s where creativity comes into play: if there’s no API, you can build one.

![Introduction to Toapi](https://img1.sycdn.imooc.com//5d2fd43e0001b3e006950604.jpg)

---

## Transforming Scraped Data into APIs

Many data-related tasks follow this basic flow: **scrape data → store data → create an API → update data regularly**. However, you’re likely not looking to master API service deployment—you just want to use the website’s data.

Enter **Toapi**. This tool automates the process, allowing you to **access real-time data from websites** effortlessly.

### Example: Toapi in Action

Here’s an example website (no API provided) that can be transformed using Toapi: [Chengdu Government Info](http://gk.chengdu.gov.cn/govInfoPub/list.action?classId=07170201020202&tn=2&p=1). The magic of Toapi makes the website data as easy to consume as a slice of cake.

![Toapi API Output Example](https://img1.sycdn.imooc.com//5d2fd46f000105de07130272.jpg)

---

## How to Build an API with Toapi

With just **10 lines of code**, you can create a data API. Let’s walk through an example:

```python
from toapi import XPath, Item, Api
from toapi import Settings

# Custom settings for the API
class MySettings(Settings):
    web = {
        "with_ajax": False  # Disable PhantomJS for AJAX loading
    }

# Define the target website for scraping
api = Api('http://gk.chengdu.gov.cn/govInfoPub/', settings=MySettings)

# Define the structure for scraped data
class Post(Item):
    url = XPath('/html/body/div[2]/div/div[3]//a/@href')
    title = XPath('/html/body/div[2]/div/div[3]//a/span[2]/text()')
    
    class Meta:
        source = XPath('/html')  # Part of the HTML containing the data
        route = {"/test?page=:page": "list.action?classId=07170201020202&tn=2&p=:page"}

# Register the scraping service
api.register(Post)

# Run the server
api.serve()

# Visit: http://127.0.0.1:5000/
```

With this code, you can create an API that retrieves data from the website. It’s simple, efficient, and only takes a few minutes to set up.

---

### Understanding the Code

1. **Custom Settings**: Configure how Toapi interacts with the website (e.g., whether AJAX is needed).
2. **Item Definition**: Map the data you want to scrape using XPath.
3. **API Registration**: Register your scraping logic with Toapi’s API framework.
4. **Run the Server**: The server is ready to serve JSON-formatted data!

---

## Why Toapi is a Game-Changer

Toapi simplifies web scraping and API creation. Instead of spending hours learning how to build a scalable API service, you can focus on extracting and using real-time data. It’s especially helpful for developers who need quick solutions without diving deep into backend complexities.

Stop wasting time on proxies and CAPTCHAs! ScraperAPI’s simple API handles millions of web scraping requests, allowing you to focus on what matters: the data. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)

---

## Reflections from the Author

This article serves as a quick guide rather than a detailed tutorial. The goal is to share the core idea and approach so that you can adapt it to your learning process.

### A Note from the Author

Sharing is about exchanging ideas and learning together. I may not be an expert, but I hope my articles inspire you to explore new tools and techniques. Constructive feedback is always welcome—I’ll continue improving and sharing as much as I can.

---

## Final Thoughts

Web scraping doesn’t have to be complicated. With tools like Toapi, you can quickly transform raw website data into usable APIs. Whether for personal projects or business applications, this approach saves time and simplifies the process.

For more detailed guides and discussions, stay tuned for future updates. Thank you for reading, and I hope this article helps you kickstart your journey in building custom APIs.

**Author**: Tony带不带水  
**Original Post**: [Jianshu Article](https://www.jianshu.com/p/ae07f8afac65)
