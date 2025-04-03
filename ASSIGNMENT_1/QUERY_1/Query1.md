# New Customers Acquired in June 2023

## Business Problem
The marketing team ran a campaign in June 2023 and wants to analyze how many new customers signed up during that period. This data will help assess the effectiveness of the campaign and guide future marketing strategies.

## Fields to Retrieve
- `PARTY_ID` 
- `FIRST_NAME` 
- `LAST_NAME` 
- `EMAIL` 
- `PHONE` 
- `CREATED_STAMP` - 

## Query Solution
```sql
SELECT
    pe.PARTY_ID, 
    pe.FIRST_NAME, 
    pe.LAST_NAME, 
    cn.INFO_STRING as EMAIL,
    tn.CONTACT_NUMBER as PHONE,
    pe.CREATED_STAMP
FROM person pe
JOIN party_role pr ON pe.PARTY_ID = pr.PARTY_ID AND ROLE_TYPE_ID = 'CUSTOMER' 
JOIN party_contact_mech pcm ON pe.PARTY_ID = pcm.PARTY_ID
LEFT JOIN contact_mech cn ON pcm.CONTACT_MECH_ID = cn.CONTACT_MECH_ID AND cn.CONTACT_MECH_TYPE_ID IN ('EMAIL_ADDRESS','TELECOM_NUMBER')
LEFT JOIN telecom_number tn ON tn.CONTACT_MECH_ID = cn.CONTACT_MECH_ID
WHERE pe.CREATED_STAMP BETWEEN '2023-06-01 00:00:00' AND '2023-06-30 23:59:59';
```

## Query Cost (15941.00)

