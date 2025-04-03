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
    p.PRODUCT_ID,
    p.PRODUCT_TYPE_ID,
    oh.PRODUCT_STORE_ID,
    SUM(oi.QUANTITY) AS TOTAL_QUANTITY,
    p.INTERNAL_NAME,
    p.FACILITY_ID,
    oh.EXTERNAL_ID,
    fa.FACILITY_TYPE_ID,
    ohi.ORDER_HISTORY_ID,
    oh.ORDER_ID,
    oi.ORDER_ITEM_SEQ_ID,
    ohi.SHIP_GROUP_SEQ_ID
FROM order_header oh
JOIN order_item oi 
ON oh.ORDER_ID = oi.ORDER_ID
JOIN product p ON p.PRODUCT_ID = oi.PRODUCT_ID 
JOIN facility fa ON p.FACILITY_ID = fa.FACILITY_ID
JOIN order_history ohi ON oh.ORDER_ID = ohi.ORDER_ID
WHERE oh.STATUS_ID = 'ORDER_COMPLETED' 
AND oh.ORDER_DATE BETWEEN '2023-08-01 00:00:00' AND '2023-08-31 23:59:59'
GROUP BY 
    p.PRODUCT_ID,
    p.PRODUCT_TYPE_ID,
    oh.PRODUCT_STORE_ID,
    p.INTERNAL_NAME,
    p.FACILITY_ID,
    oh.EXTERNAL_ID,
    fa.FACILITY_TYPE_ID,
    ohi.ORDER_HISTORY_ID,
    oh.ORDER_ID,
    oi.ORDER_ITEM_SEQ_ID,
    ohi.SHIP_GROUP_SEQ_ID;
```

## Query Cost Analysis (184840.88)
