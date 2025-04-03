## Orders with Multiple Returns
## Business Problem:
Analyzing orders with multiple returns can identify potential fraud, chronic issues with certain items, or inconsistent shipping processes.

## Fields to Retrieve:

- `ORDER_ID`
- `RETURN_ID`
- `RETURN_DATE`
- `RETURN_REASON`
- `RETURN_QUANTITY`

## Query Solution 
```sql
select 
ri.ORDER_ID,
ri.RETURN_ID,
rh.RETURN_DATE,
rr.DESCRIPTION as RETURN_REASON,
ri.RETURN_QUANTITY
from return_header rh 
join return_item ri on rh.RETURN_ID = ri.RETURN_ID
join return_reason rr on ri.RETURN_REASON_ID = rr.RETURN_REASON_ID
where ri.ORDER_ID  IN (
    select ORDER_ID  from return_item group by ORDER_ID having count(RETURN_ID) > 1
);
```

## Query Cost (3404.25)
