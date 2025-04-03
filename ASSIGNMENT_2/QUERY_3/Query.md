## Top-Selling Product in New York

## Business Problem:
Merchandising teams need to identify the best-selling product(s) in a specific region (New York) for targeted restocking or promotions.

## Fields to Retrieve:

- `PRODUCT_ID`
- `INTERNAL_NAME`
- `TOTAL_QUANTITY_SOLD`
- `CITY / STATE (within New York region)`
- `REVENUE (optionally, total sales amount)`

## Query Solution
```sql
select 
p.product_id,
p.internal_name,
sum(oi.quantity) as TOTAL_QUANTITY_SOLD,
pa.CITY,
sum(oi.quantity  * oi.unit_price) as REVENUE
from product p 
join order_item oi on p.PRODUCT_ID = oi.PRODUCT_ID
join order_header oh on oh.ORDER_ID = oi.ORDER_ID 
join order_contact_mech ocm on oi.ORDER_ID = ocm.ORDER_ID
join postal_address pa on ocm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
where pa.STATE_PROVINCE_GEO_ID = "NY" and oh.ORDER_TYPE_ID = "SALES_ORDER"
group by p.PRODUCT_ID, p.INTERNAL_NAME, pa.CITY
order by TOTAL_QUANTITY_SOLD desc
limit 1

```

## Query Cost (90075.16)