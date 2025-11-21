
# QuickSTARTAdmin


## QuickSTARTAdminStartupChecklist - <em>QuickSTARTAdmin Startup Checklist Profile</em>


```shell
curl "https://ctoregistry.com/api/v1/quick-start-admin/startup-checklist"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/QuickStartStartupChecklistResponse",
  "type": "object",
  "properties": {
    "startupChecklist": {
      "id": "/QuickStartStartupChecklist",
      "properties": {
        "version": {"type": "number"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "documents": {
          "type": "array",
          "items": {
            "id": "/QuickStartStartupChecklistDocument",
            "properties": {
              "ordinal": {"type": "number"},
              "label": {"type": "string"},
              "description": {"type": "string"},
              "footnote": {"type": "string"},
              "isRequiredForREBSubmission": {"type": "boolean"},
              "code": {"type": "string"},
              "type": {"type": "string", "enum": ["budget", "contract", "generic"]}
            },
            "required": ["ordinal", "label", "code", "type", "isRequiredForREBSubmission"]
          }
        }
      },
      "required": ["version", "createDt", "updateDt", "documents"]
    }
  }
}
```


Gets the currently set values for the startup checklist.

### HTTP Request

`GET /quick-start-admin/startup-checklist`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A

## UpdateQuickSTARTAdminStartupChecklist - <em>QuickSTARTAdmin Startup Checklist Update</em>


```shell
curl -X PUT "https://ctoregistry.com/api/v1/quick-start-admin/startup-checklist"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{"body": {"id": "/QuickStartAdminStartupChecklistBody", "type": "object", "required": []}}
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


Updates the currently set values for the startup checklist.

### HTTP Request

`PUT /quick-start-admin/startup-checklist`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | quickStartAdmin | N/A|N/A