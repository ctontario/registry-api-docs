
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
    "otpToken": {"type": "string", "description": "will be returned if 2FA is required"},
    "token": {"type": "string", "description": "will be returned if no 2FA"},
    "privilege": {"type": "string", "description": "will be returned if no 2FA"}
  },
  "required": ["id"]
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

## OTPDisable - <em>OTP Disable</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/security/otp/disable"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/OtpDisableRequestBody",
    "type": "object",
    "properties": {"userId": {"type": "string"}},
    "required": ["userId"]
  }
}
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




### HTTP Request

`POST /security/otp/disable`



### Authorization
 
N/A

## OTPGenerate - <em>OTP Generate</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/security/otp/generate"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/OtpGenerateRequestBody",
    "type": "object",
    "properties": {"userId": {"type": "string"}},
    "required": ["userId"]
  }
}
```


> Response Schema

```json
{
  "id": "/OtpGenerateResponse",
  "properties": {
    "ascii": {"type": "string"},
    "hex": {"type": "string"},
    "base32": {"type": "string"},
    "authUrl": {"type": "string"}
  },
  "required": ["base32", "authUrl"]
}
```




### HTTP Request

`POST /security/otp/generate`



### Authorization
 
N/A

## OTPValidate - <em>OTP Validate</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/security/otp/validate"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/OtpValidateRequestBody",
    "type": "object",
    "properties": {"username": {"type": "string"}, "token": {"type": "string"}},
    "required": ["username", "token"]
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
    "otpToken": {"type": "string", "description": "will be returned if 2FA is required"},
    "token": {"type": "string", "description": "will be returned if no 2FA"},
    "privilege": {"type": "string", "description": "will be returned if no 2FA"}
  },
  "required": ["id"]
}
```




### HTTP Request

`POST /security/otp/validate`



### Authorization
 
N/A

## OTPVerify - <em>OTP Verify</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/security/otp/verify"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/OtpVerifyRequestBody",
    "type": "object",
    "properties": {"userId": {"type": "string"}, "token": {"type": "string"}},
    "required": ["userId", "token"]
  }
}
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




### HTTP Request

`POST /security/otp/verify`



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