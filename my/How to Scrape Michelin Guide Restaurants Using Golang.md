
# How to Scrape Michelin Guide Restaurants Using Golang

At the dawn of the automobile era, Michelin, a tire company, introduced a travel guide that eventually included restaurant recommendations. Over time, Michelin stars became synonymous with culinary prestige, and gaining one could transform a chef's career. Conversely, losing one can have significant consequences.

Inspired by [this Reddit post](https://www.reddit.com/r/singapore/comments/pqnjd2/singapore_michelin_guide_2021_map/), I set out to scrape restaurant data from the official [Michelin Guide website](https://guide.michelin.com/en/restaurants) and compile it into a CSV file. This dataset enables users to map Michelin-awarded restaurants worldwide using [Google My Maps](https://mymaps.google.com/), as seen in [this example](https://www.google.com/maps/d/edit?mid=1wSXxkPcNY50R78_T83tUZdZuYRk2L6jY).

In this article, I’ll share the process of collecting restaurant details using Golang and the [Colly framework](http://go-colly.org/). The final dataset is freely available for download on [GitHub](https://github.com/ngshiheng/michelin-my-maps/tree/main/data) or can be explored at [michelin.jerrynsh.com](https://michelin.jerrynsh.com/).

---

**Stop wasting time on proxies and CAPTCHAs!** ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)

---

## Overview

This project aimed to achieve the following goals:

1. Collect high-quality data from the Michelin Guide website.
2. Leave a minimal footprint to avoid harming the website.

### What Is "High-Quality" Data?

High-quality data means ensuring consistency, accuracy, and correct parsing so it can be used directly without further cleaning or "data munging."

### Data to Be Collected

After analyzing the Michelin Guide's pages, I decided to collect the following details:

- **Name**  
- **Address**  
- **Location**  
- **Price** (MinPrice and MaxPrice combined into one due to website updates)  
- **Currency**  
- **Longitude**  
- **Latitude**  
- **PhoneNumber**  
- **URL** (Link to the Michelin Guide page)  
- **WebsiteURL** (The restaurant's website)  
- **Award** (e.g., 1-3 Michelin Stars or Bib Gourmand)  

### Example Data Model

Here’s an example of the restaurant data structure:

```go
// model.go

type Restaurant struct {
	Name        string
	Address     string
	Location    string
	Price       string
	Currency    string
	Cuisine     string
	Longitude   string
	Latitude    string
	PhoneNumber string
	Url         string
	WebsiteUrl  string
	Award       string
}
```

---

**Stop wasting time on proxies and CAPTCHAs!** ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)

---

## Tools and Frameworks

With numerous scraping tools available, I opted for the following:

- **Colly**: A fast, elegant web scraping framework for Golang.
- **DevTools**: Essential for analyzing the website structure.

### Selecting the Right Tool

While Python's **Scrapy** is feature-rich, it felt like overkill for this relatively simple project. I chose **Colly** for its simplicity and excellent developer experience.

If the website were rendered with JavaScript, tools like **Selenium** or **Puppeteer** would have been required. Fortunately, the Michelin Guide uses server-side rendering, making it easier to scrape.

---

**Need proxies or CAPTCHA bypassing?** ScraperAPI simplifies these challenges, so you can focus on your scraping goals. Try it today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)

---

## Minimizing Footprint

The golden rule of web scraping is to avoid harming the website. Here’s how I achieved this:

### Caching Responses

Caching greatly reduces load on the website during development and speeds up retries.

```go
cacheDir := filepath.Join(cachePath)

c := colly.NewCollector(
	colly.CacheDir(cacheDir),
	colly.AllowedDomains("guide.michelin.com"),
)
```

### Adding Delays Between Requests

Adding delays prevents overloading the website and mitigates anti-scraping measures like IP bans.

```go
c.Limit(&colly.LimitRule{
	Delay:       2 * time.Second,
	RandomDelay: 2 * time.Second,
})
```

When scraping larger datasets, using a proxy solution like [ScraperAPI](https://www.scraperapi.com/?fp_ref=coupons) is highly recommended.

## Building the Scraper

### Setting Entry Points

The scraper starts from specific URLs for each Michelin award category:

```go
var urls = []startUrl{
	{"3 MICHELIN Stars", "https://guide.michelin.com/en/restaurants/3-stars-michelin/"},
	{"2 MICHELIN Stars", "https://guide.michelin.com/en/restaurants/2-stars-michelin/"},
	{"1 MICHELIN Star", "https://guide.michelin.com/en/restaurants/1-star-michelin/"},
	{"Bib Gourmand", "https://guide.michelin.com/en/restaurants/bib-gourmand"},
}
```

### Extracting Data

I used **XPath** selectors to extract restaurant details from the HTML pages. Extracted data is passed between collectors using Colly's context feature.

```go
app.collector.OnXML(restaurantXPath, func(e *colly.XMLElement) {
	url := e.Request.AbsoluteURL(e.ChildAttr(restaurantDetailUrlXPath, "href"))
	location := e.ChildText(restaurantLocationXPath)

	e.Request.Ctx.Put("location", location)
	app.detailCollector.Request(e.Request.Method, url, nil, e.Request.Ctx, nil)
})
```

## Challenges and Solutions

### Handling JavaScript-rendered Websites

If the website were rendered with JavaScript, tools like **Selenium** or **Splash** would have been necessary. However, since Michelin Guide uses server-side rendering, this wasn’t an issue.

### Rate-Limiting and Blocking

For handling rate-limiting or IP bans, I recommend using a proxy API like [ScraperAPI](https://www.scraperapi.com/?fp_ref=coupons), which automates proxy rotation and CAPTCHA solving.

## Conclusion

Scraping Michelin Guide data was both a rewarding and challenging experience. While I initially aimed to map every Michelin-awarded restaurant using Google My Maps, limitations in My Maps’ API meant manual imports were necessary.

Despite this, the project was a success. The dataset has been well-received, with many users leveraging it for analytics and mapping. If you use the dataset or create something unique, feel free to share it with me!

For more information, explore the full source code on [GitHub](https://github.com/ngshiheng/michelin-my-maps/tree/v1.0.0).

---
