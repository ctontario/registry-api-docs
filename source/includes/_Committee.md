
# Committee


## CommitteeCheckUniqueCode - <em>Check Committee Unique Code</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-code/:code/:committeeId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeUniqueCodeParams",
    "type": "object",
    "properties": {
      "code": {"type": "string"},
      "committeeId": {"type": "string"}
    },
    "required": ["code"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an committee code is already in use or not.

### HTTP Request

`GET /committee/unique-code/:code/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeCheckUniqueName - <em>Check Committee Unique Name</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-name/:name/:committeeId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeUniqueName",
    "type": "object",
    "properties": {
      "name": {"type": "string"},
      "committeeId": {"type": "string"}
    },
    "required": ["name"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an committee name is already in use or not.

### HTTP Request

`GET /committee/unique-name/:name/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeCheckUniqueShortName - <em>Check Committee Unique Short Name</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-short-name/:shortName/:committeeId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeUniqueShortName",
    "type": "object",
    "properties": {
      "shortName": {"type": "string"},
      "committeeId": {"type": "string"}
    },
    "required": ["shortName"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an committee short name is already in use or not.

### HTTP Request

`GET /committee/unique-short-name/:shortName/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeCheckUniqueStreamName - <em>Check Committee Unique Stream Name</em>


```shell
curl "https://cto.local:9000/api/v1/committee/unique-stream-name/:streamName/:committeeId?"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeUniqueStreamName",
    "type": "object",
    "properties": {
      "streamName": {"type": "string"},
      "committeeId": {"type": "string"}
    },
    "required": ["streamName"]
  }
}
```


> Response Schema

```json
{
  "id": "/CheckExistsResponse",
  "type": "object",
  "properties": {"exists": {"type": "boolean"}},
  "required": ["exists"]
}
```


Checks to see if an committee Stream Name is already in use or not.

### HTTP Request

`GET /committee/unique-stream-name/:streamName/:committeeId?`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeCreation - <em>Create Committee</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/committee/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/CommitteeCreation",
    "type": "object",
    "properties": {
      "code": {"type": "string", "description": "The committee's code"},
      "name": {"type": "string", "description": "The name of the committee"},
      "shortName": {
        "type": "string",
        "description": "The short name of the committee"
      },
      "streamName": {
        "type": "string",
        "description": "The name of the committee in CTO Stream"
      },
      "type": {
        "type": "string",
        "description": "The type of committee",
        "enum": ["reb", "steering"]
      },
      "status": {
        "type": "string",
        "description": "The status of the committee",
        "enum": ["pending", "active", "deleted", "suspended"]
      },
      "statusEffectiveChangeDt": {
        "type": "string",
        "description": "The effective date of a change of status"
      },
      "parentInstitutionId": {
        "type": "string",
        "description": "The ID of the parent institution"
      }
    },
    "required": ["name", "code", "type", "status", "parentInstitutionId"]
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
    "id": {"type": "object|null"},
    "result": {"type": "object|array|string"}
  },
  "required": ["status", "action", "id"]
}
```


Creates a new committee

### HTTP Request

`POST /committee/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeDictionary - <em>Committee Dictionary</em>


```shell
curl "https://cto.local:9000/api/v1/dictionary/committee"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Response Schema

```json
{
  "id": "/CommitteeDictionaryResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "name": {"type": "string"},
          "streamName": {"type": "string"},
          "code": {"type": "string"}
        },
        "required": ["id", "name", "streamName", "code"]
      }
    }
  }
}
```


Gets the list of committees that are present in the system

### HTTP Request

`GET /dictionary/committee`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeList - <em>Get Committee List</em>


```shell
curl "https://cto.local:9000/api/v1/committee/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/ListQuery",
    "type": "object",
    "properties": {
      "count": {"type": "string"},
      "offset": {"type": "string"},
      "limit": {"type": "string"},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": "string"}
    }
  }
}
```


> Response Schema

