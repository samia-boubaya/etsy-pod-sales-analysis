# Etsy POD Sales Analysis

This repository contains an analysis of Etsy Print-on-Demand (POD) sales data obtained through web scraping. The goal is to uncover top-selling products, profitable niches, optimal pricing ranges, high-value keywords, and seasonal trends to help launch a scalable, stock-free Etsy store capable of generating passive income.

## 📌 Project Overview

This project analyzes Etsy listing data to answer key questions such as:

* Which POD products sell the most?
* What are the top 5 niches?
* Which price ranges convert best?
* What title keywords dominate?
* What product niches sell the most?

## 📊 Key Insights

### **Top Products by Seasonal Performance**

* **Stickers** → Strong, stable demand year-round
* **Posters** → Peak: June–September
* **Shirts** → Peak: April–August
* **Hats** → Peak: September–October
* **Phone Cases** → Peak: October–December

### **Sticker Pricing Insights**

* €2.5–€5 → 29.5% of all sticker sales
* €0–€5 total → 65.8% of sales
* €7.5+ premium → Only 6.8%

### **Top Sticker Keywords**

* autocollant (673 mentions)
* journal (90)
* scrapbooking (84)
* vinyle (83)

### **Top Niches**

* Autocollants
* Étiquettes
* Décorations


## 💼 Business Recommendations

* Prioritize stickers year-round for steady sales.
* Add seasonal products: shirts (spring/summer), posters (late summer/fall), hats (fall/winter), phone cases (holidays).
* Use top keywords in titles and tags to improve SEO.
* Focus on €0–€5 pricing for high-volume sales; test premium bundles.
* Use Printify for POD fulfillment.
* Create décor and scrapbooking products in both digital and physical formats.

## ⚠️ Limitations

* Sales estimates are based on review counts (approximate).
* No demographic or behavioral buyer data.
* Data collected from the French Etsy domain.
* Product variations not fully captured due to rate limits.
---
### 📓 SECTION OVERVIEW

- **Project / Business Idea:** What the project is about

- **Problem:** The challenge we’re addressing

- **Solution / Approach:** How we solve it

- **Research & Plots:** How we analyzed data visually

- **Insights:** What we discovered

- **Interpretation:** Why it matters

- **Implications:** What actions the business can take

- **Business Impact:** Expected results for the business

- **Limitations:** What constraints or gaps exist
==================================================================================================================================
# <div align="center">RESEARCH</div>
==================================================================================================================================
### 🌐 **Which Are the Best-Selling POD Products on Etsy?**

I’m researching print-on-demand products to sell on Etsy that only require **digital artwork and marketing**, while the POD provider handles **printing, packaging, and shipping**.


### ⭐ **Using Google Trends for POD Product Research**
💡 **Goal:** Identify which POD product category has been searched the most on Google over the past 5 years (2020–2025).

Below is the list of product categories I’m comparing:

### 🎯 **Chosen POD product to research is :** `tote bags`

| Category              | Subcategories / Examples                                      |
|-----------------------|---------------------------------------------------------------|
| **Custom Apparel**        | T-shirts, Hoodies, Sweatshirts, Tank tops                     |
| **Mug**                   | Ceramic mugs, Color-changing mugs, Espresso mugs, Travel mugs |
| **Tote Bag**              | Cotton totes, All-over print totes                            |
| **Phone Case**            | iPhone / Samsung cases, Tough / Slim cases                    |
| **Stickers**              | Die-cut stickers, Kiss-cut stickers, Sticker sheets           |
| **Hats**                  | Baseball caps, Trucker hats, Beanies                          |
| **Pillows / Cushions**    | Pillow covers, Stuffed pillows, All-over print pillow designs|
| **Blanket**               | Fleece blankets, Sherpa blankets, Woven blankets             |
| **Wall Art**              | Posters, Canvas prints, Framed posters, Metal prints         |
| **Doormat**               | Printed coir doormats, Rubber-backed doormats                |
| **Drinkware**             | Stainless steel tumblers, Water bottles, Wine tumblers       |
| **Calendar**              | Custom printed wall calendars                                 |
| **Yoga Mat**              | Printed yoga mats                                             |
| **Bedding**               | Duvet covers, Pillowcases, All-over print bed sets           |
| **Pet Accessories**       | Pet bandanas, Pet beds, Pet bowls, Pet blankets              |
| **Ornaments**             | Ceramic ornaments, Wood ornaments, Metal ornaments           |

