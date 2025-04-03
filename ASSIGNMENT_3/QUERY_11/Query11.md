## Transfer Orders Without Inventory Reservation

## Business Problem:
When transferring stock between facilities, the system should reserve inventory. If it isn’t reserved, the transfer may fail or oversell.

## Fields to Retrieve:

- `TRANSFER_ORDER_ID`
- `FROM_FACILITY_ID`
- `TO_FACILITY_ID`
- `PRODUCT_ID`
- `REQUESTED_QUANTITY`
- `RESERVED_QUANTITY`
- `TRANSFER_DATE`
- `STATUS`

## Query Solution
```sql
select 
it.inventory_transfer_id as TRANSFER_ORDER_ID,
it.FACILITY_ID as FROM_FACILITY_ID,
it.FACILITY_ID_TO as TO_FACILITY_ID,
it.PRODUCT_ID,
it.QUANTITY as REQUESTED_QUANTITY,
oisgir.QUANTITY as RESERVED_QUANTITY,
it.SEND_DATE as TRANSFER_DATE,
it.status_id as STATUS
from inventory_transfer it 
join order_item_ship_grp_inv_res oisgir on oisgir.INVENTORY_ITEM_ID = it.INVENTORY_ITEM_ID;

```

## Query Cost (14.62)