```json
{
  "id": "/CommitteeListResponse",
  "type": "object",
  "properties": {
    "meta": {
      "id": "/ListMeta",
      "properties": {
        "count": {"type": "number"},
        "limit": {"type": "number"},
        "offset": {"type": "number"}
      },
      "required": ["count", "limit", "offset"]
    },
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "code": {"type": "string"},
          "name": {"type": "string"},
          "type": {"type": "string"},
          "status": {"type": "string"},
          "institution": {
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "code": {"type": "string"},
              "name": {"type": "string"}
            },
            "required": ["id", "code", "name"]
          },
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "code",
          "name",
          "type",
          "status",
          "institution",
          "createDt",
          "updateDt"
        ]
      }
    }
  }
}
```


Gets the list of committees the user can access.

### HTTP Request

`GET /committee/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeListForUser - <em>Committees for User</em>


```shell
curl "https://cto.local:9000/api/v1/committee/user/:userId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/UserParams",
    "type": "object",
    "properties": {"userId": {"type": "string", "required": true}},
    "required": ["userId"]
  }
}
```


> Response Schema

```json
{
  "id": "/UserCommitteesResponse",
  "type": "object",
  "properties": {
    "user": {
      "id": "/UserShortProfile",
      "properties": {
        "id": {"type": "object"},
        "username": {"type": "string"},
        "contact": {
          "type": "object",
          "properties": {
            "firstName": {"type": "string"},
            "middleName": {"type": "string"},
            "lastName": {"type": "string"},
            "title": {
              "type": "string",
              "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
            }
          },
          "required": ["firstName", "lastName", "title"]
        },
        "institutionIds": {"type": "array", "items": {"type": "object"}}
      },
      "required": ["id", "username", "contact", "institutionIds"]
    },
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "committee": {
            "type": "object",
            "properties": {
              "id": {"type": "object"},
              "name": {"type": "string"}
            },
            "required": ["id", "name"]
          },
          "id": {"type": "object"},
          "role": {"type": "string"},
          "status": {"type": "string"},
          "joinDt": {"type": "date"},
          "endDt": {"type": "date"}
        },
        "required": ["committee", "id", "role", "status", "joinDt"]
      }
    }
  }
}
```


Get the committees that a user belongs too

### HTTP Request

`GET /committee/user/:userId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
self | N/A | N/A|N/A
system | admin | N/A|N/A
institution | admin | user|N/A