### **BEFORE GETTING STARTED :**

```Etsy``` is a dynamic website, so scraping it requires careful handling.

Since ```Etsy``` uses ```JavaScript``` to load some content,

```requests``` +  ``BeautifulSoup`` might work for static parts (like search results), 

but for dynamic content, ``Selenium`` is more reliable. 

I will be using ``requests`` + ``BeautifulSoup`` for ```product listings``` **(title, price, link)**

Important Note: Etsy uses dynamic loading + anti-bot protections.

Using code with standard HTML scraping can work as long as Etsy doesn’t block the request.

If blocked, using headers, rotating proxies, or the Etsy API will be required.
=======================================================================================================================================================================================
# <div align="center">IN DEPTH</div>
=======================================================================================================================================================================================
### 🧐 QUESTIONS

- Which keywords in product titles and descriptions drive the most sales?

- What keywords improve search visibility on Etsy?

- Which product niches have the highest demand?

- When is the best period to sell based on review trends?

- Which price ranges generate the most sales?

- Which country's customers are buying the most of this product?
---
### 📌 **Avoid web BLOCKED**
| Version                                   | Best For          | Pros                                           | Cons                          |
| ----------------------------------------- | ----------------- | ---------------------------------------------- | ----------------------------- |
| **Requests + BeautifulSoup + Pagination** | Simple scraping   | Fast, clean                                    | Etsy may block request        |
| **Selenium + BeautifulSoup + Pagination** | Reliable scraping | Bypasses bot protection, loads dynamic content | Slower, requires ChromeDriver |

---
## 📌 **Product PAGE**
### ⭐ **Product dataset**

The main data fields to extract from Etsy's product page :


| Field Name             | Python Data Type       | Concise Definition                      | Long Definition                                                                                       |
|------------------------|-----------------------|----------------------------------------|-------------------------------------------------------------------------------------------------------|
| **product_title**          | `str`                 | Product title                           | The full name of the product, same across all variants.                                              |
| **product_url**           | `str`                 | Short URL to product listing        | Etsy listing URL in the format `https://www.etsy.com/listing/product_id/` (e.g., "https://www.etsy.com/listing/1289965137/"). |
| **product_id**             | `int`                 | Unique product ID                       | Extracted from `product_url`; a unique identifier assigned by Etsy for each listing.               |
| **product_description**            | `str`                | Product's description           | The text content of the description of the product.                                               |
| **variations**        | `List`          | product variations / eg colour, style, material...               | List of all product variations (size, color, material, etc.), each stored as a dictionary.             |
| **current_price**      | `float`  | Current price of product               | Price of this variant after applying any discounts.                                                  |
| **old_price**          | `float`  | Original price of product              | Price of this variant before any discounts were applied (if available).                              |
| **discount_percentage**| `float`               | Variant discount percentage             | Discount applied to this variant, calculated if both current and old prices are available.           |
| **product_rating**         | `float`               | Average product rating                  | Average rating of the product out of 5 (e.g., 4.5).                                                 |
| **nbr_reviews**            | `int`                 | Total number of reviews                 | Total count of reviews received by the product.                                                     |
---
#### **`product_niche` from `product_title` and `product_description`**
| Field Name                 | Python Data Type       | Concise Definition                               |
|---------------------------|-------------------------|---------------------------------------------------|
| **product_niche**             | `str`                     | Product theme or genre (comedy, anime…)     |
---
### ⭐ **Reviews dataset**

All Reviews of the best-selling product 

| Field Name               | Python Data Type | Concise Definition                                      |
|--------------------------|------------------|----------------------------------------------------------|
| **review_variation**   | `str`            | The variation text the customer of the product purchased   |
| **review_comment**   | `str`            | The comment the customer gave the product   |
| **review_rating**        | `float`          | The rating the customer gave the product                 |
| **review_date**          | `date`           | The date when the customer posted the review             |

---

---

