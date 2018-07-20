------------------
  Account Server
------------------

https://www.thethingsnetwork.org/docs/network/account/

In order to use the API, you need to request a
[client ID](https://www.thethingsnetwork.org/docs/network/account/clientid.html)

DJS:  So what I said before was kinda right kinda not.  The Company can be the account, but the access keys are per application not per account.  So they are not excatly like users.  


## Create an application on the account server
`POST /applications`
```
{
  id: String
  name: String
  euis: [String]     # list of euis app is reachable at
  rights: [String]   # list of rights current user has for the app (which user?)
  collaborators: [{
    username: String
    email: String
    rights: [String] # list of rights collaborator has to the applicaiton
  }]
  access_keys: [{
    name: String
    key: String
    rights: [String] # the rights the key will grant if used
  }]
  created: Date-Time
  deleted: Date-Time # only if app was deleted
}
rsp -> created resource data (same structure as input)
```

## Add an access key to an application
`POST /applications/{app_id}/access-keys`
```
{
  name: String
  rights: [String] # the rights the key will grant if used
}
```
> Where is the key?

## Associate a token with an application
`POST /applications/{app_id}/token`
```
{
  # credentials for the token exchange
}
```

## Add an EUI to the application
`PUT /applications/{app_id}/euis/{eui}`

---------------------------
  Application Manager API
---------------------------

https://www.thethingsnetwork.org/docs/applications/manager/api.html/

To use this API you need an Application Access Key or JWT.

`DELETE /applications/{app_id}`

`DELETE /applications/{app_id}/devices/{dev_id}`

`GET /applications/{app_id}`

`GET /applications/{app_id}/devices/{dev_id}`

`GET /applications/{app_id}/devices`

## Register applictions

`POST /applications`
```
{
  app_id: String
}
```

## Update Application settings
`PUT /applications/{app_id}`
```
{
  app_id: "some-app-id",
  converter: "function Converter(decoded, port) {...",
  decoder: "function Decoder(bytes, port) {...",
  encoder: "Encoder(object, port) {...",
  payload_format: "",
  register_on_join_access_key: "",
  validator: "Validator(converted, port) {..."
}
```

## Create/Update devices
`PUT/POST /applications/{app_id}/devices/{dev_id}`

`PUT/POST /applications/{app_id}/devices`

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
    "activation_constraints": "local",
    "app_eui": "0102030405060708",
    "app_id": "some-app-id",
    "app_key": "01020304050607080102030405060708",
    "app_s_key": "01020304050607080102030405060708",
    "dev_addr": "01020304",
    "dev_eui": "0102030405060708",
    "dev_id": "some-dev-id",
    "disable_f_cnt_check": false,
    "f_cnt_down": 0,
    "f_cnt_up": 0,
    "last_seen": 0,
    "nwk_s_key": "01020304050607080102030405060708",
    "uses32_bit_f_cnt": true
  }
}
```

------------
  Data API
------------

https://www.thethingsnetwork.org/docs/applications/mqtt/api.html

### Uplink Messages
`Topic: <AppID>/devices/<DevID>/up`
```
{
  "app_id": "my-app-id",              // Same as in the topic
  "dev_id": "my-dev-id",              // Same as in the topic
  "hardware_serial": "0102030405060708", // In case of LoRaWAN: the DevEUI
  "port": 1,                          // LoRaWAN FPort
  "counter": 2,                       // LoRaWAN frame counter
  "is_retry": false,                  // Is set to true if this message is a retry (you could also detect this from the counter)
  "confirmed": false,                 // Is set to true if this message was a confirmed message
  "payload_raw": "AQIDBA==",          // Base64 encoded payload: [0x01, 0x02, 0x03, 0x04]
  "payload_fields": {},               // Object containing the results from the payload functions - left out when empty
  "metadata": {
    "airtime": 46336000,              // Airtime in nanoseconds
    "time": "1970-01-01T00:00:00Z",   // Time when the server received the message
    "frequency": 868.1,               // Frequency at which the message was sent
    "modulation": "LORA",             // Modulation that was used - LORA or FSK
    "data_rate": "SF7BW125",          // Data rate that was used - if LORA modulation
    "bit_rate": 50000,                // Bit rate that was used - if FSK modulation
    "coding_rate": "4/5",             // Coding rate that was used
    "gateways": [
      {
        "gtw_id": "ttn-herengracht-ams", // EUI of the gateway
        "timestamp": 12345,              // Timestamp when the gateway received the message
        "time": "1970-01-01T00:00:00Z",  // Time when the gateway received the message - left out when gateway does not have synchronized time
        "channel": 0,                    // Channel where the gateway received the message
        "rssi": -25,                     // Signal strength of the received message
        "snr": 5,                        // Signal to noise ratio of the received message
        "rf_chain": 0,                   // RF chain where the gateway received the message
        "latitude": 52.1234,             // Latitude of the gateway reported in its status updates
        "longitude": 6.1234,             // Longitude of the gateway
        "altitude": 6                    // Altitude of the gateway
      },
      //...more if received by more gateways...
    ],
    "latitude": 52.2345,              // Latitude of the device
    "longitude": 6.2345,              // Longitude of the device
    "altitude": 2                     // Altitude of the device
  }
}
```

### Device Activations
`Topic: <AppID>/devices/<DevID>/events/activations`
```
{
  "app_eui": "0102030405060708", // EUI of the application
  "dev_eui": "0102030405060708", // EUI of the device
  "dev_addr": "26001716",        // Assigned address of the device
  "metadata": {
    // Same as with Uplink Message
  }
}
```


-------------------------
  Authentication Server
-------------------------

[Overview/API](https://www.thethingsnetwork.org/docs/network/account/authentication.html)
