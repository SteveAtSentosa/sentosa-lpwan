# LPWAN Owner Adds Things Network to LPWAN Instance

1. LPWAN Owner creates LPWAN Things Account, providing a UserName/PW/eMail

2. LPWAN Owner dowloads the TTN command line tool `ttnctl`, generates a `ttnctl` login token via the TTN Web Portal, and logs into `ttnctl` on the command line.

3. LPWAN Owner registers a TTN client using the ttnctl command line application.  This proccess generates a clientId, and a clientSecret.

4. LPWAN Owner logs into the LPWAN portal, and navigates to Networks/'Create Network'

5. LPWAN Owner enters/selects: Name:`TTN NW` / Network Type: `LoRa` / Netowrk Protocol `TTN`

6. When `TTN` is selected as the Network Protocal, additional TTN specific UI input fields and an action button appears:
   ````
   Client ID     _______________
   Client Secret _______________
   [Authorize]
   ````

7. LPWan Owner enters the Client ID and Client Secret generated from Step 3, then hits the [Authorize] button

8. This directs the browser to the TTN Login Page, at which point LPWAN Owner provides the UserName/PW from step 1, and hits the [Login] button.

9. After succefully providing UserName / Password to the TTN login portal, the browser is redirected back to the LPWAN Portal Networks page and hits [SUBMIT].  At this point, the TTN account and network has been added to LPWAN.


# LPWAN User Adds an Application
# LPWAN User Adds a Device Profile
# LPWAN User Adds a Device

NOTE: there may be TTN specific input fields that need to be displayed in the UI during these operations.  This is TBD.
