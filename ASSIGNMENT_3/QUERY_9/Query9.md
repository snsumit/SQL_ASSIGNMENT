## Total Facilities That Sell the Product

## Business Problem:
Retailers want to see how many (and which) facilities (stores, warehouses, virtual sites) currently offer a product for sale.

## Fields to Retrieve:

- `PRODUCT_ID`
- `PRODUCT_NAME (or INTERNAL_NAME)`
- `FACILITY_COUNT (number of facilities selling the product)`
- `(Optionally) a list of FACILITY_IDs if more detail is needed`

## Query Solution
```sql
select
p.PRODUCT_ID,
p.internal_name as PRODUCT_NAME,
count(pf.FACILITY_ID) as FACILITY_COUNT
from product p
join product_facility pf on p.PRODUCT_ID = pf.PRODUCT_ID 
group by  p.PRODUCT_ID , p.PRODUCT_NAME
```

## Query Cost (1518892.18)


