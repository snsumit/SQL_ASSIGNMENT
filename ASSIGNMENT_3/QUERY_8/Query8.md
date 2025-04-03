## List of Warehouse Pickers

## Business Problem:
Warehouse managers need a list of employees responsible for picking and packing orders to manage shifts, productivity, and training needs.

## Fields to Retrieve:

- `PARTY_ID (or Employee ID)`
- `NAME (First/Last)`
- `ROLE_TYPE_ID (e.g., “WAREHOUSE_PICKER”)`
- `FACILITY_ID (assigned warehouse)`
- `STATUS (active or inactive employee)`

## Query Solution
```sql
select
plr.PARTY_ID,
concat(p.FIRST_NAME,' ',p.LAST_NAME) as NAME,
plr.ROLE_TYPE_ID,
pl.FACILITY_ID,
pa.status_id as STATUS
from picklist  pl
join picklist_role plr on pl.PICKLIST_ID = plr.PICKLIST_ID
join party pa on plr.PARTY_ID = pa.PARTY_ID
join person p on p.PARTY_ID = pa.PARTY_ID

```
## Query Cost (7390.96)
