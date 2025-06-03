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
Select P.PARTY_ID,P.FIRST_NAME,P.LAST_NAME,CM.INFO_STRING,TN.CONTACT_NUMBER,P1.CREATED_DATE AS ENTRY_DATE
FROM party AS P1
JOIN party_role AS PR ON P1.PARTY_ID = PR.PARTY_ID AND PR.ROLE_TYPE_ID='Customer'
JOIN person AS P ON P1.PARTY_ID = P.PARTY_ID
LEFT JOIN party_contact_mech as PCM ON PCM.PARTY_ID = P1.PARTY_ID
JOIN contact_mech AS CM ON CM.CONTACT_MECH_ID = PCM.CONTACT_MECH_ID
LEFT JOIN telecom_number AS TN ON TN.CONTACT_MECH_ID = CM.CONTACT_MECH_ID
WHERE P1.CREATED_DATE between '2023-06-01' AND '2023-06-30';
```
