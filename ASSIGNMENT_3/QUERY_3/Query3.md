## Single-Return Orders (Last Month)

## Business Problem:
The mechandising team needs a list of orders that only have one return.

## Fields to Retrieve:

- `PARTY_ID`
- `FIRST_NAME`

## Query Solution 
```sql
select 
rh.from_party_id as PARTY_ID,
p.FIRST_NAME 
from return_header rh 
join  person p on p.PARTY_ID = rh.FROM_PARTY_ID 
where rh.RETURN_DATE >=  DATE_FORMAT(NOW() - INTERVAL 1 MONTH, '%23-%m-01')
AND rh.RETURN_DATE < DATE_FORMAT(NOW(), '%23-%m-01')
group by rh.FROM_PARTY_ID , p.FIRST_NAME
having count(rh.RETURN_ID) = 1

```
## Query Cost (1150.8)