# Does Eating Healthy Actually Cost More?

**Matching about 988,000 U.S. grocery products to real shelf prices to test one of the most common beliefs about food, and turning the results into rules shoppers can actually use.**

![Python](https://img.shields.io/badge/Python-3-3776AB?logo=python&logoColor=white) ![pandas](https://img.shields.io/badge/pandas-150458?logo=pandas&logoColor=white) ![NumPy](https://img.shields.io/badge/NumPy-013243?logo=numpy&logoColor=white) ![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?logo=scipy&logoColor=white) ![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?logo=googlecolab&logoColor=white)

[View the full notebook](B02-Health-Vs-Price-US-Packaged-Groceries.ipynb) · [Key findings](#key-findings) · [Approach](#approach) · [My role](#my-role)

---

## TL;DR

Shoppers on a budget are told healthy food costs more. **Compared fairly, per 100 g in the same aisle, it doesn't.** Healthier products were about 17% cheaper than less healthy ones, and the biggest savings came from choosing store brands and the right store. The "healthy is expensive" belief likely comes from comparing package prices instead of unit prices.

| Result | Number |
|---|---|
| Healthier (Nutri-Score A/B) vs less healthy (D/E) products, same aisle | **17% cheaper** per 100 g |
| Store brands vs national brands, same aisle | **42% cheaper** per 100 g |
| Same product, cheapest vs priciest store | **14%** price gap (median product) |
| Aisles where healthy food carries a significant price premium | **0** |

![Healthier vs less healthy products in the same aisle](images/fig9_healthy_vs_unhealthy_same_aisle.png)

## The business problem

If budget shoppers believe healthy eating is unaffordable, many stop trying. That belief shapes what people buy, how retailers promote products, and how health programs talk about cost. This project asks whether the belief holds up in real shelf-price data, and where shoppers can actually save.

**Who can use this:** retailers and grocery apps designing price and promotion tools, public health teams working on food affordability, and budget-conscious shoppers.

## Key findings

**1. In the same aisle, the healthier product usually costs less.**
Nutri-Score A/B products cost about 17% less per 100 g than D/E products, and no aisle showed a significant health premium (chart above).

**2. The healthiest aisles are also the cheapest.**
Legumes, vegetables, milk and yogurt, plain grains and fruit cost about $1 per 100 g. Chocolate, biscuits, nuts and cheese cost $2.30–6.

![Typical price per 100 g by food group](images/fig8_price_by_aisle.png)

**3. "Healthy is expensive" is a comparison problem.**
Per package, less-processed food costs about 11% more. Per 100 g, healthier food is cheaper. The sticker price hides the real cost.

**4. Store brands are the biggest saving.**
They cost about 42% less per 100 g than national brands in the same aisle, and were healthier in 10 of 14 aisles.

![Store brands vs national brands in the same food group](images/fig13_store_vs_national_brands.png)

**5. Where you shop matters.**
The exact same barcode varied by a median of 14% between the cheapest and priciest store. Whole Foods was not more expensive for identical items.

![Same product, different store](images/fig14_same_product_different_store.png)

**6. A sale tag isn't a better deal.**
Ultra-processed products go on sale slightly more often, but the average discount is about the same (around 24%) at every processing level.

![Share of price tags on promotion by processing level](images/fig15_promotions_by_processing.png)

## Recommendations

| For | Recommendation |
|---|---|
| Shoppers | Compare price per 100 g, swap down a Nutri-Score grade, and try the store brand first |
| Retailers | Make unit prices easier to read and promote healthy staples as often as snacks |
| Product teams | Build swap suggestions into shopping apps (prototype below) |

## Approach

1. **Data engineering:** cleaned two crowd-sourced datasets, repaired barcodes that had lost leading zeros, removed duplicates and impossible values, and used regular (non-sale) prices.
2. **Data integration:** joined products to shelf prices by barcode and calculated price per 100 g. About 988,000 products narrowed to 9,858 with both a price and a package size.
3. **Fair comparisons:** every price test compares products within the same food group, so the result reflects health, not the difference between aisles.
4. **Hypothesis testing:** tested 8 hypotheses using price ratios on log prices with 95% confidence intervals, and adjusted p-values for testing many food groups at once (false discovery rate).
5. **Product prototype:** built a rule-based swap engine that finds a healthier, cheaper, similar product for a scanned item. It found a swap for 89% of Nutri-Score D/E products.

## Skills demonstrated

| Area | Details |
|---|---|
| Data wrangling | pandas cleaning, joins on barcode, handling missing and invalid values at scale |
| Statistics | Welch t-tests on log prices, confidence intervals, Spearman correlation, multiple-testing correction |
| Visualization | Matplotlib and Seaborn charts designed around one question each |
| Communication | Findings framed for a non-technical audience, with clear recommendations |
| Product thinking | Translated analysis into a working app prototype |

## Next step: SmartCart

A gamified app built on Open Prices: scan a product, see whether it's a good price for its aisle, get up to three healthier and cheaper swaps, and earn points. Every price tag a user photographs adds to the open data the app relies on.

## Limitations

- **Concentrated price data:** about 85% of prices come from California and most from one contributor. The findings are relative comparisons within aisles, so we'd expect the patterns to hold elsewhere, but more regional data would confirm it.
- **Crowd-sourced labels:** some products have missing or incorrect information.
- **Correlation, not causation:** the analysis shows which products cost more, not why.

## Data

| Source | What it provides |
|---|---|
| [Open Food Facts](https://world.openfoodfacts.org/data) | Product details, Nutri-Score (health grade A–E), NOVA processing level, nutrients, package size |
| [Open Prices](https://prices.openfoodfacts.org) | Real shelf prices photographed by shoppers, matched by barcode |

The data files are too large for GitHub and can be downloaded from the links above.

## Repository contents and how to run

| File | Description |
|---|---|
| `B02-Health-Vs-Price-US-Packaged-Groceries.ipynb` | Full analysis: cleaning, hypotheses, charts and conclusions |
| `images/` | Key charts used in this README |

1. Open the notebook in [Google Colab](https://colab.research.google.com/) or Jupyter.
2. Download the data from the sources above.
3. Update the `path` variable to the folder where the data is saved.
4. Run all cells.

## My role

- **Analysis and code:** wrote the Python code and charts for the section comparing health scores (Nutri-Score) with environmental scores (Green-Score), including the within-aisle comparisons that showed where the healthier product is also the lower-impact one.
- **Storytelling across the project:** wrote the chart titles, guiding questions and key takeaways for the figures so each chart answers one clear question for a non-technical reader.
- **Quality review:** checked the notebook against the project requirements and flagged inconsistencies between the written conclusions and the code outputs before submission.
- **Presentation:** shaped the overall storyline of the final presentation and led the section asking whether customers pay a price premium to eat healthier, covering the across-aisle prices, the within-aisle comparison and the promotions analysis.
- **Q&A preparation:** prepared answers on the methodology, such as why prices were compared per 100 g and how far the findings generalize beyond California.
- **Portfolio:** built and documented this GitHub repository.

## Team

A team project for BA780 Introduction to Data Analytics, MS in Business Analytics, Boston University Questrom School of Business (Fall 2026).

Aashna Soni · Alex Chen · Dhruv Thakkar · Gauri Nandihalli · Peter Chang


**Gauri Nandihalli** · MS in Business Analytics, Boston University
