Bad APIKEY
- the base 64 is given a number but no representing a valid user id
- the base 64 is given a string.



curl -k -X GET https://localhost:8443/api/public/stats/markPosed/1\
   -H "Authorization: BMTBT-MTA=.6bf567b9-e1ed-42c0-9424-1bad4e887672"
