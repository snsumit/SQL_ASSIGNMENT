# Orders Completed Hourly

## Business Problem
Operations teams may want to see how orders complete across the day to schedule staffing effectively and optimize workflows.


## Fields to Retrieve
- `HOURS` 
- `TOTAL_ORDER` 

## Query Solution
```sql
SELECT
    HOUR(os.STATUS_DATETIME) AS HOURS,
    COUNT(oh.ORDER_ID) AS TOTAL_ORDER
FROM order_header oh 
JOIN order_status os 
ON oh.ORDER_ID = os.ORDER_ID 
WHERE os.STATUS_ID = "ORDER_COMPLETED"
GROUP BY HOURS;
```

## Query Cost (40426.17)
