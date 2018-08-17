# Sent from TTN Portal

https://account.thethingsnetwork.org/users/login

```json
POST https://account.thethingsnetwork.org/api/v2/users/login
{

  "username": "SteveAtSentosaTTN",   "maps to" : "users:username",
  "password": "somePassword",        "maps to" : "users:passwordHash", "note" : "TTN expects PW in the clear"
}
```

rsp:
```json
{
  "username": "SteveAtSentosaTTN",
  "email": "ttn@sentosatech.com",
  "created": "2018-07-19T16:08:18.292Z",
  "valid": true,
  "_id": "5b50b772a1a34500329cbb00",
  "canBeInvitedToSlack": true
}
```

rsp cookies:
```
session: eyJ1c2VyIjoiNWI1MGI3NzJhMWEzNDUwMDMyOWNiYjAwIn0=...
session.sig: rZcQ3PpQwUz1Q-dUddXPt_Dyic8
session_id: a6KVqF30FXU6Xm
```

# Documentation

> did not find any for login