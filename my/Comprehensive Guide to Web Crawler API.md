
# Comprehensive Guide to Web Crawler API

This guide provides an overview of the **Web Crawler API** operations for App Search, focusing on API usage, features, and shared concerns. If you're developing or troubleshooting web crawler integrations, this guide will help you get started.

## Table of Contents
1. [Introduction](#introduction)
2. [Enterprise Search Base URL](#enterprise-search-base-url)
3. [Authentication Options](#authentication-options)
4. [Crawl Request API](#crawl-request-api)
5. [Crawl Schedule API](#crawl-schedule-api)
6. [Process Crawl API](#process-crawl-api)
7. [Domain Management](#domain-management)
8. [Advanced Troubleshooting](#advanced-troubleshooting)

---

## Introduction

The **Web Crawler API** enables developers to interact with App Search's web crawling functionality through several endpoints. Each API operation provides tools to manage crawl requests, schedules, and domain configurations.

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. Start your free trial today! 👉 [Start Your Free Trial](https://www.scraperapi.com/?fp_ref=coupons)

---

## Enterprise Search Base URL

To interact with the Web Crawler API, use the **Enterprise Search Base URL** as the starting point for all API requests. The URL is represented in `curl` examples as:

```bash
${ENTERPRISE_SEARCH_BASE_URL}
```

This URL points to your Enterprise Search deployment. For example:

```bash
curl \
--request "GET" \
--url "${ENTERPRISE_SEARCH_BASE_URL}/api/as/v1/engines/${ENGINE_NAME}/crawler" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${TOKEN}"
```

---

## Authentication Options

The API supports three authentication methods:
- **Basic Authentication:** Use a `username` and `password`.
- **Elasticsearch Token:** Use an Elasticsearch-issued token.
- **App Search Key:** Use an App Search private key.

Example authentication setup:

```bash
--header "Authorization: Bearer ${TOKEN}"
```

---

## Crawl Request API

### Get Active Crawl Request

Retrieve details about the current active crawl:

```bash
GET <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/crawl_requests/active
```

**Example Response:**

```json
{
  "id": "601b21adbeae67679b3b760a",
  "status": "running",
  "created_at": "2023-01-01T00:00:00Z",
  "begun_at": "2023-01-01T01:00:00Z",
  "completed_at": null
}
```

### Cancel Active Crawl

Cancel an active crawl for an engine:

```bash
POST <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/crawl_requests/active/cancel
```

---

## Crawl Schedule API

### Get Current Crawl Schedule

Retrieve the crawl schedule for an engine:

```bash
GET <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/crawl_schedule
```

**Example Response:**

```json
{
  "engine": "example_engine",
  "frequency": 2,
  "unit": "week"
}
```

---

## Process Crawl API

### View Process Crawl Details

Use this API to debug a specific URL or review a crawl’s history:

```bash
GET <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/process_crawls/<process_crawl_id>
```

**Example Response:**

```json
{
  "id": "61421fe6e725695876d72d2e",
  "total_url_count": 167,
  "denied_url_count": 92,
  "domains": ["https://example.com"],
  "created_at": "2023-01-01T00:00:00Z",
  "completed_at": "2023-01-01T01:00:00Z"
}
```

---

## Domain Management

### List Domains

Retrieve the list of domains associated with an engine:

```bash
GET <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/domains
```

**Example Response:**

```json
{
  "results": [
    {
      "id": "61a8eb863932dd78141fb0df",
      "name": "https://example.com",
      "document_count": 1000,
      "entry_points": ["/"]
    }
  ]
}
```

### Add a New Domain

Add a domain to the crawler configuration:

```bash
POST <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/domains
```

**Example Request Body:**

```json
{
  "name": "https://example.com"
}
```

---

## Advanced Troubleshooting

### Validate a URL

Validate whether the crawler can access a specific URL:

```bash
POST <enterprise_search_base_url>/api/as/v1/engines/<engine_name>/crawler/validate_url
```

**Example Request Body:**

```json
{
  "url": "https://example.com",
  "checks": ["url", "tcp", "url_request"]
}
```

---

### ScraperAPI Advertisement

Stop wasting time on proxies and CAPTCHAs! ScraperAPI's simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more. Start your free trial today! 👉 [https://www.scraperapi.com/?fp_ref=coupons](https://www.scraperapi.com/?fp_ref=coupons)
