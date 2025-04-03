## Retrieve the Current Facility (Physical or Virtual) of Open Orders

## Business Problem:
The business wants to know where open orders are currently assigned, whether in a physical store or a virtual facility (e.g., a distribution center or online fulfillment location).

## Fields to Retrieve:

- `ORDER_ID`
- `ORDER_STATUS`
- `FACILITY_ID`
- `FACILITY_NAME`
- `FACILITY_TYPE_ID`

## Query Solution
```sql
SELECT 
oh.ORDER_ID,
oh.STATUS_ID as ORDER_STATUS,
f.FACILITY_ID,
f.FACILITY_NAME,
f.FACILITY_TYPE_ID
FROM order_header oh 
join order_item_ship_group oisg on oh.ORDER_ID = oisg.ORDER_ID
join facility f on oisg.FACILITY_ID = f.FACILITY_ID
where oh.STATUS_ID in ('ORDER_CREATED' , 'ORDER_APPROVED');
```
## Query Cost (131155.08)

