## Canceled Orders (Last Month)

## Business Problem:
The merchandising team needs to know how many orders were canceled in the previous month and their reasons.

## Fields to Retrieve:

- `TOTAL ORDERS`
- `CANCELATION REASON`

## Query Solution
```sql
SELECT 
    COUNT(oh.ORDER_ID) AS TOTAL_ORDERS,
    os.CHANGE_REASON AS CANCELATION_REASON
FROM order_header oh
JOIN order_status os ON oh.ORDER_ID = os.ORDER_ID
WHERE oh.STATUS_ID = 'ORDER_CANCELLED' 
AND oh.ORDER_TYPE_ID = 'SALES_ORDER'
AND os.STATUS_DATETIME >= DATE_FORMAT(NOW() - INTERVAL 1 MONTH, '23-%m-01')
AND os.STATUS_DATETIME < DATE_FORMAT(NOW(), '23-%m-01')
GROUP BY os.CHANGE_REASON;
```
## Query Cost (57016.05)
