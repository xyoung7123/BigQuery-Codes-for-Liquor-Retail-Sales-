[Liquor Sales Dashboard.xlsx](https://github.com/xyoung7123/BigQuery-Codes-for-Liquor-Retail-Sales-/files/9077942/Liquor.Sales.Dashboard.xlsx)
# BigQuery-Codes-for-Liquor-Retail-Sales-
BigQuery Codes for Sales Analysis of Liquor Business

--Checking out all the relevant columns required for analysis
SELECT * FROM `bigquery-public-data.iowa_liquor_sales.sales` LIMIT 1000

--Selecting only top 10000 rows from the sales record
SELECT invoice_and_item_number, date, store_name, city, store_location, county,category_name, vendor_name, item_description, bottle_volume_ml, state_bottle_cost, state_bottle_retail, bottles_sold, sale_dollars, volume_sold_liters       
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
order by volume_sold_liters desc
LIMIT 10000


SELECT  *
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
LIMIT 100000


SELECT  invoice_and_item_number, date, city, store_location, 
category_name, vendor_name, item_description,
 bottle_volume_ml, state_bottle_cost, state_bottle_retail, 
 bottles_sold, sale_dollars, volume_sold_liters
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
order by sale_dollars desc
limit 100000


--CHECKING FOR DUPLICATES
select  count(distinct vendor_name) 
from `bigquery-public-data.iowa_liquor_sales.sales` 


--CHECKING FOR LENGTH OF CELL
 SELECT LENGTH(invoice_and_item_number)
 FROM `bigquery-public-data.iowa_liquor_sales.sales` 



--CHECKING LENGTH OF STRINGS
 SELECT invoice_and_item_number
 FROM `bigquery-public-data.iowa_liquor_sales.sales` 
 WHERE LENGTH(invoice_and_item_number)>15


--CHECKING FOR TEXT STRINGS
SELECT invoice_and_item_number
 FROM `bigquery-public-data.iowa_liquor_sales.sales` 
 WHERE SUBSTR(invoice_and_item_number, 1, 15) = 'S150842-0020010'


-- USING THE TRIM TO CHECK FOR EMPTY SPACES
 SELECT DISTINCT invoice_and_item_number
 FROM `bigquery-public-data.iowa_liquor_sales.sales` 
 WHERE TRIM(invoice_and_item_number) = 'S150842-0020010'


--CHECKING NUMERICAL DATA FOR OUTLINERS
SELECT MIN(state_bottle_cost) AS min_cost, MAX(state_bottle_cost) AS max_cost
FROM `bigquery-public-data.iowa_liquor_sales.sales` 

--CHECKING FOR NULL VALUES OR EMPTY CELLS
SELECT *
FROM `bigquery-public-data.iowa_liquor_sales.sales` 
WHERE category_name IS NULL

--CHECKING FOR DUPLICATES
SELECT COUNT(*)
FROM `bigquery-public-data.iowa_liquor_sales.sales` 


--Extract Year from the date 
SELECT 
EXTRACT(YEAR FROM date) as year,
COUNT(*) AS Number_of_sales
FROM 
`bigquery-public-data.iowa_liquor_sales.sales`
GROUP BY
year
ORDER BY Number_of_sales DESC

--deriving unit product price
SELECT 
vendor_name,
item_description,
state_bottle_cost,
state_bottle_retail,
(state_bottle_cost/state_bottle_retail)*100 as Unit_Price
FROM 
`bigquery-public-data.iowa_liquor_sales.sales` 
WHERE 
state_bottle_retail <> 0


--Deriving Profit
SELECT 
state_bottle_cost, 
state_bottle_retail,
state_bottle_retail	- state_bottle_cost as unit_profit
FROM 
`bigquery-public-data.iowa_liquor_sales.sales`


--Selecting Total Profit
SELECT 
state_bottle_cost, 
state_bottle_retail,
bottles_sold,
(state_bottle_retail	- state_bottle_cost) * bottles_sold as unit_profit
FROM 
`bigquery-public-data.iowa_liquor_sales.sales` 

