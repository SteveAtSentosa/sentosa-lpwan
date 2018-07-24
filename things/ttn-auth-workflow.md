```
1. lpwan-owner creates things account w specific un/pw/email

2. using things ttnctl command line app
  - request a client-id (we choose this) (ttn client request: client name, callback URI, scope, grant type)
    secret comes back

3. lpwan-owner navigates Create Network on the LPWAN portal, and selects Things NW Protocol

4. lpwan-portal -> lpwan-server
GET lpwan-server/protocols/ttn/fields (or whatever)
rsp ->
{
  "TTN Client Name" : "String",
  "TTN Client Secret" : "String,
}

5. LPWAN UI dislpays Things specific UI based
  - fields from 4
  - Portal "Sign Into Your Things Account"

6. User fills in the fields in 4, then hits the  "Sign Into Your Things Account" button

7. browser goes to ttn-server/users/authorize?clientId=ttnClientId&redirect=http://lpwan-url.com:3000/admin/networks&response-type=code
   user logs into TTN using un/pw from 1.

8. TTN redirects back to LPWAN portal via redirect URL -> https://lpwan-url.com:3000/admin/networks?code=ABCD,


9. lpwan-portal pulls code from redirected URL

10. lpwan-portal -> ttn-server
   POST ttn-server/users/token
   body
   {
    code: ABCD (pulled from redirected URL)
    header: Base64(ttnClientId:clietnSecret)
   }
   rsp
   {
    "refresh_token": "2ClRfsOlgOFFIJIB5JX8lD-UlzWHk-yHYEWzs7xD1QY",
    "access_token": "eyJ0eXAiOiJKV1Qi...",
   }

11. lpwan-portal -> lpwan-server
   PUT lpwan-server/ttn/tokens (or whatever)
   body
   {
    "refresh_token": "2ClRfsOlgOFFIJIB5JX8lD-UlzWHk-yHYEWzs7xD1QY",
    "access_token": "eyJ0eXAiOiJKV1Qi...",
   }

12. User hits "Done" in the Create Network
POST /jim/you/add/here
{
  clientId
  clientSecret
  etc.
}
```




----------------------------------------------------------------------------------
 Rough Notes Below
----------------------------------------------------------------------------------

Things:

Things Command Line Tool

Request client ID
  provide: callBackid
  scope: [profile apps components gateways]
  grants: auth code refresh token


GET code


                                  (OAuth callback)


then base 64 encode:

API:

  Loginto

  Post: .../token
  {
    code ...
    grant_type...

  }

  Create NW:

  Button: Auth TTN Account
    you will go to TTN portal
    login, and the callback will be called
      We are verying our user to make sure it is one thier users


Oauth2 Redirect Login
  RSP: Get code back through redirected URL
POST /users/token:
  input: code from above (iomprtant for 5 mintes)
  header: basic BASE64(client ID, and ???)


