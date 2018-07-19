# Current lpwan UI Inpfut fields

### Create Company

```
Company Name : `companies:name`
Admin User Name: `users:username`
Admin User Password: `users:passwordHash`
Admin User Email Address: `users:email`
Network Types: (checkbox) `networkTypes:name` / `companyNetworkTypeLinks:companyId<>networkTypeId`
  LoRa:
    LoRaWan Region: `companyNetworkTypeLinks:networkSettings: {serviceProfile:{region}}`
```

### Create User

```
User Name: `users:username`
Email: `users:email`
Password: `users:passwordHash`
```

### Create Application

```
CompanyId (implicit by logged in user): `applications:companyId`
App Name: `applications:name`
App Description: `applications:description`
Post URL (sensor data destinaion): `applications:baseUrl`
Reporting Protocol: `applications:reportingProtocolId`
Network Types: (checkbox) `networkTypes:name` / `applicationNetworkTypeLinks:applicationId<>networkTypeId`
  LoRa:
    Payload Codec: `applicationNetworkTypeLinks:networkSettings: {payloadCodec}`
```

### Create Device Profile

```
CompanyId (implicit by logged in user): `deviceProfiles:companyId`
Device Profile Name: `deviceProfiles:name`
Device Profile Description: `deviceProfiles:description`
Network Types: (checkbox) `networkTypes:name` / `deviceProfiles:networkTypeId`
  LoRa:
    General: LoraWAN MAC Version: `deviceProfiles:networkSettings:{macVersion}`
             LoraWAN Regional Paramaters Revision: `deviceProfiles:networkSettings:{regParamsRevision}`
             Max EIRP: `deviceProfiles:networkSettings:{maxEIRP}`
    Join:    Supports Join (y/n): `deviceProfiles:networkSettings:{supportsJoin}`
             RX1 Delay: `deviceProfiles:networkSettings:{rxDelay1}`
             RX1 Data Rate Offset: `deviceProfiles:networkSettings:{rxDROffset1}`
             RX2 Data Rate: `deviceProfiles:networkSettings:{rxDataRate2}`
             RX2 Channel Frequency: `deviceProfiles:networkSettings:{rxFreq2}`
             Factory Preset Frequencies (list): `deviceProfiles:networkSettings:{factoryPresetFreqs}`
    Class-C: Supports Class-C (y/n): `deviceProfiles:networkSettings:{supportsClassC}`
             Class-C Confirmed Downlink Timeout: `deviceProfiles:networkSettings:{classCTimeout}`
```

### Create Device

```
Application Id (implicit by selected app): `devices:applicationId`
Device Name: `devices:name`
Device Description: `devices:description`
Device Model: `devices:deviceModel`
Network Types: (checkbox) `networkTypes:name` / `deviceNetworkTypeLinks:deviceId<>networkTypeId`
  LoRa:
    Device Profile (selection list) : `deviceNetworkTypeLinks:deviceProfileId`
    Device EUI: `deviceNetworkTypeLinks:networkSettings:{devEUI}`
    Device Address: `deviceNetworkTypeLinks:networkSettings:{devAddr}`
    Network Session Key: `deviceNetworkTypeLinks:networkSettings:{nwkSKey}`
    Application Session Key: `deviceNetworkTypeLinks:networkSettings:{appSKey}`
    Uplink Frame Counter: `deviceNetworkTypeLinks:networkSettings:{fCntUp}`
    Downlink Frame Counter: `deviceNetworkTypeLinks:networkSettings:{fCntDown}`
    Disable Frame Counter Validation (y/n): `deviceNetworkTypeLinks:networkSettings:{skipFCntCheck}`
    ??? : `deviceNetworkTypeLinks:networkSettings:{isABP}`
```


### lpwan UI operations that don't result in external messaging

```
Create Network Type
Create Network Provider
Create Network Protocols
Create Network
```