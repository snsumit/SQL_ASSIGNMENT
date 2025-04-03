# Payment Captured but Not Shipped

## Business Problem
Finance teams want to ensure revenue is recognized properly. If payment is captured but no shipment has occurred, it warrants further review to prevent financial discrepancies and customer dissatisfaction.


## Fields to Retrieve
- `ORDER_ID` 
- `ORDER_STATUS` 
- `PAYMENT_STATUS` 
- `SHIPMENT_STATUS` 

## Query Solution
```sql
SELECT
    oh.ORDER_ID,
    oh.STATUS_ID AS ORDER_STATUS,
    opp.STATUS_ID AS PAYMENT_STATUS,
    sh.STATUS_ID AS SHIPMENT_STATUS
FROM order_header oh
JOIN order_payment_preference opp ON oh.ORDER_ID = opp.ORDER_ID 
JOIN order_shipment os ON oh.ORDER_ID = os.ORDER_ID 
JOIN shipment sh ON os.SHIPMENT_ID = sh.SHIPMENT_ID 
WHERE opp.STATUS_ID = "PAYMENT_SETTLED"  
AND sh.STATUS_ID != "SHIPMENT_SHIPPED";
```

## Query Cost (44391.48)