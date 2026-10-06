# Veda-Technology-Task-29
# 🛒 Product Basket Analysis

> Finding products that are frequently purchased together using association-style analysis in Python.

**Task 29 | Level 2 | Data Analytics Track | Veda Technology Internship**

---

##  Overview

Retail stores collect thousands of transactions every day, and hidden inside this data are useful buying patterns. This project performs a **Market Basket Analysis** on order-level data to discover which products customers tend to buy **together** in the same order.

The results are used to build a simple **product recommendation function** ("Customers who bought X also bought Y").

##  Objectives

- Introduce association-style analysis
- Identify the **top product pairs** bought together
- Measure the strength of each relationship using **Support, Confidence and Lift**
- Produce **product recommendations** from the strongest associations


##  Tools and Libraries

- **Python 3**
- **Pandas** for data cleaning and grouping
- **collections.Counter** and **itertools.combinations** for counting product pairs
- **Matplotlib** for charts
- **Google Colab** as the working environment

##  Methodology

1. **Load data:** read the CSV into a Pandas DataFrame.
2. **Clean data:**
   - drop rows with missing descriptions
   - remove cancelled orders (invoice numbers starting with `C`)
   - remove zero or negative quantity and price
   - exclude non-product codes such as `POST`, `DOT`, `M`, `BANK CHARGES`
3. **Build baskets:** keep the 200 most popular products and group transactions by **invoice number** to get one list of unique products per order. Orders with fewer than 2 products are dropped.
4. **Count pairs:** generate all unique pairs per order with `combinations(items, 2)`, which automatically **excludes self-pairs**, and count them with `Counter`.
5. **Measure strength:** calculate Support, Confidence and Lift for every pair appearing in at least 50 orders.

###  Metrics

| Metric | Meaning | Formula |
|---|---|---|
| **Support** | Share of all orders containing both A and B | `count(A,B) / total orders` |
| **Confidence** | Of the orders containing A, the share that also contain B | `count(A,B) / count(A)` |
| **Lift** | How much more often A and B are bought together than by chance (above 1 means a real association) | `Confidence / (count(B) / total orders)` |

##  Results

After cleaning and filtering, **1,327 orders** contained at least two products.

### Top 5 product pairs

| # | Product 1 | Product 2 | Orders |
|---|---|---|---|
| 1 | Paper Chain Kit 50's Christmas | Party Bunting | 137 |
| 2 | Jumbo Bag Baroque Black White | Jumbo Bag Pink Polkadot | 122 |
| 3 | Jumbo Bag Baroque Black White | Jumbo Bag Red Retrospot | 122 |
| 4 | Regency Cakestand 3 Tier | Set of 3 Cake Tins Pantry Design | 119 |
| 5 | Jumbo Bag Pink Polkadot | Jumbo Bag Red Retrospot | 118 |

### Strongest associations (by Lift)

| Product A | Product B | Count | Support | Confidence | Lift |
|---|---|---|---|---|---|
| Lunch Bag Red Retrospot | Lunch Bag Black Skull | 112 | 0.0844 | 0.640 | **4.67** |
| Baking Set 9 Piece Retrospot | Retrospot Tea Set Ceramic 11 PC | 98 | 0.0739 | 0.563 | **4.59** |
| White Metal Lantern | Glass Star Frosted T-Light Holder | 101 | 0.0761 | 0.577 | **4.14** |
| Lunch Bag Red Retrospot | Lunch Bag Spaceboy Design | 109 | 0.0821 | 0.623 | **4.11** |
| Hand Warmer Red Polka Dot | Knitted Union Flag Hot Water Bottle | 95 | 0.0716 | 0.537 | **4.05** |

### Sample recommendation

```
Customers who bought: PAPER CHAIN KIT 50'S CHRISTMAS

Product B        Confidence   Lift
PARTY BUNTING    0.626        3.69
```

##  Key Insights

- Most strong pairs belong to the **same product family or design theme** (matching lunch bags, jumbo bags, kitchen sets, decorative items).
- All top pairs have a **Lift well above 1**, which confirms genuine relationships between the products and not just popularity.
- The results can support **"customers also bought" suggestions, bundle offers, product placement and cross-selling** to raise the average order value.


##  Project Structure

```
├── README.md
├── online_retail_II_sample.csv                  # dataset
├── Task29_Product_Basket_Analysis.ipynb         # Colab notebook
└── Task29_Product_Basket_Analysis_Report.pdf    # detailed report
```

##  Future Improvements

- Use the **Apriori / FP-Growth** algorithm to find item sets of three or more products
- Include the **full product range** instead of the top 200 products
- Analyse patterns by **country or season**
- Build a small **Streamlit app** for live recommendations
