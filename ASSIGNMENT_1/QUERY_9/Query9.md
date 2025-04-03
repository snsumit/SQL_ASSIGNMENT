## BOPIS Orders Revenue (Last Year)

## Business Problem:
BOPIS (Buy Online, Pickup In Store) is a key retail strategy. Finance wants to know the revenue from BOPIS orders for the previous year.

## Fields to Retrieve:

- `TOTAL ORDERS`
- `TOTAL REVENUE`

## Query Solution
```sql
select  
     count(oh.ORDER_ID) as TOTAL_ORDERS,
     sum(oh.GRAND_TOTAL) as TOTAL_REVENUE
from order_header oh
join order_item_ship_group oisp
on oh.ORDER_ID = oisp.ORDER_ID
where oh.SALES_CHANNEL_ENUM_ID = "WEB_SALES_CHANNEL" 
AND oh.STATUS_ID="ORDER_COMPLETED" 
AND oisp.SHIPMENT_METHOD_TYPE_ID = "STOREPICKUP"
and oh.ORDER_TYPE_ID = "SALES_ORDER" 
AND YEAR(oh.ORDER_DATE) = YEAR(CURDATE()) - 2;   
```

## Query Cost (41207.93)