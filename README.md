# ShopSmart Retail Sales, Inventory and Returns Analysis

An end-to-end Excel analysis of 50,000 orders across 25 stores, 500 products and 5,000 customers. Using Power Query, Excel formulas, pivot tables and an interactive dashboard, I investigated management's three concerns (sales fluctuation, inventory shortage and rising returns) and produced eight actionable recommendations.

**Tools:** Excel | Power Query | XLOOKUP | Pivot Tables | Pivot Charts | Slicers

---

## Dashboard

![Dashboard](images/dashboard.png)


---

## Business Problem

Management noticed three issues:

1. Fluctuating sales
2. Inventory shortages
3. Increasing product returns

**Objective:** test each concern against the data, answer 10 business questions, and recommend what to do next.

---

## Headline Results

| Metric | Result |
|---|---|
| Total revenue | ₦2.25B |
| Orders | 50,000 (only 33% completed) |
| Customers | 5,000 |
| Top product | Beauty Item 210 (₦7.38M) |
| Top category | Beauty (₦523M) |
| Peak month | December (₦201M) |
| Top region | South (₦724.5M) |
| Returned orders | 2,442 (₦63.4M refunded) |

---

## Key Findings

1. **Sales fluctuation is mild and volume-driven.** Monthly revenue ranges from ₦170.7M (February) to ₦201.0M (December), about 18%. The completion rate stays near 33% every month.
2. **Two-thirds of orders earn nothing.** 16,861 orders were cancelled and 16,610 are pending; only 16,529 were completed.
3. **Store gaps are larger than monthly gaps.** The Lagos stores combined earn ₦377M, while Kano earns ₦81M.
4. **Stock is not placed where demand is.** Only 21 of 500 stock lines (4%) are at or below reorder level, but stock and store revenue are almost uncorrelated (-0.07). The lowest-stocked stores are STR011 Kaduna (2,570 units), STR023 Abuja (3,139) and STR005 Enugu (3,349).
5. **Returns come from every cause.** Late Delivery (650), Wrong Item (631), Customer Changed Mind (625) and Damaged (594). Beauty has the most returns (614).
6. **Return controls are weak.** 67% of returns are linked to cancelled or pending orders, and 1,787 refunds exceed the order value.

**Top risk:** revenue depends on order completion, and refunds are being logged against orders that never completed.
**Top opportunity:** Kano, Awka and Enugu underperform; lifting them towards average store revenue is the clearest growth room.

---

## Recommendations

| # | Recommendation | Action | Target |
|---|---|---|---|
| 1 | Fix order completion | Follow up pending orders within 24 hours, send payment reminders, record cancellation reasons | Completion from 33% to 45% |
| 2 | Plan for peaks and dips | Run promotions in low months (February, June); secure stock before October to December | Monthly spread under 10% |
| 3 | Rebalance stock by demand | Move stock to Kaduna, Abuja (STR023) and Enugu | Stock-to-sales correlation above 0.5 |
| 4 | Automate reorders | Alert at reorder level; review flagged lines weekly | No line below reorder level for over 7 days |
| 5 | Stock top sellers in several stores | Hold the top 50 products in more than one store | Fewer stock-outs |
| 6 | Cut preventable returns | Add a pick-and-pack check; review courier performance | Returns down 20% |
| 7 | Tighten refund controls | Refund only completed orders, capped at order value | Zero returns on non-completed orders |
| 8 | Beauty quality review | Review descriptions, packaging and supplier quality | Beauty returns down 25% |

---

## Data Model

| Table | Primary key | Foreign keys |
|---|---|---|
| Customer | Customer_ID | |
| Product | Product_ID | |
| Orders | Order_ID | Customer_ID, Product_ID, Store_ID |
| Store | Store_ID | |
| Return | Return_ID | Order_ID |
| Employee | Employee_ID | Store_ID |
| Supplier | Supplier_ID | |
| Inventory | Inventory_ID | Product_ID, Store_ID |

Suppliers are linked to products through Brand + " Supplies" = Supplier_Name.

---

## Method

**1. Data preparation (Power Query)**
- Combined nine source files into one master workbook
- Cleaned and trimmed text, removed duplicates, formatted dates
- Converted money columns to number format with comma separators
- Added to **Orders:** Total_Revenue and Category
- Added to **Inventory:** Unit_Cost, Inventory_Value and Reorder_Status
- Used Group By on Orders and Returns to get total orders, total returns, return rate and total customers by category

**2. Calculations and lookups**
- Headline figures with Excel formulas (total revenue, quantity sold, average order value, counts)
- XLOOKUP to bring in names, categories, prices and suppliers

**3. Analysis and visualisation**
- 14 pivot tables (product, month, store, category, region, state, gender, segment, customers, returns)
- Pivot charts and an interactive dashboard with slicers

**Calculation logic**

| Measure | Definition |
|---|---|
| Total_Revenue | Quantity × Unit_Price × (1 − Discount %) for Completed orders, otherwise 0; shipping excluded |
| Inventory_Value | Stock_On_Hand × Unit_Cost (at cost) |
| Reorder_Status | "Reorder Needed" if Stock_On_Hand ≤ Reorder_Level |
| Return rate | Returned orders ÷ total orders |
| Average order value | Total revenue ÷ number of orders |

---

## Assumptions and Data Notes

- Revenue counts completed orders only; cancelled and pending orders count as 0.
- Orders and returns cover January to December 2025. Inventory is a snapshot with restock dates from July to October 2026, so stock levels are not from the sales year.
- Inventory is valued at cost, not selling price.
- Four stores share the name "ShopSmart Lagos", so store-level analysis uses Store_ID.
- Four customers share the name Nicole Smith, so customer-level analysis uses Customer_ID.
- Average order value across all 50,000 orders is ₦44,937; across completed orders only it is about ₦135,933.

---

## Repository Contents

```
├── README.md
├── ShopSmart_Analysis.xlsx          # master workbook, pivots and dashboard
├── ShopSmart_Management_Brief.docx  # management summary
└── images/
    └── dashboard.png
```

---

## Contact

**[Fajobi Adijat Oluwatoyin ]** | [https://www.linkedin.com/in/adijat-fajobi] | [oluwatoyinfajobi2004@gmail.com]
