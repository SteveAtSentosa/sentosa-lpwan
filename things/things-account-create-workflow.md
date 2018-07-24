
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
   Name               URI Secret                    Secret            Scope
   YOUR-CLIENT-NAME   "your-lpwan-server.com/etc"   oWuDsnpI67x...    [profile apps components gateways]
   ```

7. Record the `Name`, and `Secret`, which you will enter into the LPWAN UI when adding the TTN Network to LPWAN