## Store with Most One-Day Shipped Orders (Last Month)

## Business Problem:
Identify which facility (store) handled the highest volume of “one-day shipping” orders in the previous month, useful for operational benchmarking.

## Fields to Retrieve:

- `FACILITY_ID`
- `FACILITY_NAME`
- `TOTAL_ONE_DAY_SHIP_ORDERS`
- `REPORTING_PERIOD`

## Query Solution
```sql
select 
f.facility_id,
f.facility_name,
count(osig.order_id) as TOTAL_ONE_DAY_SHIP_ORDERS
from facility f 
join order_item_ship_group  osig on f.FACILITY_ID = osig.FACILITY_ID AND osig.SHIPMENT_METHOD_TYPE_ID = "NEXT_DAY"
join order_header oh on oh.ORDER_ID = osig.ORDER_ID
where oh.ORDER_DATE >= DATE_FORMAT(NOW() - INTERVAL 1 MONTH, '23-%m-01') 
AND oh.ORDER_DATE < DATE_FORMAT(NOW(), '23-%m-01')
group by f.FACILITY_ID , f.FACILITY_NAME 
order by TOTAL_ONE_DAY_SHIP_ORDERS desc
limit 1;

```
## Query Cost (31589.30)
