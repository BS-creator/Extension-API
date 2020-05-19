# Extension-API
Documentation to help you create extensions for WebCull

## Initalize Account
Load the currently active account bookmark structure.
```
[POST] https://webcull.com/api/load
```
### [POST] params
```
[
  "__DbSessionNamespaces" : WEBCULL_SESSION
]
```
> *WEBCULL_SESSION: This is captured from the `__DbSessionNamespaces` key created by visiting `https://webcull.com`

#### Response when there's a session available
```
[
  "success" : "TRUE",
  "stacks" : [...]
]
```

#### Response when there's no session available
```
[
  "success" : "TRUE",
  "no_user" : "TRUE"
]
```
