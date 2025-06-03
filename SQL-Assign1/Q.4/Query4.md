## Product IDs Across Systems

## Business Problem:
To sync an order or product across multiple systems (e.g., Shopify, HotWax, ERP/NetSuite), the OMS needs to know each system’s unique identifier for that product. This query retrieves the Shopify ID, HotWax ID, and ERP ID (NetSuite ID) for all products.

## Fields to Retrieve
- `PRODUCT_ID` 
- `SHOPIFY_ID` 
- `HOTWAX_ID` 
- `ERP_ID` or `NETSUITE_ID` 

## Query Solution
```sql
SELECT PR.PRODUCT_ID,SHP.SHOPIFY_PRODUCT_ID,PR.PRODUCT_ID AS HOTWAX_ID, GI.ID_VALUE AS NETSUITE_ID
FROM product PR 
JOIN  shopify_product as SHP ON SHP.PRODUCT_ID = PR.PRODUCT_ID
JOIN good_identification GI ON PR.PRODUCT_ID = GI.PRODUCT_ID
WHERE GOOD_IDENTIFICATION_TYPE_ID = 'ERP_ID';
```
