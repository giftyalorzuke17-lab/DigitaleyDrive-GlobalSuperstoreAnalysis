# Global Superstore: Sales and Profitability Analysis

Capstone project for the Digitaley Drive Data Analyst Bootcamp.

## Overview

Global Superstore is a New York based online retailer with customers in 147 countries and three product categories: Office Supplies, Furniture and Technology. This project analyses 51,290 order lines (1 Jan 2012 to 31 Dec 2015) to find where the business makes and loses money, and what management should do about it.

**Main finding:** discounts, not demand or shipping, are the biggest cause of losses.

## Dataset

`global_superstore_2016.xlsx` has three sheets:

| Sheet | Contents |
|---|---|
| Orders | 51,290 order lines: dates, customer, location, product, sales, quantity, discount, profit, shipping cost |
| Returns | 1,079 returned orders |
| People | Regional managers |

**Cleaning checks:** no duplicate rows, and no missing values apart from Postal Code, which no question uses. Customers are identified by Customer ID, because 35 customer names are shared by different IDs.

## Tools

Excel and Power BI. Power Query was used to load and check the data, a data model and DAX measures to calculate the results, and Power BI for the dashboard.

## Business questions and answers

Questions 1 and 3 use 2014. All others use 2012 to 2015. Averages are per order line.

| # | Question | Answer |
|---|---|---|
| 1a | Top 3 countries by profit, 2014 | United States ($81,727), China ($44,474), India ($32,897) |
| 1b | Top products in each | US: Canon imageCLASS 2200 Advanced Copier ($9,520), GBC Ibimaster 500 ($2,968), HP Designjet T520 ($2,800). China: Hon Executive Leather Armchair ($1,430), Samsung Smart Phone ($1,081), Hamilton Beach Refrigerator ($1,080). India: Apple Smart Phone ($2,818), Cisco Smart Phone ($1,253), Memorex Router ($1,207) |
| 2 | Highest average US shipping cost | Copiers ($165.29), Machines ($132.25), Tables ($69.95) |
| 3a | Nigeria's profit, 2014 | -$24,956, last of 40 African countries. Africa overall made $26,687 |
| 3b | Why | Average discount is 70% on every line (rest of Africa: 1.7%). Shipping is lower ($8.71 vs $23.22), so it is not the cause |
| 4a | Least profitable sub-category in Southeast Asia | Tables (-$18,618) |
| 4b | Stop selling anywhere? | Indonesia first (-$10,680 at a 47% discount). Tables also lose money in Thailand, the Philippines, Myanmar and Vietnam |
| 5a | Least profitable US city (10+ orders) | Lancaster (-$157.37 average profit per line) |
| 5b | Why | One 3D printer sold at 70% off lost $6,600. Without it, the average is about -$14 |
| 6 | Highest average profit in Australia | Appliances ($139.01) |
| 7 | Most valuable customers | Tamara Chand ($8,745), Raymond Buch ($6,807), Adrian Barton ($5,363). They mostly buy Copiers and Binders. The top 10% of customers earn about 87% of net profit |

## Recommendations

1. **Cap discounts.** Add an approval rule above a set level, such as 30%.
2. **Fix Nigeria pricing.** Review the flat 70% discount, which Uganda and Zimbabwe also have.
3. **Stop selling Tables in Indonesia**, and review the other four loss-making countries.
4. **Retain top customers**, focusing on buyers of Copiers, Binders and Phones.
5. **Verify the data.** Flat discounts per country look like a pricing rule or a data issue.

## How the analysis was done

1. **Load and clean (Power Query).** Load the `Orders` sheet, set Order Date to a date type, remove duplicates, check for blanks, and add a Year column from Order Date.
2. **Model.** Use `Orders` as the main table. The `Returns` and `People` sheets can be related to it (by Order ID and Region), but no question needed them.
3. **Create DAX measures.**

```DAX
Total Profit = SUM(Orders[Profit])
Total Sales = SUM(Orders[Sales])
Avg Profit per Line = AVERAGE(Orders[Profit])
Avg Shipping Cost = AVERAGE(Orders[Shipping Cost])
Avg Discount = AVERAGE(Orders[Discount])
Order Count = DISTINCTCOUNT(Orders[Order ID])
```

4. **Build visuals and answer each question.**

| # | How it was answered |
|---|---|
| 1 | Filter Year to 2014. Bar chart of Total Profit by Country with a Top 3 filter, then a table of Product Name by Total Profit with a Top 3 filter for each country |
| 2 | Filter Country to United States. Bar chart of Avg Shipping Cost by Sub-Category, Top 3 |
| 3 | Filter Year to 2014 and Market to Africa. Compare Total Profit, Avg Shipping Cost and Avg Discount by Country |
| 4 | Filter Country to the eight Southeast Asian countries. Total Profit by Sub-Category, then Total Profit by Country for Tables |
| 5 | Filter Country to United States and Order Count to 10 or more. Avg Profit per Line by City, sorted lowest first |
| 6 | Filter Country to Australia. Avg Profit per Line by Sub-Category |
| 7 | Total Profit by Customer ID, with Category and Sub-Category as a breakdown for the top customers |

Excel pivot tables can be used to cross-check the same totals.

# Project files

| File | Description |
|---|---|
| `global_superstore_2016.xlsx` | Source data |
| `[your file name].pbix` | Power BI report with the data model, measures and dashboard |
| Dashboard screenshot | Picture of the dashboard (also posted on LinkedIn) |
| Presentation deck | Slides summarising the findings |

 

Author

[Gifty Alorzuke] | [www.linkedin.com/in/giftyalorzuke]

# DigitaleyDrive-GlobalSuperstoreAnalysis
final capstone project on global superstore dataset
