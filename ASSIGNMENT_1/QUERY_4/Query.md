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
SELECT 
    p.PRODUCT_ID,
    sp.SHOPIFY_PRODUCT_ID,
    p.PRODUCT_ID AS HOTWAX_ID,
    gi.GOOD_IDENTIFICATION_TYPE_ID as NETSUITE_ID
FROM product p 
JOIN shopify_product sp ON p.PRODUCT_ID = sp.PRODUCT_ID
JOIN good_identification gi 
ON p.PRODUCT_ID = gi.PRODUCT_ID 
WHERE gi.GOOD_IDENTIFICATION_TYPE_ID = "ERP_ID";
```

## Query Cost Analysis (184584.96)
