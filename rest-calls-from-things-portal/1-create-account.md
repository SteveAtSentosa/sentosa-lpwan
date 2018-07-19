
TTN portal page: https://account.thethingsnetwork.org/register

# Message 1

```json
POST https://account.thethingsnetwork.org/api/v2/users
{
  "email": "ttn@sentosatech.com",
  "username": "SteveAtSentosaTTN",
  "password": "somePassword"
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

rsp cookies
```
session: eyJ1c2VyIjoiNWI1MGQxNzFhMWEzNDUwMDMyOWNjMDQxIn0...
session.sig: FLzDtVjDuyb77TV13VlIHXQUfzk
```