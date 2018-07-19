# Create Company

> As far as I can tell, Things does not have the concept of company

# Create User

> Via the Things portal (did not find API to create user)

* User Name -> `lpwan:users:username`
* Email -> `lpwan:users:email`
* Password -> `lpwan:users:passwordHash`

# Create Application

> Account Server API

```
POST /applications
{
  id: '' -> **?**
  name: String `lpwan:applications:name`
  euis: [String] -> **?**   // list of euis app is reachable at
  rights: [String] -> **?** //  list of rights current user has for the app (which user?)
  collaborators: [{ -> **?**
    username: String
    email: String
    rights: [String] # list of rights collaborator has to the applicaiton
  }]
  access_keys: [{ -> **?**
    name: String
    key: String
    rights: [String] # the rights the key will grant if used
  }]
  created: Date-Time
  deleted: Date-Time # only if app was deleted
}
```

# Create Device Profile

> As far as I can tell, Things does not have the concept of device profile


# Create Device

> Application Manager API

```
POST /applications/{app_id}/devices
  altitude: Num -> **new**  // is this optional?
  latitude: Num -> **new**  // is this optional?
  longitude: Num -> **new** // is this optional?
  app_id: -> **?**          // where does this come from?
  attributes: { key: '', value: '' } // Assuming we don't have to do anything here
  description: String -> `lpwan:devices:description`,
  dev_id: String -> **?**
  lorawan_device: {
    activation_constraints: "e.g. local", -> **?**
    app_eui: String -> `deviceNetworkTypeLinks:networkSettings:{devEUI}`
    app_id: String -> **?** // Where does this come from?
    app_key: String -> **?**
    app_s_key: String -> `deviceNetworkTypeLinks:networkSettings:{appSKey}`,
    nwk_s_key: String -> `deviceNetworkTypeLinks:networkSettings:{nwkSKey}`
    dev_addr: String -> `deviceNetworkTypeLinks:networkSettings:{devAddr}`,
    dev_eui: `deviceNetworkTypeLinks:networkSettings:{devEUI}`,
    dev_id: String -> **?** // Where does this come from?
    disable_f_cnt_check: Bool -> `deviceNetworkTypeLinks:networkSettings:{skipFCntCheck}`
    f_cnt_down: Num -> `deviceNetworkTypeLinks:networkSettings:{fCntUp}`
    f_cnt_up: Num -> `deviceNetworkTypeLinks:networkSettings:{fCntDown}`
    last_seen: Num -> **?**
    uses32_bit_f_cnt: Bool -> **?**
  }
}
```