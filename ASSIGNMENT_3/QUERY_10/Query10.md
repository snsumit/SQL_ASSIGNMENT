## Total Items in Various Virtual Facilities

## Business Problem:
Retailers need to study the relation of inventory levels of products to the type of facility it's stored at. Retrieve all inventory levels for products at locations and include the facility type Id. Do not retrieve facilities that are of type Virtual.

## Fields to Retrieve:

- `PRODUCT_ID`
- `FACILITY_ID`
- `FACILITY_TYPE_ID`
- `QOH (Quantity on Hand)`
- `ATP (Available to Promise)`

## Query Solution 
```sql
select 
ii.product_id,
ii.facility_id,
f.facility_type_id,
ii.QUANTITY_ON_HAND_TOTAL AS QOH,
ii.AVAILABLE_TO_PROMISE_TOTAL as ATP
from inventory_item ii
join facility f on f.FACILITY_ID = ii.FACILITY_ID  AND f.FACILITY_TYPE_ID != 'VIRTUAL_FACILITY'
```
## Query Cost (2002983.00)

