
# 🚀 Amazon Scraper: Simplify Your Amazon Data Collection

![Amazon Scraper Featured Image](https://raw.githubusercontent.com/omkarcloud/amazon-scraper/master/images/amazon-scraper-featured-image.png)

Amazon Scraper is your go-to solution for collecting Amazon product data effortlessly. Whether you're a researcher, developer, or e-commerce entrepreneur, this tool is designed to save you time and effort.

---

## **Stop Wasting Time on Proxies and CAPTCHAs!**
ScraperAPI’s simple API handles millions of web scraping requests, so you can focus on the data. Get structured data from Amazon, Google, Walmart, and more.  
👉 **[Start your free trial today!](https://www.scraperapi.com/?fp_ref=coupons)**  

---

## Features at a Glance

![Forks](https://img.shields.io/github/forks/omkarcloud/amazon-scraper?style=for-the-badge) ![Stars](https://img.shields.io/github/stars/omkarcloud/amazon-scraper?style=for-the-badge&color=yellow) ![License](https://img.shields.io/github/license/omkarcloud/amazon-scraper?color=orange&style=for-the-badge)

Amazon Scraper is an open-source project that simplifies extracting product data from Amazon. Use it responsibly and in compliance with local and international laws.

### **Disclaimer**
By using Amazon Scraper, you agree to comply with all applicable local and international laws related to data scraping, copyright, and privacy. The developers are not responsible for any misuse of this software. Please use Amazon Scraper ethically and within legal boundaries.

For any issues or concerns, contact **Chetan Jain** at [chetan@omkar.cloud](mailto:chetan@omkar.cloud).

---

## 🚀 Getting Started

### **1️⃣ Clone the Repository**
```bash
git clone https://github.com/omkarcloud/amazon-scraper
cd amazon-scraper
```

### **2️⃣ Install Dependencies**
```bash
python -m pip install -r requirements.txt
```

### **3️⃣ Start Scraping**
Run the following command to begin scraping:
```bash
python main.py
```

Find your results in the `output` directory.

![CSV Result Example](https://raw.githubusercontent.com/omkarcloud/amazon-scraper/master/images/amazon-scraper-csv-result.png)

> _If you don't have Python installed, follow this [simple guide](https://github.com/omkarcloud/amazon-scraper/blob/master/advanced.md#-i-dont-have-python-installed-how-can-i-run-the-scraper)._  

---

## ❓ How to Scrape Amazon Search Results?

1. Open the `main.py` file.
2. Add the keywords you want to search for in the `queries` list:
    ```python
    queries = [
      "Macbook",
    ]
    Amazon.search(queries)
    ```
3. Run the script:
    ```bash
    python main.py
    ```
Your results will appear in the `output` folder.

---

## ❓ How to Scrape Amazon Products by ASIN?

To scrape product details by ASIN, use the following code:
```python
asins = [
  "B08CZT64VP",
]
Amazon.get_products(asins)
```

---

## ❓ How to Scrape Amazon Data Using Your API?

Follow these steps to use the Amazon API for additional scraping:

1. **Sign up on RapidAPI** via [this link](https://rapidapi.com/auth/sign-up).
2. Subscribe to the **Free Plan** via [this link](https://rapidapi.com/Chetan11dev/api/amazon-scraper/pricing).
3. Copy your API key and use it in the scraper:
    ```python
    queries = [
      "watch",
    ]
    Amazon.search(queries, key="YOUR_API_KEY")
    ```
4. Run the script, and your data will be saved in the `output` directory:
    ```bash
    python main.py
    ```

---

## Why Choose ScraperAPI?

ScraperAPI takes care of proxies, CAPTCHAs, and server rotation. Access reliable data extraction services without hassle.  
👉 **[Start your free trial now!](https://www.scraperapi.com/?fp_ref=coupons)**  

---

## Additional Tools for Developers

- **[Botasaurus](https://github.com/omkarcloud/botasaurus):** A powerful framework for web scraping with anti-detection features, parallelization, and caching. Cut your development time by 50%!

---

## Need Help?  

For further assistance, contact us on WhatsApp. We'll be happy to help you with any questions or technical issues!

---
