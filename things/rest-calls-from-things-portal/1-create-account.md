# Sent from TTN Portal

https://account.thethingsnetwork.org/register

```json
POST https://account.thethingsnetwork.org/api/v2/users
{
  "username": "SteveAtSentosaTTN",   "maps to" : "users:username",
  "email": "ttn@sentosatech.com",    "maps to" : "users:email",
  "password": "somePassword",        "maps to" : "users:passwordHash", "note" : "things expects PW in the clear"
}
rsp:
{
  "email": "ttn@sentosatech.com",
  "user": {
    "username": "SteveAtSentosaTTN",
    "email": "ttn@sentosatech.com",
    "created": "2018-07-19T16:08:18.292Z",
    "name": {},
    "valid": false,
    "_id": "5b50b772a1a34500329cbb00",
    "canBeInvitedToSlack": true
  }
}
```

rsp cookies:
```
session: eyJ1c2VyIjoiNWI1MGQxNzFhMWEzNDUwMDMyOWNjMDQxIn0...
session.sig: FLzDtVjDuyb77TV13VlIHXQUfzk
```

# Documentation

> did not find any for create account