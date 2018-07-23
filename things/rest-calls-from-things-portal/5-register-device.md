# Sent from TTN Portal

https://console.thethingsnetwork.org/applications/stc-app-1/devices

```
POST https://console.thethingsnetwork.org/api/applications/stc-app-1/devices
headers
  authority: console.thethingsnetwork.org
  method: POST
  path: /api/applications/stc-app-1/devices
  authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSU...
  origin: https://console.thethingsnetwork.org
  referer: https://console.thethingsnetwork.org/applications/stc-app-1/devices/stc-dev-1
```
> note: App key is created by the portal

body:
```json
{
  "dev_id": "stc-dev-1",          "maps to" : ?, "note" : "not sure if this had to be globally unique to TTN",
  "app_eui": "70B3D57ED0010C49",  "maps to" : ?, "note" : "see applicaiton create notes",
  "dev_eui": "1234567890098765",  "maps to" : "deviceNetworkTypeLinks:networkSettings:{devEUI}",
}
```

rsp:
```json
{
  "app_id": "stc-app-1",
  "dev_id": "stc-dev-1", "maps to" : "?", "note" : "not sure if this had to be globally unique to TTN",
  "description": "",
  "last_seen": "0001-01-01T00:00:00Z",
  "app_eui": "70B3D57ED0010C49",
  "dev_eui": "1234567890098765",
  "app_key": "FDEA735778F18A4BAD885D5557B621C4",
  "fcnt_up": 0,
  "fcnt_down": 0,
  "disable_fcnt_check": false,
  "uses_32bit_fcnt": true,
  "location": null
}
```

# Documentation

[Part of the Application Manager API](https://www.thethingsnetwork.org/docs/applications/manager/api.html/)

`POST /applications/{app_id}/devices`
```
  "altitude": 0,
  "app_id": "some-app-id",
  "attributes": {
    "key": "",
    "value": ""
  },
  "description": "Some description of the device",
  "dev_id": "some-dev-id",
  "latitude": 52.375,
  "longitude": 4.887,
  "lorawan_device": {
    "activation_constraints": "local", -> ?
    "app_eui": "0102030405060708", -> `deviceNetworkTypeLinks:networkSettings:{devEUI}`
    "app_id": "some-app-id",                         -> unique TTN App ID
    "app_key": "01020304050607080102030405060708",   -> returned during app creawtions
    "app_s_key": "01020304050607080102030405060708", -> `deviceNetworkTypeLinks:networkSettings:{appSKey}`
    "nwk_s_key": "01020304050607080102030405060708", ->`deviceNetworkTypeLinks:networkSettings:{nwkSKey}`
    "dev_addr": "01020304",        -> deviceNetworkTypeLinks:networkSettings:{devAddr}
    "dev_eui": "0102030405060708", -> `deviceNetworkTypeLinks:networkSettings:{devEUI}`
    "dev_id": "some-dev-id",       -> ?
    "disable_f_cnt_check": false,  -> `deviceNetworkTypeLinks:networkSettings:{skipFCntCheck}`
    "f_cnt_down": 0,               -> `deviceNetworkTypeLinks:networkSettings:{fCntDown}`
    "f_cnt_up": 0,                 -> `deviceNetworkTypeLinks:networkSettings:{fCntUp}`
    "last_seen": 0,                -> output only?
    "uses32_bit_f_cnt": true       -> ?
  }
}
```
