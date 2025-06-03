# List of All Active Physical Products

## Business Problem
The merchandising team often needs a list of all active physical products to manage logistics, warehousing, and shipping efficiently.

## Fields to Retrieve
- `PRODUCT_ID` 
- `PRODUCT_TYPE_ID` 
- `INTERNAL_NAME` 

## Query Solution
```sql
SELECT PR.PRODUCT_ID,PR.PRODUCT_TYPE_ID,INTERNAL_NAME
FROM product as PR
join product_type as PTYP on PTYP.PRODUCT_TYPE_ID = PR.PRODUCT_TYPE_ID
where PTYP.IS_PHYSICAL='Y'
AND PR.SALES_DISCONTINUATION_DATE IS NULL;
```
