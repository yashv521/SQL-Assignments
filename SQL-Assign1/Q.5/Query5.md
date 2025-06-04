# Completed Orders in August 2023

## Business Problem
After running similar reports for a previous month, the business team now needs all completed orders in August 2023 for analysis. This data will help in performance assessment and identifying trends in order completion.


## Fields to Retrieve
- `PRODUCT_ID` 
- `PRODUCT_TYPE_ID` 
- `PRODUCT_STORE_ID`  
- `TOTAL_QUANTITY` 
- `INTERNAL_NAME` 
- `FACILITY_ID` 
- `EXTERNAL_ID` 
- `FACILITY_TYPE_ID` 
- `ORDER_HISTORY_ID` 
- `ORDER_ID` 
- `ORDER_ITEM_SEQ_ID` 
- `SHIP_GROUP_SEQ_ID` 

## Query Solution
```sql
SELECT 
  PR.PRODUCT_ID,
  PR.PRODUCT_TYPE_ID,
  OH.PRODUCT_STORE_ID,
  OI.QUANTITY AS TOTAL_QUANTITY,
  PR.INTERNAL_NAME,
  F.FACILITY_ID,
  OH.EXTERNAL_ID,
  F.FACILITY_TYPE_ID,
  OHS.ORDER_HISTORY_ID,
  OH.ORDER_ID,
  OI.ORDER_ITEM_SEQ_ID,
  OI.SHIP_GROUP_SEQ_ID
FROM order_header AS OH
JOIN order_status AS OS ON OH.ORDER_ID = OS.ORDER_ID
JOIN order_item AS OI ON OH.ORDER_ID = OI.ORDER_ID
JOIN product AS PR ON PR.PRODUCT_ID = OI.PRODUCT_ID
JOIN product_store AS PS ON OH.PRODUCT_STORE_ID = PS.PRODUCT_STORE_ID
JOIN order_item_ship_group AS OISG ON OH.ORDER_ID = OISG.ORDER_ID
JOIN facility AS F ON OISG.FACILITY_ID = F.FACILITY_ID
JOIN order_history AS OHS ON OH.ORDER_ID = OHS.ORDER_ID
WHERE OS.STATUS_ID = 'ORDER_COMPLETED'
  AND OS.STATUS_DATETIME BETWEEN '2023-08-01' AND '2023-09-01';

```
