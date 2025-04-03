## Lost and Damaged Inventory

## Business Problem:
Warehouse managers need to track “shrinkage” such as lost or damaged inventory to reconcile physical vs. system counts.

## Fields to Retrieve:

- `INVENTORY_ITEM_ID`
- `PRODUCT_ID`
- `FACILITY_ID`
- `QUANTITY_LOST_OR_DAMAGED`
- `REASON_CODE (Lost, Damaged, Expired, etc.)`
- `TRANSACTION_DATE`

## Query Solution
```sql
select
ii.inventory_item_id,
ii.product_id,
ii.facility_id,
iiv.QUANTITY_ON_HAND_VAR as quantity_lost_or_damaged,
iiv.variance_reason_id as reason_code,
iiv.created_stamp as TRANSACTION_DATE
from inventory_item ii
join inventory_item_variance iiv on ii.INVENTORY_ITEM_ID = iiv.INVENTORY_ITEM_ID AND iiv.VARIANCE_REASON_ID in ("VAR_LOST","VAR_DAMAGED")
```

## Query Cost (583794.51)


