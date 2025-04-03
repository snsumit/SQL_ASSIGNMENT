## Orders from New York

## Business Problem:
Companies often want region-specific analysis to plan local marketing, staffing, or promotions in certain areas—here, specifically, New York.

## Fields to Retrieve:

-`ORDER_ID`
-`CUSTOMER_NAME`
-`STREET_ADDRESS (or shipping address detail)`
-`CITY`
-`STATE_PROVINCE`
-`POSTAL_CODE`
-`TOTAL_AMOUNT`
-`ORDER_DATE`
-`ORDER_STATUS`

## Query Solution 
```sql
SELECT distinct
 oh.ORDER_ID,
 p.FIRST_NAME,
 p.LAST_NAME,
 pa.ADDRESS1 as STREET_ADDRESS,
 pa.CITY,
 pa.STATE_PROVINCE_GEO_ID as STATE_PROVINCE,
 pa.POSTAL_CODE,
 oh.GRAND_TOTAL as TOTAL_AMOUNT,
 oh.ORDER_DATE,
 oh.STATUS_ID as ORDER_STATUS
FROM order_header oh 
join order_role  orl on orl.ORDER_ID = oh.ORDER_ID
join person p on orl.PARTY_ID = p.PARTY_ID
join order_contact_mech ocm on ocm.ORDER_ID = oh.ORDER_ID
join contact_mech cm on ocm.CONTACT_MECH_ID = cm.CONTACT_MECH_ID
join postal_address pa on pa.CONTACT_MECH_ID = cm.CONTACT_MECH_ID
where pa.STATE_PROVINCE_GEO_ID = "NY";
```
## Query Cost (280388.77)

