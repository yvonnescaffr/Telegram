
# Comprehensive Guide to Google's Crawlers (User Agents)

## Introduction

"Crawlers" (sometimes referred to as "spiders" or "bots") are programs designed to automatically discover and scan websites by following links from one page to another. Google’s primary crawler is known as **Googlebot**. This article provides an overview of Google's crawlers, their functions, and how to control them effectively using tools like `robots.txt`.

---

**Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)**

---

## Overview of Google's Crawlers

Google employs a variety of crawlers for its products and services. Below are key points to understand their usage:

1. **User Agent Tokens**: These are identifiers used in the `robots.txt` file to specify rules for different crawlers. When creating rules, match the appropriate user agent token for the crawler you want to control.
2. **Complete User Agent Strings**: These provide detailed descriptions of the crawler and can be found in HTTP requests and server logs.

---

### Common Google Crawlers

#### 1. **Googlebot Image**
   - **Purpose**: Crawls and indexes images for Google Images.
   - **User Agent Token**: `Googlebot-Image`
   - **Complete User Agent String**: 
     ```
     Googlebot-Image/1.0
     ```

#### 2. **Googlebot (Mobile-Friendly Version)**
   - **Purpose**: Crawls and indexes pages optimized for mobile devices.
   - **User Agent Token**: `Googlebot`
   - **Complete User Agent String**: 
     ```
     Mozilla/5.0 (Linux; Android 6.0.1; Nexus 5X Build/MMB29P) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/W.X.Y.Z Mobile Safari/537.36 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)
     ```

#### 3. **Feedfetcher**
   - **Purpose**: Fetches RSS and Atom feeds for Google services.
   - **Note**: Does not follow `robots.txt` rules.
   - **User Agent Token**: `FeedFetcher-Google`
   - **Complete User Agent String**: 
     ```
     FeedFetcher-Google; (+http://www.google.com/feedfetcher.html)
     ```

#### 4. **Google Site Verification**
   - **Purpose**: Verifies ownership of websites.
   - **Note**: Ignores `robots.txt` rules.
   - **User Agent Token**: `Google-Site-Verification`
   - **Complete User Agent String**: 
     ```
     Mozilla/5.0 (compatible; Google-Site-Verification/1.0)
     ```

---

## Explanation of Chrome/W.X.Y.Z in User Agents

In some user agent strings, you’ll see a placeholder like **Chrome/W.X.Y.Z**. This represents the version of the Chrome browser used by the crawler. For example, it could be `41.0.2272.96`. Over time, this version number updates to match the latest Chromium release used by Googlebot.

When filtering server logs or searching for these crawlers, use wildcards for the version number instead of specifying an exact value.

---

## Configuring `robots.txt` for Google Crawlers

The `robots.txt` file allows you to control how Google crawlers interact with your site. Here are a few use cases:

### 1. Allow All Google Crawlers
If you want Google to crawl all your content, you don’t need a `robots.txt` file at all.

### 2. Block All Google Crawlers
Use the following rule to block all Google crawlers:
```plaintext
User-agent: Googlebot
Disallow: /
```

### 3. Allow Specific Crawlers
For instance, to block image crawling but allow everything else:
```plaintext
User-agent: Googlebot
Disallow:

User-agent: Googlebot-Image
Disallow: /personal
```

### 4. Allow Ads but Block Search Indexing
To allow Google Ads crawlers but block pages from appearing in search results:
```plaintext
User-agent: Googlebot
Disallow: /

User-agent: Mediapartners-Google
Disallow:
```

---

## Controlling Crawl Rates

Each Google crawler operates at different speeds depending on its purpose. Google determines the optimal crawl rate algorithmically. If Googlebot crawls your site too frequently, you can adjust the crawl rate using Google Search Console.

---

## Deprecated Google Crawlers

Some Google crawlers are no longer in use. These include:

### 1. **Duplex on the Web**
   - **Purpose**: Powered the “Duplex on the Web” service.
   - **User Agent Token**: `DuplexWeb-Google`
   - **Complete User Agent String**: 
     ```
     Mozilla/5.0 (Linux; Android 11; Pixel 2; DuplexWeb-Google/1.0) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.193 Mobile Safari/537.36
     ```

### 2. **Web Light**
   - **Purpose**: Ensures pages load faster for slow connections. It ignores `robots.txt` rules.
   - **Note**: Checks for the `no-transform` header on websites.

---

## Conclusion

Understanding Google’s crawlers and configuring them properly ensures your website is optimized for search engine indexing and traffic. By using tools like `robots.txt`, you can fine-tune how Google interacts with your site to achieve your business goals.

---

> Stop struggling with proxies and CAPTCHAs! Try ScraperAPI, the ultimate solution for web scraping with built-in proxy management and CAPTCHA handling. Get started today: [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)
