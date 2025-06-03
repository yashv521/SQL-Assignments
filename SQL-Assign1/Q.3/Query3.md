# Products Missing NetSuite ID

## Business Problem
A product cannot sync to NetSuite unless it has a valid NetSuite ID. The OMS (Order Management System) needs a list of all products that still need to be created or updated in NetSuite.

## Fields to Retrieve
- `PRODUCT_ID` 
- `INTERNAL_NAME` 
- `PRODUCT_TYPE_ID`
- `NETSUITE_ID` 

## Query Solution
```sql
SELECT PR.PRODUCT_ID,INTERNAL_NAME,PR.PRODUCT_TYPE_ID,GI.ID_VALUE AS NETSUITE_ID
FROM product as PR 
JOIN product_type as PTYP on PR.PRODUCT_TYPE_ID = PTYP.PRODUCT_TYPE_ID
LEFT JOIN good_identification as GI on PR.PRODUCT_ID = GI.PRODUCT_ID
WHERE GI.ID_VALUE IS NULL OR GI.ID_VALUE='' and GI.GOOD_IDENTIFICATION_TYPE_ID = 'ERP_ID' ;
```
