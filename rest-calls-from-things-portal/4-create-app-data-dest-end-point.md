
TTN Portal Page: https://console.thethingsnetwork.org/applications/stc-app-1/integrations

# Message 1

```
POST https://console.thethingsnetwork.org/api/applications/stc-app-1/integrations/http-ttn
headers:
  authority: console.thethingsnetwork.org
  method: POST
  path: /api/applications/stc-app-1/integrations/http-ttn
  scheme: https
  authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI...
  origin: https://console.thethingsnetwork.org
  referer: https://console.thethingsnetwork.org/applications/stc-app-1/integrations/create/http-ttn
```

payload:
```json
{
  "process_id": "stc-integration-proc-id-1",
  "access_key": "ttn-account-v2.H8Xfuw8wkyIH1botyCfFOdXwlrNOXQtsVRD-J1MObN0",
  "settings": {
    "TTN_APP_ACCESS_KEY": "ttn-account-v2.H8Xfuw8wkyIH1botyCfFOdXwlrNOXQtsVRD-J1MObN0",
    "TTI_URL": "https://stc-app-1:8080",
    "TTI_METHOD": "POST",
    "TTI_AUTHORIZATION": "some-auth-header-value"
  }
}
```

resp:
```json
{
  "process_id": "stc-integration-proc-id-1",
  "platform": "",
  "app_id": "stc-app-1",
  "mqtt_broker": "eu.thethings.network:1883",
  "settings": {
    "TTI_AUTHORIZATION": "some-auth-header-value",
    "TTI_METHOD": "POST",
    "TTI_URL": "https://stc-app-1:8080",
    "TTN_APP_ACCESS_KEY": "ttn-account-v2.H8Xfuw8wkyIH1botyCfFOdXwlrNOXQtsVRD-J1MObN0"
  },
  "url": ""
}
```