# BigQuery-Codes-for-Liquor-Retail-Sales-
BigQuery Codes for Sales Analysis of Liquor Business

--Checking out all the relevant columns required for analysis
SELECT * FROM `bigquery-public-data.iowa_liquor_sales.sales` LIMIT 1000

--Selecting only top 10000 rows from the sales record
SELECT invoice_and_item_number, date, store_name, city, store_location, county,category_name, vendor_name, item_description, bottle_volume_ml, state_bottle_cost, state_bottle_retail, bottles_sold, sale_dollars, volume_sold_liters       
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
order by volume_sold_liters desc
LIMIT 10000
