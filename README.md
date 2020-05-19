# Extension-API
Documentation to help you create extensions for WebCull

# Index
1. [Load current account](#load-current-account)
1. [Modify bookmark details](#modify-bookmark-details)

## Load current account
Load the currently active account bookmark structure.
```
[POST] https://webcull.com/api/load
```
#### POST params
```
[
	"__DbSessionNamespaces" : WEBCULL_SESSION
]
```
> *WEBCULL_SESSION: This is captured from the `__DbSessionNamespaces` key created by visiting `https://webcull.com`

##### Response when there's a session available
```
[
	"success" : "TRUE",
	"stacks" : [...]
]
```

##### Response when there's no session available
```
[
	"success" : "TRUE",
	"no_user" : "TRUE"
]
```

## Modify bookmark details
Load the currently active account bookmark structure.
```
[POST] https://webcull.com/api/modify
```
#### POST params
```
[
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	proc : 'modify',
	stack_id : STACK_ID,
	name : KEY,
	value : VALUE
]
```
> KEY: Is a string with the value of `order_id`, `value`, `nickname`, `tags`, `notes`

##### Response when there's a session available
```
[
	"success" : "TRUE",
	"stacks" : [...]
]
```

##### Response when there's no session available
```
[
	"success" : "TRUE",
	"no_user" : "TRUE"
]
```
