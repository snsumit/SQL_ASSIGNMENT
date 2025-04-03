## Items Where QOH and ATP Differ

## Business Problem:
Sometimes the Quantity on Hand (QOH) doesn’t match the Available to Promise (ATP) due to pending orders, reservations, or data discrepancies. This needs review for accurate fulfillment planning.

## Fields to Retrieve:

- `PRODUCT_ID`
- `FACILITY_ID`
- `QOH (Quantity on Hand)`
- `ATP (Available to Promise)`
- `DIFFERENCE (QOH - ATP)`

## Query Solution
```sql
select 
ii.product_id,
ii.facility_id,
ii.QUANTITY_ON_HAND_TOTAL as QOH,
ii.AVAILABLE_TO_PROMISE_TOTAL as ATP,
(ii.quantity_on_hand_total - ii.available_to_promise_total) as DIFFERENCE 
from  inventory_item ii 
where ii.QUANTITY_ON_HAND_TOTAL <> ii.AVAILABLE_TO_PROMISE_TOTAL;
```

## Query Cost (215710.69)