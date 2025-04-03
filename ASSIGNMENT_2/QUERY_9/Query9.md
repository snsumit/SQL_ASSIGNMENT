## Order Item Current Status Changed Date-Time

## Business Problem:
Operations teams need to audit when an order item’s status (e.g., from “Pending” to “Shipped”) was last changed, for shipment tracking or dispute resolution.

## Fields to Retrieve:

- `ORDER_ID`
- `ORDER_ITEM_SEQ_ID`
- `CURRENT_STATUS_ID`
- `STATUS_CHANGE_DATETIME`
- `CHANGED_BY`

## Query Solution
```sql
select
os.ORDER_ID,
os.ORDER_ITEM_SEQ_ID,
os.status_id as CURRENT_STATUS_ID,
os.STATUS_DATETIME as STATUS_CHANGE_DATETIME,
os.STATUS_USER_LOGIN as CHANGE_BY
from order_status os
where os.ORDER_ITEM_SEQ_ID is not null;

```

## Query Cost (69174.81)