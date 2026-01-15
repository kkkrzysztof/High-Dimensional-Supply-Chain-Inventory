# About the Project:

This is a BI/Analytics project done based on the Kaggle dataset entitled "[High-Dimensional Supply Chain Inventory Dataset](https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset/data)."

## Project Legend:

:white_check_mark: Done
:x: Not done
:construction: In progress

## Project Tasks:

- :white_check_mark: Set PBIX file's regional settings to US (to ensure proper decimal and date format so that it's not necessary to replace values e.g. decimal/thousand separator)
- :white_check_mark: Data Loading (loading from CSV with proper row delimiter; cleaning text, trimming text just in case; setting the first row as header)
- :white_check_mark: Data Profiling (confirmed number of columns (15), confirmed consistent column-naming format ("Column_name"), setting datatypes, confirmed no nulls, confirmed no row duplicates (group by [Date]&[SKU_ID]&[Warehouse_ID]&[Supplier_ID]), confirmed no categorical duplicates (consistent naming: distinct value=distinct category))
- :white_check_mark: Creating a "dates" table
- :white_check_mark: Checked combinations of categorical variables (SKU_ID, Warehouse_ID, Supplier_ID, Region)
- :white_check_mark: Run summary statistics in PQ/M (discovered a column with zero variance, "Stockout_Events" - all values are 0)
:construction: Calculating basic measures
- :white_check_mark: Done basic analysis of KPIs per various categories
:x: Make the dashboard pretty
:x: Make the dashboard interactive/user-friendly (with tooltips, buttons, bookmarks, etc.)

# About the Dataset:

Based on the information from the [original dataset source repository](https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset/data), here is the (mostly sourced) interpretation of the columns in the dataset:

1. **Date:** Daily timestamps spanning one year of activity.
2. **SKU-Level Detail:** Unique product identifiers (ID) with varying demand patterns.
3. **Warehouse and Region:** Spatial dimensions representing distribution networks.
4. **Units Sold:** Number of units sold in a day (simulated with seasonal trends and random noise).
5. **Inventory Levels:** Dynamic on-hand stock that evolves over time.
6. **Supplier Lead Times:** Variable delivery delays for replenishment orders.
7. **Reorder Points and Quantities:** Inventory policy thresholds and simulated replenishments.
8. **Promotions:** Binary indicator of promotional periods influencing demand.
9. **Stockout Events:** Flags indicating when demand exceeds available inventory.
10. **Supplier Information:** Links products to specific suppliers with unique lead times.
11. **Cost and Price:** Realistic unit costs and selling prices with profit margins.
12. **Forecasted Demand:** Approximate prediction values reflecting planning estimates.