## CommitteeMemberCreation - <em>Committee Add Member</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/committee/:committeeId/members/add"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeParams",
    "type": "object",
    "properties": {"committeeId": {"type": "string"}},
    "required": ["committeeId"]
  },
  "body": {
    "id": "/CommitteeMemberCreation",
    "type": "object",
    "properties": {
      "userId": {
        "type": "string",
        "description": "The userId of the user's account to add as a committee member"
      },
      "role": {
        "type": "string",
        "description": "The role of the member",
        "enum": ["chair", "member", "staff", "director", "contact"]
      },
      "status": {
        "type": "string",
        "description": "The status of the member",
        "enum": ["pending", "active", "suspended", "ended"]
      },
      "joinDt": {
        "type": "string",
        "description": "The date the member joined the committee"
      }
    },
    "required": ["userId", "role", "status"]
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
    "id": {"type": "object|null"},
    "result": {"type": "object|array|string"}
  },
  "required": ["status", "action", "id"]
}
```


Adds a user for one existing committee

### HTTP Request

`POST /committee/:committeeId/members/add`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeMemberEdit - <em>Committee Edit Member</em>


```shell
curl -X POST "https://cto.local:9000/api/v1/committee/:committeeId/members/edit"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeParams",
    "type": "object",
    "properties": {"committeeId": {"type": "string"}},
    "required": ["committeeId"]
  },
  "body": {
    "id": "/CommitteeMemberEdit",
    "type": "object",
    "properties": {
      "userId": {
        "type": "string",
        "description": "The userId of the user's account to add as a committee member"
      },
      "role": {
        "type": "string",
        "description": "The role of the member",
        "enum": ["chair", "member", "staff", "director", "contact"]
      },
      "status": {
        "type": "string",
        "description": "The status of the member",
        "enum": ["pending", "active", "suspended", "ended"]
      },
      "joinDt": {
        "type": "string",
        "description": "The date the member joined the committee"
      },
      "memberId": {
        "type": "string",
        "description": "The userId of the user's account to add as a committee member"
      }
    },
    "required": ["userId", "role", "status", "memberId"]
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
    "id": {"type": "object|null"},
    "result": {"type": "object|array|string"}
  },
  "required": ["status", "action", "id"]
}
```


updates user information for one existing committee

### HTTP Request

`POST /committee/:committeeId/members/edit`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A

## CommitteeMembers - <em>Committee Members</em>


```shell
curl "https://cto.local:9000/api/v1/committee/:committeeId/members"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeParams",
    "type": "object",
    "properties": {"committeeId": {"type": "string"}},
    "required": ["committeeId"]
  }
}
```


> Response Schema

```json
{
  "id": "/CommitteeMembersResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "role": {"type": "string"},
          "status": {"type": "string"},
          "createDt": {"type": "date"},
          "endDt": {"type": "date"},
          "user": {
            "id": "/UserShortProfile",
            "properties": {
              "id": {"type": "object"},
              "username": {"type": "string"},
              "contact": {
                "type": "object",
                "properties": {
                  "firstName": {"type": "string"},
                  "middleName": {"type": "string"},
                  "lastName": {"type": "string"},
                  "title": {
                    "type": "string",
                    "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                  }
                },
                "required": ["firstName", "lastName", "title"]
              },
              "institutionIds": {"type": "array", "items": {"type": "object"}}
            },
            "required": ["id", "username", "contact", "institutionIds"]
          }
        },
        "required": ["id", "role", "status", "createDt", "user"]
      }
    }
  }
}
```


gets all the members of a committee

### HTTP Request

`GET /committee/:committeeId/members`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
committee | member | committee|N/A

## CommitteeProfile - <em>Get Committee</em>


```shell
curl "https://cto.local:9000/api/v1/committee/:committeeId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/CommitteeParams",
    "type": "object",
    "properties": {"committeeId": {"type": "string"}},
    "required": ["committeeId"]
  }
}
```


> Response Schema

```json
{
  "id": "/CommitteeProfileResponse",
  "type": "object",
  "properties": {
    "committee": {
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "code": {"type": "string"},
        "name": {"type": "string"},
        "type": {"type": "string"},
        "status": {"type": "string"},
        "shortName": {"type": "string"},
        "streamName": {"type": "string"},
        "institution": {
          "type": "object",
          "properties": {
            "id": {"type": "object"},
            "code": {"type": "string"},
            "name": {"type": "string"}
          },
          "required": ["id", "code", "name"]
        },
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"}
      },
      "required": [
        "id",
        "code",
        "name",
        "type",
        "status",
        "shortName",
        "streamName",
        "institution",
        "createDt",
        "updateDt"
      ]
    }
  }
}
```


Gets the data associated to one committee.

### HTTP Request

`GET /committee/:committeeId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
committee | member | committee|N/A

## CommitteeUpdate - <em>Update Committee</em>


```shell
curl -X PUT "https://cto.local:9000/api/v1/committee/:committeeId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "body": {
    "id": "/CommitteeUpdate",
    "type": "object",
    "properties": {
      "code": {"type": "string", "description": "The committee's code"},
      "name": {"type": "string", "description": "The name of the committee"},
      "shortName": {
        "type": "string",
        "description": "The short name of the committee"
      },
      "streamName": {
        "type": "string",
        "description": "The name of the committee in CTO Stream"
      },
      "type": {
        "type": "string",
        "description": "The type of committee",
        "enum": ["reb", "steering"]
      },
      "status": {
        "type": "string",
        "description": "The status of the committee",
        "enum": ["pending", "active", "deleted", "suspended"]
      },
      "statusEffectiveChangeDt": {
        "type": "string",
        "description": "The effective date of a change of status"
      },
      "parentInstitutionId": {
        "type": "string",
        "description": "The ID of the parent institution"
      }
    },
    "required": ["name", "type"]
  },
  "params": {
    "id": "/CommitteeParams",
    "type": "object",
    "properties": {"committeeId": {"type": "string"}},
    "required": ["committeeId"]
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
    "id": {"type": "object|null"},
    "result": {"type": "object|array|string"}
  },
  "required": ["status", "action", "id"]
}
```


Updates an existing committee

### HTTP Request

`PUT /committee/:committeeId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A