# Create (register) Company / Create User Account

* Loriot does not expose account APIs
* An API key is required for REST interactions with Loriot Servers
  - I assume this is provided by Loriot when creating a Loriot account is created
  - Question: will there be a single lpwan-owner API key for all interactions, or will a account/key be created (out of band) for each customer company that registers with lpwan-owner

# Create (register) application

* Loriot does expose APIs to create an application.
* Question: will this have to be done manually by lpwan-owner for each application that lpwan customers register?  Maybe Loriot can provide a CL specific REST API for creating applicaitons?

## Create Device Profile

* Loriot does not have the notion of device profile, but we can pull data needed from the lpwan device profile to populate device creation as needed.

# Create (register) Device

`POST https://[server].loriot.io/1/nwk/app/[APPID]/devices`

`params`
```
  APPID: Docs say: 'number: User-friendly name of the application' -> which is it?
```
Notes/Questions
- When a lpwan-user registers an app with lpwan, who is responsible for registering the app with Loriot  Does lpwan-owner do it behind the scenes?  Is the lpwan-user responsible for regestering thier apps with Loriot
- It looks like the Loriot APPID will out of our control, so we will need a way (for lpwan-owner?) to enter it via UI for each applicaiton a user creates

`body`
```
{
}
```
`rsp ->`
```json
{
  "appeui": "Device LoRaWAN AppEUI, hex string",
  "devclass": "Device LoRaWAN class, one capital character",
  "subscription": "App Subscription",
  "txrate": "daily tx rate limitation",
  "rxrate": "daily rx rate limitation",
  "appkey": "Device AppKey, as hex string",
  "devaddr": "LoRaWAN DevAddr as a hex string",
  "nwkskey": "Device NwkSKey, as hex string",
  "appskey": "Device AppSKey, as hex string",
  "seqno": "LoRaWAN FCntUp",
  "seqdn": "LoRaWAN FCntDn",
  "seqq": "LoRaWAN last enqueued sequence number",
  "seqrelax": "Enable unsecure seqno processing",
  "seqdnreset": "Seqdn reset enabled status",
  "adr": "ADR enabled / disabled",
  "adrCnt": "number of frames since last ADR"
}
```

## Enroll a device (not sure what this is)

`POST https://[server].loriot.io/1/nwk/app/[APPID]/devices`

`params`
```
  APPID: Same notes/questions as above
```
`body:`
```json
{
  "deveui":	"Optional", "maps to" : "`deviceNetworkTypeLinks:networkSettings:{devEUI}`",
}

If deveui parameter is not provided, DevEUI will be generated along with the rest of the parameters (generate new device).

```

`rsp ->`
```json
{
  "appeui": "Device LoRaWAN AppEUI, hex string",
  "devclass": "Device LoRaWAN class, one capital character",
  "appkey": "Device AppKey, as hex string",
  "devaddr": "LoRaWAN DevAddr as a hex string",
  "nwkskey": "Device NwkSKey, as hex string",
  "appskey": "Device AppSKey, as hex string",
  "seqno": "LoRaWAN FCntUp",
  "seqdn": "LoRaWAN FCntDn",
  "seqq": "LoRaWAN last enqueued sequence number",
  "seqrelax": "Enable unsecure seqno processing",
  "adr": "ADR enabled / disabled",
}
```

## Update a Device

`POST https://[server].loriot.io/1/nwk/app/[APPID]/device/[DEVEUI]`
```json
{
  "rxw": "RX window (1 or 2) to be used by default by the device",
          ?: "how does this map to `deviceProfiles:{rxDelay1, rxDROffset1, rxDataRate2, rxFreq2}",
  "seqrelax": "strict/relaxed checking", "maps to" : ?,
  "devclass": "A = Class A, B = Class B, C = Class C",
               ? : "lpwan distinguishes between C/non-C, but not A/B. What to do here",
  "adrMin": "minimum adaptive datarate to be used for ADR", "maps to" : ?,
  "adrMax": "maximum adaptive datarate to be used by ADR", "maps to" : ?,
  "adrFix": "fixed datarate to be used by ADR", "maps to" : ?,
}
```

# Key Management

## Update APPKEY

`POST https://[server].loriot.io/1/nwk/app/[APPID]/device/[DEVEUI]/appkey`
```json
{
}
```
> If the appkey parameter is supplied, the device will be assigned with the custom APPKEY. If appkey is not supplied, an APPKEY will be generated.

-> rsp : `not documented`

## Delete APPKEY

`DELETE https://[server].loriot.io/1/nwk/app/[APPID]/device/[DEVEUI]/appkey`

## Update APPSKEY

`POST https://[server].loriot.io/1/nwk/app/[APPID]/device/[DEVEUI]/appskey`
```json
{
}
```
-> rsp : `no response`

## Delete APPSKEY

`DELETE https://[server].loriot.io/1/nwk/app/[APPID]/device/[DEVEUI]/appskey`
