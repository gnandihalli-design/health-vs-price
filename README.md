# Does Eating Healthy Actually Cost More?

**A Python analysis of U.S. grocery prices that tests the belief that healthy food is expensive, and turns the results into simple rules for shopping smarter.**

![Python](https://img.shields.io/badge/Python-3-blue) ![pandas](https://img.shields.io/badge/pandas-data%20analysis-150458) ![Google Colab](https://img.shields.io/badge/Google%20Colab-notebook-F9AB00)

---

## The question

Budget shoppers are often told that healthy food costs more, so many stop trying. We wanted to know whether that's true once prices are compared fairly: **per 100 g, between similar products in the same aisle**, the way a shopper actually chooses.

**Who this is for:** budget-conscious shoppers, and anyone designing tools or policy to make healthy eating more affordable.

## Key findings

**1. In the same aisle, the healthier product usually costs less.**
Nutri-Score A/B products cost about **17% less per 100 g** than D/E products in the same aisle, and no aisle showed a significant price premium for health.

![Healthier vs less healthy products in the same aisle](images/fig9_healthy_vs_unhealthy_same_aisle.png)

**2. The healthiest aisles are also the cheapest.**
Legumes, vegetables, milk and yogurt, plain grains and fruit cost about **$1 per 100 g**. Chocolate, biscuits, nuts and cheese cost $2.30–6.

![Typical price per 100 g by food group](images/fig8_price_by_aisle.png)

**3. "Healthy is expensive" likely comes from how people compare prices.**
Per package, less-processed food costs about 11% more. Per 100 g, healthier food is cheaper. The sticker price hides the real cost.

**4. Store brands are the biggest saving.**
Store brands cost about **42% less per 100 g** than national brands in the same aisle, and were healthier in 10 of 14 aisles.

![Store brands vs national brands in the same food group](images/fig13_store_vs_national_brands.png)

**5. Where you shop matters.**
The exact same product varied by a median of **14%** between the cheapest and priciest store.

![Same product, different store](images/fig14_same_product_different_store.png)

**6. A sale tag isn't a better deal.**
Ultra-processed products go on sale slightly more often, but the average discount is about the same (around 24%) at every processing level.

![Share of price tags on promotion by processing level](images/fig15_promotions_by_processing.png)

## Smart-shopper rules

| Rule | Why |
|---|---|
| Read the price per 100 g, not the package price | Package size hides the real cost |
| Swap down a Nutri-Score grade, not up in price | Healthier options in the same aisle are usually cheaper |
| Try the store brand first | Cheaper and often healthier |
| Know your store | The same item can cost noticeably more elsewhere |
| Don't let sale tags steer the cart | Promotions cluster on snacks without bigger discounts |

## Data

| Source | What it provides |
|---|---|
| [Open Food Facts](https://world.openfoodfacts.org/data) | Product details, Nutri-Score (health grade A–E), NOVA processing level, nutrients, package size |
| [Open Prices](https://prices.openfoodfacts.org) | Real shelf prices, photographed by shoppers, matched to products by barcode |

From about 988,000 U.S. products, 9,858 had both a shelf price and a known package size, which is what price per 100 g requires. The data files are too large for GitHub and can be downloaded from the links above.

## Approach

1. **Cleaned** the product and price data: fixed barcodes, removed duplicates and impossible values, and used the regular (non-sale) price.
2. **Joined** products to prices by barcode and calculated **price per 100 g**.
3. **Compared like with like:** every price test compares products within the same food group, so we measure the effect of health on price rather than the difference between aisles.
4. **Tested 8 hypotheses** using price ratios with 95% confidence intervals, adjusting for testing many food groups at once.
5. **Prototyped a swap app** that suggests a healthier, cheaper, similar product for a scanned item.

## Limitations

- **Concentrated price data:** about 85% of prices come from California and most from one contributor, so results describe these stores rather than all U.S. prices. The patterns are relative comparisons within aisles, so we'd expect them to hold elsewhere, but more regional data would confirm it.
- **Crowd-sourced labels:** Open Food Facts is user-entered, so some products have missing or incorrect information.
- **Correlation, not causation:** we show which products cost more, not why.

## Next step: SmartCart

A gamified app built on Open Prices: scan a product, see whether it's a good price for its aisle, get up to three healthier and cheaper swaps, and earn points. Every price tag a user photographs also adds to the open data the app relies on.

## Repository contents

| File | Description |
|---|---|
| `B02-Health-Vs-Price-US-Packaged-Groceries.ipynb` | Full analysis: cleaning, hypotheses, charts and conclusions |
| `images/` | Key charts used in this README |

## How to run

1. Open the notebook in [Google Colab](https://colab.research.google.com/) or Jupyter.
2. Download the data from Open Food Facts and Open Prices.
3. Update the `path` variable in the notebook to the folder where your data is saved.
4. Run all cells.

**Tools:** Python, pandas, NumPy, SciPy, Matplotlib, Seaborn, Google Colab

## My role

I wrote the code and charts comparing health and environmental scores within each food group, and I presented the price-premium section, which asked whether customers pay more to eat healthier. I also set up this repository.

## Team

Built for BA780 Introduction to Data Analytics, MS in Business Analytics, Boston University Questrom School of Business (Fall 2026).

- Aashna Soni
- Alex Chen
- Dhruv Thakkar
- Gauri Nandihalli
- Peter Chang
