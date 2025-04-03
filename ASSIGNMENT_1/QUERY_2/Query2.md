# List of All Active Physical Products

## Business Problem
The merchandising team often needs a list of all active physical products to manage logistics, warehousing, and shipping efficiently.

## Query Objective
Retrieve details of all active physical products.

## Fields to Retrieve
- `PRODUCT_ID` - Unique identifier for the product
- `PRODUCT_TYPE_ID` - Type of product
- `INTERNAL_NAME` - Internal name of the product

## Query Solution
```sql
SELECT 
    p.PRODUCT_ID,
    p.PRODUCT_TYPE_ID,
    p.INTERNAL_NAME
FROM product AS p 
JOIN product_type pt 
ON p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
WHERE pt.IS_PHYSICAL = 'Y'  
AND (p.SALES_DISCONTINUATION_DATE IS NULL 
AND p.SUPPORT_DISCONTINUATION_DATE IS NULL);
```

## Query Cost (81484.22)