{
    "token_type": "bearer",
    "refresh_token": "2ClRfsOlgOFFIJIB5JX8lD-UlzWHk-yHYEWzs7xD1QY",
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJzdWIiOiI1YjJhN2IyMTZhNDFhZTAwMzBhOTExZWQiLCJpc3MiOiJ0dG4tYWNjb3VudC12MiIsImlhdCI6MTUzMjM3MTk5MiwidHlwZSI6InVzZXIiLCJjbGllbnQiOiJscHdhbi10ZXN0Iiwic2NvcGUiOlsicHJvZmlsZSIsImFwcHMiLCJjb21wb25lbnRzIiwiZ2F0ZXdheXMiXSwiaW50ZXJjaGFuZ2VhYmxlIjp0cnVlLCJ1c2VybmFtZSI6ImRzY2hyaW1wc2hlcnIiLCJlbWFpbCI6ImQuc2NocmltcHNoZXJAY2FibGVsYWJzLmNvbSIsImNyZWF0ZWQiOiIyMDE4LTA2LTIwVDE2OjA0OjQ5Ljc2N1oiLCJuYW1lIjp7ImZpcnN0IjoiRGFuIiwibGFzdCI6IlNjaHJpbXBzaGVyIn0sInZhbGlkIjp0cnVlLCJfaWQiOiI1YjJhN2IyMTZhNDFhZTAwMzBhOTExZWQiLCJleHAiOjE1MzIzNzU2NTJ9.ESKcszCy-CiVuADBOo2L_Fy4qIS8ahs0yPaCmGWpTRV61Uq7AftadPyevReTTEGvLXqNwE7Sz12XwPmY9sHsE5FF_g4MKvRETqwLfWM8wfjt5Ij8JVaFtKxpotobOqBsETEySk0EHiT4SZip0HW-SHQuLnNpZHF1ffdLYN3Zu-_-Qj_GLm4ceAqwJ3F5NVT-LBxsN3-Bl7MMjj6h-n7Ay5Ko9IKdGnbrWkbDlFp29WaEUngf4fWh5eSjrhWUKzYnyQ9Di055eGOKSCZEHT3ido1uskSibPGyn5bnR_n3oQxNZhMPiK__ckDCgPTQyi-ZFj2FWs-KEyHqZTj02pp3MQRkaB3TBC7jkmAB5lWbhKXsXB1-Kffmbq12UY1aHNzSl7RkrklmwQISPcYfjqCF9MHU5En31Y9rOx4BhMldWPoYZMp3ukzNrDmffgqVKa29zkJ_FKEUbRzRh-vOjkeNuWkkCnd7rZIvwkNsT1_2lOwALwhc7KD54QAKCzGA-LHJl1Isf6J7qQPCmLNfTaSaZ0-P0ah5GPSuWhbPaYMeMd7zLzXInPVo28I642Q48ghsU5I0ZnyyKmzEUwq5vt1eAdgg-fNsKzAnqT53CSkZCrGuM0WzaCMqKeramxWYyNeFnezwDSkaYHRE-bPmsQjd2IHeOgUVg2-7QmephcZ1lwA",
    "expires_in": 3600
}

access_token: used for actual API calls
when access token expires,

------------------

Each app / device will have it's own keys
  On TTN: App by App Basis

Once you have app token, you can do whatever

Every App Has own Key
- Creation: bearer token: admin account


I will need: ClientID, redirect URL, response-type

Code will in URL : I can pull that off
  stuff it in a post /users/token
  to get bearer token and refresh token

  Dan will provide util to store that info




lpwan-portal -> lpwan-server
GET .../clientInfo

Flow:

Get ClientInfo (speific to LPWAN account to TTN)
{

}

GET /users/authorize?clientId=id, redirect=http:abc.def.com

Will comback to redirect

with code = in URL


POST

take base64 encoded client secret


=======================

Make sure that I understand diff between bearer token and key


1. lpwan-portal -> lpwan-server
   GET lpwan-server/ttn/clientInfo (or whatever)
   rsp -> { ttnClientId }

2. lpwan-portal Create Network Page: user hits button "Sign Into TTN"
   browser goes to ttn-server/users/authorize?clientId=ttnClientId&redirect=http://lpwan-url.com:3000/admin/networks
   user logs into TTN
   TTN redirects back to LPWAN portal via redirect URL -> https://lpwan-url.com:3000/admin/networks?code=ABCD,

3. lpwan-portal pulls code from redirected URL

4. lpwan-portal -> ttn-server
   POST ttn-server/users/token
   body
   {
    input: ABCD (pulled from redirected URL)
    header: Base64(ttnClientId + ?I Forgot? )
   }
   rsp
   {
    "refresh_token": "2ClRfsOlgOFFIJIB5JX8lD-UlzWHk-yHYEWzs7xD1QY",
    "access_token": "eyJ0eXAiOiJKV1Qi...",
   }

5. lpwan-portal -> lpwan-server
   PUT lpwan-server/ttn/tokens (or whatever)
   body
   {
    "refresh_token": "2ClRfsOlgOFFIJIB5JX8lD-UlzWHk-yHYEWzs7xD1QY",
    "access_token": "eyJ0eXAiOiJKV1Qi...",
   }
