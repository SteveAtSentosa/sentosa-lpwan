
 TTN portal page: https://console.thethingsnetwork.org/applications/stc-app-1/devices

# Message 1

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
  "dev_id": "stc-dev-1",
  "app_eui": "70B3D57ED0010C49",
  "dev_eui": "1234567890098765"
}
```

rsp:
```json
{
  "app_id": "stc-app-1",
  "dev_id": "stc-dev-1",
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