## Detailed Return Information
## Business Problem:
Certain teams need granular return data (reason, date, refund amount) for analyzing return rates, identifying recurring issues, or updating policies.

## Fields to Retrieve:

- `RETURN_ID`
- `ENTRY_DATE`
- `RETURN_ADJUSTMENT_TYPE_ID (refund type, store credit, etc.)`
- `AMOUNT`
- `COMMENTS`
- `ORDER_ID`
- `ORDER_DATE`
- `RETURN_DATE`
- `PRODUCT_STORE_ID`

## Query Solution
```sql
select distinct
rh.return_id,
rh.entry_date,
ra.return_adjustment_type_id,
ra.amount,
ra.comments,
ri.order_id,
oh.order_date,
rh.return_date,
oh.product_store_id
from return_header rh 
join return_item  ri on ri.RETURN_ID = rh.RETURN_ID
join return_adjustment ra on rh.RETURN_ID = ra.RETURN_ID
join order_header oh on ri.ORDER_ID = oh.ORDER_ID

```

## Query Cost (6296.60)
