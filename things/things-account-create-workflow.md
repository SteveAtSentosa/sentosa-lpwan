
[Full TTN Authenticaiton Documentation Is Here](https://www.thethingsnetwork.org/docs/network/account/authentication.html#1-make-an-authorization-request)

# Proccess for Provisinoing a Things Netowrk in LPWAN

1. Install the TTN command line application `ttnctl`
   - Download from [here](https://www.thethingsnetwork.org/docs/network/cli/quick-start.html) and unzip the contents
   - You may want to rename the provided platform speicfic name, such as `ttnctl-linux-amd64`, to `ttnctl`, and you may want to move this file to a directory that is in your envornment PATH

2. Create a TTN account [here](https://account.thethingsnetwork.org/register)

3. Get a ttnctl access code
   - Login into your TTN account
   - you should be directed to https://account.thethingsnetwork.org/. If not paste this URL in the browser address bar after logging in.
   - select the `ttnctl access code` link and copy the access code that is displayed

4. Login to ttnctl at a terminal commant line
   ```bash
   # to login
   $ ttnctl user login ACCESS-CODE-FROM-STEP-3

   # to see help for this command
   $ ttnctl user login --help

   ```

5. Register a TTN client at the ttnctl command line
   ```bash
   # to register a client
   $ ttnctl clients request YOUR-CLIENT-NAME "Add your client discription" --scope "profile,apps,components,gateways" --grants "authorization_code,refresh_token" --uri "https://your-lpwan-server.com:3000/admin/networks"

   # to see help for this command
   $ ttnctl clients request --help
   ```
6. Regtreive your client via ttnctl
   ```bash
   $ ttnctl client list
   ```
   You will see the following type of information displayed
   ```
   Name               URI Secret                    Secret            ...    Status
   YOUR-CLIENT-NAME   "your-lpwan-server.com/etc"   oWuDsnpI67x...    ...    Pending
   ```

7. Record the `Name`, and `Secret`, which you will enter into the LPWAN UI when adding the TTN Network to LPWAN

8. You will recieve an email when the client has been activated by the TTN orginzation, at which point you will be able to add TTN as an LPWAN Network


https://account.thethingsnetwork.org/users/authorize?client_id=lpwan-ttn-test&&response_type=code&redirect_uri=http://localhost:3000/admin/networks

TESTING 7/28/18 by Jim (thought this was worth capturing somewhere):
After resetting the URI to http://sentosatech.com:3000/admin/networks/oauth, I ran some tests.  In order to redirect to my local lpwanserver, I changed my /etc/hosts file to say sentosatech.com was 127.0.0.1.  Makes for easy testing.

Final working Query:
https://account.thethingsnetwork.org/users/authorize?client_id=lpwan-ttn-test&&response_type=code&redirect_uri=http://sentosatech.com:3000/admin/networks/oauth

Started with some bad queries, some as mistakes, some on purpose:
I mistakenly tried subbing the secret code from the client in for "code".  Response:
http://sentosatech.com:3000/admin/networks/oauth?error=unsupported_response_type&error_description=Unknown%20response_type%20parameter%20passed

I left the localhost URI in the request:
http://localhost:3000/admin/networks/oauth?error=invalid_request&error_description=Wrong%20RedirectUri%20provided


SUCCESS response:
http://sentosatech.com:3000/admin/networks/oauth?code=xPEpietYrvjpjfSy6hr8d9s-9BOr18TPauq1tX6zMA4


If the user chooses to reject the request, rather than accept:
http://sentosatech.com:3000/admin/networks/oauth?error=access_denied&error_description=User%20denied%20the%20access%20to%20the%20resource

This is tricky to make happen, you have to log in to their UI, find the list of enabled 3rd party accessors (under the account pulldown (upper-right), select settings.  On left select Third Party Clients.)  Then deauthorize.

Before I knew that, I got back to the authorization request screen and select reject.  Looks to me that once you've accepted, you always return a code until you deauthorize.
http://sentosatech.com:3000/admin/networks/oauth?code=6_kkBiI7VxrUqdOaRkivXDio0vydJsk5po2hw8jn03Q

When I deauthorized via the UI, and then logged in and rejected, I got this:
http://sentosatech.com:3000/admin/networks/oauth?error=access_denied&error_description=User%20denied%20the%20access%20to%20the%20resource

So, lessons learned:
1) Just because you have a code, doesn't mean it's valid.  User can revoke at any time via TTN (would be the LPWAN owner account doing that, but still could happen).
2) Just because the user selects "reject", doesn't mean we won't get a code back.  This MAY be a bug, we MAY get a bogus code, but given the error message when I went through and deactivated, I don't think that's the code is invalid.  Still, just another datapoint that says, if you have a code, it may not be valid.
