## Completed Return Items

## Business Problem:
Customer service and finance often need insights into returned items to manage refunds, replacements, and inventory restocking.

## Fields to Retrieve:

- `RETURN_ID`
- `ORDER_ID`
- `PRODUCT_STORE_ID`
- `STATUS_DATETIME`
- `ORDER_NAME`
- `FROM_PARTY_ID`
- `RETURN_DATE`
- `ENTRY_DATE`
- `RETURN_CHANNEL_ENUM_ID`

## Query Solution
```sql
select 
rh.return_id,
oh.order_id,
oh.product_store_id,
rs.status_datetime,
oh.order_name,
rh.from_party_id,
rh.RETURN_DATE,
rh.entry_date,
rh.RETURN_CHANNEL_ENUM_ID 
from return_header rh
join return_item ri on ri.RETURN_ID = rh.RETURN_ID AND ri.STATUS_ID = "RETURN_COMPLETED"
join order_header oh on ri.ORDER_ID = oh.ORDER_ID
join return_status rs on rh.RETURN_ID = rs.RETURN_ID AND rs.STATUS_ID = "RETURN_COMPLETED"
```
## Query Cost (9696.18)