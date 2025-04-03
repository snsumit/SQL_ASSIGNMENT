## Completed Sales Orders (Physical Items)

## Business Problem:
Merchants need to track only physical items (requiring shipping and fulfillment) for logistics and shipping-cost analysis.

## Fields to Retrieve:

- `ORDER_ID`
- `ORDER_ITEM_SEQ_ID`
- `PRODUCT_ID`
- `PRODUCT_TYPE_ID`
- `SALES_CHANNEL_ENUM_ID`
- `ORDER_DATE`
- `ENTRY_DATE`
- `STATUS_ID`
- `STATUS_DATETIME`
- `ORDER_TYPE_ID`
- `PRODUCT_STORE_ID`

## Query Solution
```sql
select 
oi.order_id,
oi.order_item_seq_id,
oi.product_id,
p.product_type_id,
oh.sales_channel_enum_id,
oh.order_date,
oh.entry_date,
oh.status_id,
os.status_datetime,
oh.order_type_id,
oh.product_store_id
from order_header oh 
join order_item oi on oh.ORDER_ID = oi.ORDER_ID
join order_status os on oh.ORDER_ID = os.ORDER_ID 
join product p on oi.PRODUCT_ID = p.PRODUCT_ID
join product_type  pt on p.PRODUCT_TYPE_ID = pt.PRODUCT_TYPE_ID
where oh.STATUS_ID = "ORDER_COMPLETED" and  oh.ORDER_TYPE_ID = "SALES_ORDER"
and pt.IS_PHYSICAL = "Y"
```

## Query Cost (304880.55)
