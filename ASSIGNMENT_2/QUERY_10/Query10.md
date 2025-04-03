## Total Orders by Sales Channel

## Business Problem:
Marketing and sales teams want to see how many orders come from each channel (e.g., web, mobile app, in-store POS, marketplace) to allocate resources effectively.

## Fields to Retrieve:

- `SALES_CHANNEL`
- `TOTAL_ORDERS`
- `TOTAL_REVENUE`
- `REPORTING_PERIOD`

## Query Solution
```sql
select
oh.sales_channel_enum_id as SALES_CHANNEL,
count(oh.order_id) as TOTAL_ORDERS,
sum(oh.grand_total) as TOTAL_REVENUE,
DATE_FORMAT(oh.ORDER_DATE, '%Y-%m') AS REPORTING_PERIOD 
from order_header oh 
group by SALES_CHANNEL , REPORTING_PERIOD

```

## Query Cost (8450.55)