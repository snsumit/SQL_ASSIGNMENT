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
SELECT 
    p.PRODUCT_ID,
    p.INTERNAL_NAME,
    p.PRODUCT_TYPE_ID,
    gi.GOOD_IDENTIFICATION_TYPE_ID as NETSUITE_ID
FROM product p
LEFT JOIN good_identification gi
ON p.PRODUCT_ID = gi.PRODUCT_ID  
WHERE gi.GOOD_IDENTIFICATION_TYPE_ID = 'ERP_ID' 
AND (gi.ID_VALUE IS NULL OR gi.ID_VALUE = "");
```

## Query Cost (3.33)
