# Extension-API
Documentation to help you create extensions for WebCull

# Index
1. [General](#general)
1. [Load current account](#load-current-account)
1. [Get list of accounts](#get-list-of-accounts)
1. [Switch an account](#switch-an-account)
1. [Modify bookmark details](#modify-bookmark-details)
1. [Move bookmark](#move-bookmark)
1. [Save bookmark](#save-bookmark)
1. [Remove stacks](#remove-stacks)
1. [Process web data](#process-web-data)



## General
#### Required header data
All requests must have the following header data
Key            |Value
---------------|---------------------------------
Content-Type   |application/x-www-form-urlencoded
Accept-Encoding|gzip



## Load current account
Load the currently active account bookmark structure.
```
[POST] https://webcull.com/api/load
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION
}
```
> *WEBCULL_SESSION: This is captured from the `__DbSessionNamespaces` cookie created by visiting `https://webcull.com`

##### Response when there's a session available
```
{
	"success" : "TRUE",
	"stacks" : [...]
}
```

##### Response when there's no session available
```
{
	"success" : "TRUE",
	"no_user" : "TRUE"
}
```


## Get list of accounts
Output a list of accounts that are currently authenticated on this session
```
[POST] https://webcull.com/api/accounts
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION
}
```


##### Response when there's users
```
{
	"users": [
		{
			"name": "USERS_NAME",
			"email": "USERS_EMAIL",
			"icon": "USERS_ICON"
		},
		...
	],
	"success": "true"
}
```

##### Response when there's no users
```
{
	"users": [],
	"success": "true"
}
```

## Switch an account
Change the currently active account within the session (Only applies to user who have multiple accounts logged into one session)
```
[POST] https://webcull.com/api/switch
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	"email" : "webfeeds@webcull.com"
}
```

##### Response when successful
```
{
	"stacks": STACK_OBJECT,
	"account": "EMAIL_THAT_WAS_SWITCHED",
	"success": "true"
}
```

##### Response when unsuccessful
```
{
	"success": "true",
	"unavailable": "true"
}
```


## Modify bookmark details
Load the currently active account bookmark structure.
```
[POST] https://webcull.com/api/modify
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	proc : 'modify',
	stack_id : STACK_ID,
	name : KEY,
	value : VALUE
}
```
> KEY: Is a string with the value of `order_id`, `value`, `nickname`, `tags`, `notes`


##### Response when there's a session available
```
{
	"success" : "TRUE",
	"stacks" : [...]
}
```

##### Response when there's no session available
```
{
	"success" : "TRUE",
	"no_user" : "TRUE"
}
```


## Move bookmark
```
[POST] https://webcull.com/api/savelocation
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	arrCrumbs : "STACK_ID,STACK_ID,,",
	arrCrumbsValues : ",,NAME_OF_NEW_STACK,NAME_OF_NEW_STACK",
	stack_id : STACK_ID
}
```

##### Response when successful
```
{
	"success" : "TRUE",
	"stack_id" : STACK_ID,
	"order_id" : ORDER_NUMBER,
	"parent_id": PARENT_ID,
	"new_stack_ids" : [
		STACK_ID, 
		STACK_ID, 
		...
	]
}
```


## Save bookmark
```
[POST] https://webcull.com/api/autosavelink
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	url : WEBSITE_URL
}
```

##### Response when the bookmark has already been saved
```
{
	"bookmarks_found" : [
		{
			"stack_id" : STACK_ID,
			"parent_id" : PARENT_ID,
			"web_data_id" : WEB_DATA_ID,
			"is_url" : BOOL,
			"order_id" : order_id,
			"parse_date" : STRING,
			"nickname" : STRING,
			"value" : STRING,
			"tags" : STRING,
			"icon" : STRING,
			"notes" : STRING,
			"modified" : STRING,
			"created" : STRING
		}
	],
	"user" : [
		"hash" : STRING,
		"name" : STRING,
		"icon" : STRING
	],
	"stacks" : {
		STACK_CLUSTER
	},
	"success": "TRUE"
}
```

##### Response when its a newly saved bookmark
```
{
	"web_data_id" : WEB_DATA_ID,
	"value" : URL,
	"parent_id" : 0,
	"is_url" : BOOL,
	"nickname" : STRING,
	"order_id" : ORDER_NUMBER,
	"stack_id" : STACK_ID,
	"success" : TRUE,
	"new_bookmark" : "true",
	"user" : [
		"hash" : STRING,
		"name" : STRING,
		"icon" : STRING
	],
	"stacks" : {
		STACK_CLUSTER
	}
}
```


## Remove stacks
```
[POST] https://webcull.com/api/remove
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	"stack_id" : "STACK_ID, STACK_ID, ..."
}
```

##### Response successful
```
{
	"success" : "true"
}
```


## Process web data
```
[POST] https://webcull.com/api/process
```
#### POST params
```
{
	"__DbSessionNamespaces" : WEBCULL_SESSION,
	"web_data_id" : WEB_DATA_ID
}
```

##### Response successful
```
{
	"phone": STRING,
	"email": STRING,
	"parse_date": TIMESTAMP,
	"icon": STRING
}
```


## The end
Are we missing something? Let us know on [twitter](https://twitter.com/webcull).
