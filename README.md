# Zomato Analytics Dashboard

An interactive Power BI dashboard that analyzes 10,000 food-delivery orders: customer ratings, delivery time, order value, delivery partners, payment methods, and discount usage across 7 cuisines.

**Tools:** Power BI, Excel

---

## Dataset

| Item | Detail |
|---|---|
| Source | Kaggle: Zomato DATASET] |
| File | `Zomato.xlsx` |
| Size | 10,000 orders, 15 columns |
| Period | 17 Jan 2023 to 16 Jan 2025 |

> Customer names, restaurant names, and review text in this file appear to be synthetic. The findings below describe this dataset only and should not be read as real-world market trends.

### Data dictionary

| Column | Type | Description |
|---|---|---|
| Order_ID | Text | Unique order identifier |
| Customer_Name | Text | Customer name |
| Customer_Location | Text | Customer location |
| Restaurant_Name | Text | Restaurant name |
| Restaurant_Location | Text | Restaurant location |
| Cuisine | Text | Cuisine type (7 categories) |
| Order_Date | Date | Date the order was placed |
| Delivery_Time_Minutes | Integer | Delivery time, 10 to 120 minutes |
| Order_Amount | Decimal | Order value, about 100 to 2,000 |
| Delivery_Partner | Text | Partner A, B, C, or D |
| Payment_Method | Text | UPI, Net Banking, Cash, Credit Card, Debit Card |
| Rating | Integer | Customer rating, 1 to 5 |
| Review_Text | Text | Customer review |
| Review_Date | Date | Date the review was written |
| Is_Discount_Applied | Boolean | Whether a discount was used |

## Data quality checks

| Check | Result |
|---|---|
| Rows / columns | 10,000 / 15 |
| Missing values | 0 |
| Duplicate rows | 0 |
| Unique Order_IDs | 10,000 |
| Review_Date earlier than Order_Date | 4,973 rows (49.7%), flagged as a known issue; Review_Date is not used in any KPI |

## Objectives

1. Measure overall customer satisfaction and delivery performance.
2. Compare cuisines on order volume, rating, order value, and delivery time.
3. Compare delivery partners on volume, rating, and delivery time.
4. Understand payment-method mix and discount usage.
5. Test whether delivery time or order value is related to rating.

## Key findings

### Overall

| Metric | Value |
|---|---|
| Total orders | 10,000 |
| Total order value | 10,533,747 |
| Average order amount | 1,053.4 |
| Average rating | 3.0 / 5 |
| Average delivery time | 65.2 minutes |
| Orders with a discount | 49.9% (4,991 orders) |

### By cuisine

| Cuisine | Orders | Avg rating |
|---|---|---|
| Thai | 1,470 | 2.96 |
| American | 1,459 | 3.02 |
| Italian | 1,444 | 2.98 |
| Indian | 1,442 | 2.98 |
| Japanese | 1,422 | 3.04 |
| Chinese | 1,408 | 3.01 |
| Mexican | 1,355 | 2.99 |

### By delivery partner

| Partner | Orders | Avg rating | Avg delivery (min) |
|---|---|---|---|
| Partner A | 2,523 | 3.02 | 65.1 |
| Partner B | 2,569 | 3.02 | 65.1 |
| Partner C | 2,411 | 3.02 | 65.7 |
| Partner D | 2,497 | 2.93 | 64.9 |

### By payment method

| Method | Orders | Avg order amount | Avg rating |
|---|---|---|---|
| UPI | 2,024 | 1,063.9 | 3.00 |
| Net Banking | 2,013 | 1,046.3 | 3.03 |
| Cash | 1,997 | 1,049.5 | 2.96 |
| Credit Card | 1,984 | 1,039.0 | 2.96 |
| Debit Card | 1,982 | 1,068.1 | 3.03 |

### Discounts

| Group | Orders | Avg order amount | Avg rating |
|---|---|---|---|
| Discount applied | 4,991 | 1,043.3 | 3.03 |
| No discount | 5,009 | 1,063.4 | 2.97 |

### Delivery time and rating

| Delivery time band | Orders | Avg rating |
|---|---|---|
| 10 to 30 min | 1,874 | 2.99 |
| 31 to 60 min | 2,696 | 3.03 |
| 61 to 90 min | 2,719 | 2.99 |
| 91 to 120 min | 2,711 | 2.98 |

### Observations

- Orders are spread almost evenly across all 7 cuisines (1,355 to 1,470 each) and all 4 delivery partners.
- The average rating stays close to 3.0 for every cuisine, partner, and payment method, so differences between groups are small.
- Partner D has the lowest average rating (2.93) even though it has the fastest average delivery (64.9 minutes).
- Ratings are spread evenly from 1 to 5 (about 2,000 orders each). Delivery time and rating are essentially uncorrelated (r = -0.006), and so are order amount and rating (r = -0.003). In this dataset, faster delivery does not lead to higher ratings.
- Discounted orders have a slightly lower average order amount (1,043.3 vs 1,063.4) and a slightly higher rating (3.03 vs 2.97).
- Order volume grew from 4,714 orders in 2023 to 5,083 in 2024 (2025 covers only 16 days: 203 orders).

## Dashboard

[ADD 2 to 3 screenshots, for example: `![Overview](docs/overview.png)`]

**Filters:** cuisine, delivery partner, payment method, order date.

### KPI definitions (DAX)

These assume the data table is named `Zomato`.

```DAX
Total Orders = COUNTROWS(Zomato)
Total Order Value = SUM(Zomato[Order_Amount])
Avg Order Amount = AVERAGE(Zomato[Order_Amount])
Avg Rating = AVERAGE(Zomato[Rating])
Avg Delivery Time = AVERAGE(Zomato[Delivery_Time_Minutes])
Discount Rate = DIVIDE(COUNTROWS(FILTER(Zomato, Zomato[Is_Discount_Applied] = TRUE())), COUNTROWS(Zomato))
```

## Repository structure

```
Zomato-Dashboard/
├── data/        # Zomato.xlsx
├── dashboard/   # .pbix file and exported PDF
├── docs/        # screenshots
└── README.md
```

## How to use

1. Download the repository.
2. Open the `.pbix` file in Power BI Desktop.
3. If prompted, point the data source to `data/Zomato.xlsx`.

## Author

Ashi Jain, [GitHub](https://github.com/Ashijain30)

## 🖼️ Dashboard Preview
![Zomato Dashboard Preview]<img width="1573" height="786" alt="DASHBOARD" src="https://github.com/user-attachments/assets/fb72d52d-e90f-4c8e-9dd8-2b8bbe5d9120" />


---


---




