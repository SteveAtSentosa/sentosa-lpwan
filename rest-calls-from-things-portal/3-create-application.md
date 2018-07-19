
TTN portal page: https://console.thethingsnetwork.org/applications

# Message 1

```
POST https://console.thethingsnetwork.org/api/applications
headers:
  authority: console.thethingsnetwork.org
  method: POST
  path: /api/applications
  authorization: Bearer eyJ0eXAiOiJKV1QiLCJhb...
  origin: https://console.thethingsnetwork.org
  referer: https://console.thethingsnetwork.org/applications/add
```

body:
```json
{
  "id": "stc-app-1",
  "name": "Test App"
}
```
> note: app eui is created by the portal

rsp:
```json
{
  "id": "stc-app-1",
  "name": "Test App",
  "euis": [
    "70B3D57ED0010C49"
  ],
  "access_keys": [
    {
      "name": "default key",
      "key": "ttn-account-v2.H8Xfuw8wkyIH1botyCfFOdXwlrNOXQtsVRD-J1MObN0",
      "rights": [
        "messages:up:r",
        "messages:down:w",
        "devices"
      ]
    }
  ],
  "created": "2018-07-19T16:31:02.822Z",
  "collaborators": [
    {
      "username": "SteveAtSentosaTTN",
      "rights": [
        "settings",
        "delete",
        "collaborators",
        "devices"
      ]
    }
  ],
  "registered": false,
  "rights": [
    "settings",
    "delete",
    "collaborators",
    "devices"
  ]
}
```

# Message 2

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
  "handler": "ttn-handler-eu"
}
```

resp: none