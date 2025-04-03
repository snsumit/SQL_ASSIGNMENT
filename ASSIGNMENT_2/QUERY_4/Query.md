## Store-Specific (Facility-Wise) Revenue

## Business Problem:
Different physical or online stores (facilities) may have varying levels of performance. The business wants to compare revenue across facilities for sales planning and budgeting.

## Fields to Retrieve:

- `FACILITY_ID`
- `FACILITY_NAME`
- `TOTAL_ORDERS`
- `TOTAL_REVENUE`
- `DATE_RANGE`

## Query Solution
```sql
select 
f.facility_id,
f.facility_name,
count(oh.order_id) as TOTAL_ORDERS,
sum(oh.grand_total) as TOTAL_REVENUE
from facility f 
join order_header oh on oh.ORIGIN_FACILITY_ID = f.FACILITY_ID
where oh.STATUS_ID = "ORDER_COMPLETED"
group by f.FACILITY_ID , f.FACILITY_NAME 
order by TOTAL_REVENUE desc ;
```

## Query Cost (19564.41)