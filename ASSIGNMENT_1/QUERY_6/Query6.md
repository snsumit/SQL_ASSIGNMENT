# Newly Created Sales Orders and Payment Methods

## Business Problem
Finance teams need to see new orders and their payment methods for reconciliation and fraud checks. This helps ensure accurate financial reporting and detect any fraudulent transactions.


## Fields to Retrieve
- `ORDER_ID` 
- `TOTAL_AMOUNT` 
- `PAYMENT_METHOD` 
- `SHOPIFY_ORDER_ID` 

## Query Solution
```sql
SELECT 
    oh.ORDER_ID,
    oh.GRAND_TOTAL AS TOTAL_AMOUNT,
    opp.PAYMENT_METHOD_TYPE_ID AS PAYMENT_METHOD,
    oh.EXTERNAL_ID AS SHOPIFY_ORDER_ID
FROM order_header oh 
JOIN order_payment_preference opp
ON oh.ORDER_ID = opp.ORDER_ID 
WHERE oh.ORDER_DATE BETWEEN '2023-08-01 00:00:00' AND '2023-08-31 23:59:59';
```

## Query Cost (16974.70)