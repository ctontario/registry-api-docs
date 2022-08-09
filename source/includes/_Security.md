
# Security


## Authentication - <em>Authentication</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/security/authentication"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/AuthenticationBody",
    "type": "object",
    "properties": {"username": {"type": "string"}, "password": {"type": "string"}},
    "required": ["username", "password"]
  }
}
```


> Response Schema

```json
{
  "id": "/AuthenticationResponse",
  "type": "object",
  "properties": {
    "id": {"type": "object"},
    "token": {"type": "string"},
    "privilege": {"type": "string"}
  },
  "required": ["id", "token", "privilege"]
}
```



<aside class="notice">This route is public and does not require authentication</aside>


Tests a users credentials, and if successful returns a token to access the system

### HTTP Request

`POST /security/authentication`



### Authorization
 
N/A

## Logout - <em>Logout</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/security/logout"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/ActionResponse",
  "type": "object",
  "properties": {
    "status": {"type": "string"},
    "action": {"type": "string"},
    "id": {"type": ["object", "null"]},
    "result": {"type": ["object", "array", "string"]}
  },
  "required": ["status", "action", "id"]
}
```


Sets a users token as logged out to prevent access immediately

### HTTP Request

`PUT /security/logout`



### Authorization
 
N/A

## PrivilegeToken - <em>Get Privilege Token</em>


```shell
curl "https://ctoregistry.com/api/v1/security/privilegeToken"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/PrivilegeTokenResponse",
  "type": "object",
  "properties": {"privilege": {"type": "string"}},
  "required": ["privilege"]
}
```


Gets the currently authenticated users privilege token

### HTTP Request

`GET /security/privilegeToken`



### Authorization
 
N/A