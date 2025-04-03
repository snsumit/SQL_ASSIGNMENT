## Shipping Addresses for October 2023 Orders

## Business Problem:
Customer Service might need to verify addresses for orders placed or completed in October 2023. This helps ensure shipments are delivered correctly and prevents address-related issues.

## Fields to Retrieve:

- `ORDER_ID`
- `PARTY_ID (Customer ID)`
- `CUSTOMER_NAME (or FIRST_NAME / LAST_NAME)`
- `STREET_ADDRESS`
- `CITY`
- `STATE_PROVINCE`
- `POSTAL_CODE`
- `COUNTRY_CODE`
- `ORDER_STATUS`
- `ORDER_DATE`

## Query Solution
```sql
SELECT distinct
  oh.ORDER_ID,
  orl.PARTY_ID,
  p.FIRST_NAME,
  p.LAST_NAME,
  pa.ADDRESS1 as STREET_ADDRESS,
  pa.CITY,
  pa.STATE_PROVINCE_GEO_ID as STATE_PROVINCE,
  pa.POSTAL_CODE,
  tn.COUNTRY_CODE,
  oh.STATUS_ID as ORDER_STATUS,
  oh.ORDER_DATE
FROM order_header oh 
join order_role orl on oh.ORDER_ID = orl.ORDER_ID 
join person p on orl.PARTY_ID = p.PARTY_ID
join order_contact_mech ocm on  oh.ORDER_ID = ocm.ORDER_ID 
AND ocm.CONTACT_MECH_PURPOSE_TYPE_ID='SHIPPING_LOCATION' 
join order_contact_mech as oc on oh.ORDER_ID = oc.ORDER_ID AND oc.CONTACT_MECH_PURPOSE_TYPE_ID = "PHONE_SHIPPING"
join telecom_number   tn on oc.CONTACT_MECH_ID = tn.CONTACT_MECH_ID 
join postal_address pa on ocm.CONTACT_MECH_ID = pa.CONTACT_MECH_ID
join order_status  os on oh.ORDER_ID = os.ORDER_ID
where oh.order_type_id = 'SALES_ORDER'
AND oh.STATUS_ID IN ('ORDER_COMPLETED','ORDER_CREATED')
AND os.STATUS_DATETIME BETWEEN '2023-10-01 00:00:00' AND '2023-10-31 23:59:59';
```

## Query Cost (238342.33)