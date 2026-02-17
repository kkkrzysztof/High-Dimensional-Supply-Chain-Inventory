# About the Project:

This is a BI/Analytics project done based on the Kaggle dataset entitled "[High-Dimensional Supply Chain Inventory Dataset](https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset/data)."

## Project Legend:

:white_check_mark: Done
:x: Not done
:construction: In progress

## Project Tasks:

- :white_check_mark: Ensuring that localization is in English (File>Options and settings>Options>CURRENT FILE>Regional Settings>Locale for import>"English (United States)"; File>Options and settings>Options>GLOBAL>Regional Settings>Application language, Model language>"English (United States)"; System Settings>Time & language>Language & region>Region>Regional format>"English (United States)"); ensuring consistent decimal and datetime format so that it's not necessary to replace values e.g. decimal/thousand separators; used EN_US localization since the project is dedicated to English-speaking audiences
- :white_check_mark: Creating a "FolderPath" parameter to store the string of the path of the folder where the *.pbix file happens to be situated (good practice)
- :white_check_mark: Data Loading (loading from CSV with proper row delimiter; cleaning text, trimming text just in case; setting the first row as header); there is a separate query "load_data" for just fetching data, and another one calle "supply_chain_dataset" for changing datatypes
- :white_check_mark: Data Profiling (confirmed number of columns (15), confirmed consistent column-naming format ("Column_name"), setting datatypes, confirmed no nulls, confirmed no row duplicates (group by [Date]&[SKU_ID]&[Warehouse_ID]&[Supplier_ID]), confirmed no categorical duplicates (consistent naming: distinct value=distinct category))
- :white_check_mark: Fixed IDs for "correct alphabetic order" e.g SKU_1 -> SKU_01; this comes up in the visuals
- :white_check_mark: Creating a "dates" table
- :white_check_mark: Checked combinations of categorical variables (SKU_ID, Warehouse_ID, Supplier_ID, Region)
- :white_check_mark: Run summary statistics in PQ/M (discovered a column with zero variance, "Stockout_Events" - all values are 0)
- :white_check_mark: Calculating basic measures
- :white_check_mark: Using a DAX "_Measures" table ("_Measures = SELECTCOLUMNS( {} , "_", BLANK() )") for storing Measures (good practice)
- :white_check_mark: Done basic analysis of KPIs per various categories, measures
- :white_check_mark: Selecting a specific date format in Power BI Table View ("14 March 2001 (d mmmm yyyy)")
- :white_check_mark: Decided on "20" as the default margin size
- :white_check_mark: Setting explicit formatting for measures
- :white_check_mark: "Sales" report page finished
- :white_check_mark: "Regions" report page finished
- :white_check_mark: "Warehouses" report page finished
- :white_check_mark: "Suppliers" report page finished
- :white_check_mark: "SKUs" report page finished
- :white_check_mark: Add shadows to visuals
- :white_check_mark: Make the dashboard somewhat interactive/user-friendly/navigable (with tooltips, buttons, bookmarks, etc.)
- :construction: Turning "supply_chain_dataset" and "dates" Power Query queries into static CSV files (because we assume that no data (rows) is going to be added to either of those); it's for efficiency (no need for recalculation). I can use "Export query results" tool from Home>Output Data>Export query results.
- :construction: Describing the measures (definitions and interpretations)
- :construction: Creating my own theme and apply it globally
- :construction: Study the column meaning more deeply
- :construction: Thinking up new ways of analyzing the data (measures, columns)
- :construction: Make the dashboard pretty (good taste? may need tutorial for that)
- :x: Creating a custom theme for my dashboards and reports?
- :x: Designing a mobile view (might require Power BI Pro?)

# About the Dataset

## Overview

Based on the information from the [original dataset source repository](https://www.kaggle.com/datasets/ziya07/high-dimensional-supply-chain-inventory-dataset/data), here is the (mostly sourced) interpretation of the columns in the dataset:

1. **Date**: Daily timestamps spanning one year of activity.
2. **SKU-Level Detail**: Unique product identifiers (ID) with varying demand patterns.
3. **Warehouse and Region**: Spatial dimensions representing distribution networks. There are 5 warehouses and 4 regions in total.
4. **Units Sold**: Number of units sold in a day (simulated with seasonal trends and random noise).
5. **Inventory Levels**: Dynamic on-hand stock (at the end of the day in a specific warehouse) that evolves over time. Inventory level of an SKU in a warehouse changes based on the number of units sold and e.g. if inventory level for a day is 592, units sold for the next day is 17, and no amount of the SKU was delivered to the warehouse, then inventory level for the next day is 575 (=592-17).
6. **Supplier Lead Times**: Variable delivery delays for replenishment orders.
7. **Reorder Points and Quantities**: Inventory policy thresholds and simulated replenishments.
8. **Promotions**: Binary indicator of promotional periods influencing demand.
9. **Stockout Events**: Flags indicating when demand exceeds available inventory.
10. **Supplier Information**: Links products to specific suppliers with unique lead times.
11. **Cost and Price**: Realistic unit costs and selling prices with profit margins.
12. **Forecasted Demand**: Approximate prediction values reflecting planning estimates.

## Interpretations

Here are interpretations of columns created as a result of analyzing the data:

13. **Beginning Inventory Level**: The number of units (of a specific SKU) at the beginning of the day in a specific warehouse.
14. **Ending Inventory Level**: The original "Inventory Level" column, renamed for clarity.
15. **Units Arrived**: The column "Order Quantity" was renamed to "Units Arrived" (at the warehouse), because it refers specifically to the number of units ordered for the warehouse (not orders made by customers). Renamed to resolve ambiguity.

## Assumptions

Here are some implicit assumptions:

1. **Region**="Sold-to-region"="Ship-to-region" — I assume that "Region" means the region from which orders are made and where the orders are delivered; regions are associated with sales (units sold). Power Query region analysis showed that a single warehouse may correspond to different regions, so the region isn't the place where a warehouse is located.
2. **Suppliers** in this dataset are those who deliver SKUs to warehouses, not SKUs to customers. Power Query region analysis demonstrated that a single warehouse can cooperate with multiple suppliers, so a given supplier isn't necessarily limited to a specific warehouse.
3. **What a single row is**: A single transaction dataset row seems to correspond to the activity of each combination of day, SKU, warehouse, supplier, and region. A single row shows the number of SKU sold (with a specific price and specific cost) from a warehouse (and likely shipped as well) to a region, the number of SKUs delivered to a warehouse by a supplier, and the final number of the SKU at the end of the day.

## Observations

Here are some observations:

1. **SKU**: A specific SKU doesn't necessarily have to be supplied by all suppliers, which suggests some degree of specialization in terms of what suppliers can provide to warehouses.