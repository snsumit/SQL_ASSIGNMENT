## Low Stock or Out of Stock Items Report

## Business Problem:
Avoiding out-of-stock situations is critical. This report flags items that have fallen below a certain reorder threshold or have zero available stock.

## Fields to Retrieve:

- `PRODUCT_ID`
- `PRODUCT_NAME`
- `FACILITY_ID`
- `QOH (Quantity on Hand)`
- `ATP (Available to Promise)`
- `REORDER_THRESHOLD`
- `DATE_CHECKED`

## Query Solution
```sql
select 
p.product_id,
p.product_name,
ii.facility_id,
ii.QUANTITY_ON_HAND_TOTAL,
ii.AVAILABLE_TO_PROMISE_TOTAL,
pf.minimum_stock as  reorder_threshold,
current_timestamp() as Date_checked
from inventory_item ii
join product p on ii.PRODUCT_ID = p.PRODUCT_ID
join product_facility pf on p.PRODUCT_ID = pf.PRODUCT_ID and ii.FACILITY_ID = pf.FACILITY_ID
where ii.QUANTITY_ON_HAND_TOTAL <= pf.MINIMUM_STOCK   -- low stock 
or ii.QUANTITY_ON_HAND_TOTAL = 0; -- out of stock

```

## Query Cost (3908683.13)

