## Orders Without Picklist
## Business Problem:
A picklist is necessary for warehouse staff to gather items. Orders missing a picklist might be delayed and need attention.

## Fields to Retrieve:

- `ORDER_ID`
- `ORDER_DATE`
- `ORDER_STATUS`
- `FACILITY_ID`
- `DURATION (How long has the order been assigned at the facility)`

## Query Solution
```sql

select distinct
oh.order_id,
oh.order_date,
oh.status_id,
oisg.facility_id,
datediff(date(os.status_datetime), date(oh.entry_date)) as duration
from order_header oh
join order_item_ship_group oisg on oisg.ORDER_ID = oh.ORDER_ID
join order_status  os on os.ORDER_ID = oh.ORDER_ID
join picklist pl on pl.FACILITY_ID = oisg.FACILITY_ID
where pl.STATUS_ID is null

```

## Query Cost (8108.22)
