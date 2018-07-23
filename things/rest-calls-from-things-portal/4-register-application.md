# Sent from TTN Portal

2nd message sent as part of create application proccess on the UI

```
POST https://console.thethingsnetwork.org/api/applications/stc-app-1/registration
headers:
  authority: console.thethingsnetwork.org
  method: PUT
  path: /api/applications/stc-app-1/registration
  authorization: Bearer eyJ0eXAiOiJKV1QiLCJhb
  origin: https://console.thethingsnetwork.org
  referer: https://console.thethingsnetwork.org/applications/stc-app-1
```

body:
```json
{
  "handler": "ttn-handler-eu", "maps to" : ?, "note" : "new ui input needed?"
}
```

resp: none

# Documentation

> Have not found correspnding API (yet), does below API do the same thing?

[Part of Application Manager API](https://www.thethingsnetwork.org/docs/applications/manager/api.html/)

`POST /applications`
```
{
  app_id: String
}
```
