
# Study


## DeleteStudyUserAccess - <em>Save Study User Access</em>


```shell
curl -X DELETE "https://ctoregistry.com/api/v1/study/:studyId/access/:userAccessId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyAccessDeleteParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}, "userAccessId": {"type": "string"}},
    "required": ["studyId", "userAccessId"]
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



        Deletes a study access for a user.  The study access must be locally created or an error will be returned
        

### HTTP Request

`DELETE /study/:studyId/access/:userAccessId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A

## SaveStudyUserAccess - <em>Save Study User Access</em>


```shell
curl -X POST "https://ctoregistry.com/api/v1/study/:studyId/access"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyAccessParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}},
    "required": ["studyId"]
  },
  "body": {
    "id": "/StudyAccessBody",
    "type": "object",
    "properties": {
      "userAccessId": {"type": "string"},
      "userId": {"type": "string"},
      "roleName": {"type": "string"},
      "roleCode": {"type": "string", "enum": ["readOnly"]}
    },
    "required": ["userId", "roleCode"]
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



        Updates or creates a study access for a user
        

### HTTP Request

`POST /study/:studyId/access`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A

## StudyAccess - <em>Get Study Access</em>


```shell
curl "https://ctoregistry.com/api/v1/study/:studyId/access"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}},
    "required": ["studyId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyAccessResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/StudyAccess",
        "properties": {
          "id": {"type": ["object", "null"]},
          "firstName": {"type": "string"},
          "lastName": {"type": "string"},
          "userId": {"type": "object"},
          "email": {"type": "string"},
          "roleName": {"type": "string"},
          "roleCode": {"type": "string", "enum": ["readOnly"]},
          "source": {"type": "string", "enum": ["stream", "local", "system"]},
          "status": {"type": "string", "enum": ["active", "deleted"]},
          "deletedDt": {"type": "date"},
          "institutionId": {"type": "object"},
          "institutionName": {"type": "string"},
          "updateDt": {"type": "date"},
          "createDt": {"type": "date"}
        },
        "required": [
          "id",
          "firstName",
          "lastName",
          "userId",
          "email",
          "source",
          "status",
          "updateDt",
          "createDt"
        ]
      }
    }
  },
  "required": ["data"]
}
```



        Gets the list of users that can access the study.
        

### HTTP Request

`GET /study/:studyId/access`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A

## StudyForms - <em>Get Study Forms</em>


```shell
curl "https://ctoregistry.com/api/v1/study/:studyId/forms"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}},
    "required": ["studyId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyFormsResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "properties": {
          "formCode": {"type": "string"},
          "formName": {"type": "string"},
          "formNameUnmapped": {"type": "string"},
          "reviewReferences": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "reviewReference": {"type": "string"},
                "reviewStatus": {"type": "string"}
              },
              "required": ["reviewReference"]
            }
          },
          "parentFormIdNumber": {"type": "number"},
          "formIdNumber": {"type": "number"},
          "initialSubmitDt": {"type": "date"},
          "initialApprovalDt": {"type": "date"},
          "initialReviewDt": {"type": "date"},
          "initialReviewType": {
            "type": "string",
            "enum": ["Full Board Review", "Delegated Review", "Admin Review"]
          },
          "hasFees": {"type": ["boolean", "null"]},
          "centre": {"type": ["string", "null"]},
          "centreStatus": {
            "type": ["string", "null"],
            "enum": [
              "Active",
              "Completed",
              "Expired",
              "None",
              "Not Approved",
              "Pending",
              "Suspended",
              "Terminated",
              "Withdrawn"
            ]
          },
          "events": {
            "type": "array",
            "items": {
              "id": "/StudyFormEvent",
              "properties": {
                "reviewReference": {"type": "string"},
                "centre": {"type": ["string", "null"]},
                "event": {"type": "string"},
                "eventUnmapped": {"type": "string"},
                "eventDt": {"type": "date"}
              },
              "required": ["event", "eventUnmapped", "eventDt"]
            }
          }
        },
        "required": [
          "formCode",
          "formName",
          "formNameUnmapped",
          "formIdNumber",
          "reviewReferences",
          "events"
        ]
      }
    }
  },
  "required": ["data"]
}
```



        Gets the raw forms data that has been recorded for the study and event history for each form type
        

### HTTP Request

`GET /study/:studyId/forms`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
committee | member | study|N/A
institution | admin | study|Study has a participating site application for the target institution of the privilege.                        Study where the lead applicant institution matches the target institution, and the study has been approved by the BoR

## StudyList - <em>Get Studies</em>


```shell
curl "https://ctoregistry.com/api/v1/study/"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/StudyListQuery",
    "type": "object",
    "properties": {
      "offset": {"type": "integer", "minimum": 0, "default": 0},
      "limit": {"type": "integer", "minimum": 0, "default": 20},
      "sortby": {"type": "string"},
      "order": {"type": "string"},
      "search": {"type": "string"},
      "status": {"type": ["string", "array"]},
      "csv": {"type": "boolean"},
      "centreInstitutionIds": {
        "type": ["string", "array"],
        "description": "an array of centre institution IDs"
      },
      "institutionIds": {
        "type": ["string", "array"],
        "description": "an array of sponsor institution IDs"
      },
      "committeeIds": {"type": ["string", "array"], "description": "an array of committee IDs"},
      "studyType": {
        "type": ["string", "array"],
        "description": "an array of types",
        "items": {"enum": ["canReview", "quickStart"]}
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/StudyListResponse",
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
        "id": "/Study",
        "type": "object",
        "properties": {
          "id": {"type": "object"},
          "isInvestigatorInitiatedStudy": {"type": "boolean"},
          "sponsor": {
            "type": ["string", "null"],
            "description": "@Deprecated: Use studySponsor.name instead."
          },
          "studySponsor": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": ["string", "null"]}},
            "required": ["name"]
          },
          "ohrp": {"type": "boolean"},
          "fda": {"type": "boolean"},
          "observational": {"type": "boolean"},
          "provincialStatus": {
            "type": "string",
            "enum": [
              "Active",
              "Completed",
              "Expired",
              "None",
              "Not Approved",
              "Pending",
              "Suspended",
              "Terminated",
              "Withdrawn"
            ]
          },
          "expiryDt": {"type": ["date", "null"]},
          "studyDisplayName": {"type": ["string", "number"]},
          "shortTitle": {"type": "string"},
          "studyIdentifier": {"type": ["string", "null"]},
          "title": {"type": ["string", "null"]},
          "reviewerLink": {"type": "string"},
          "applicantLink": {"type": "string"},
          "reb": {
            "type": "object",
            "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
            "required": ["name"]
          },
          "projectIdNumber": {"type": "number"},
          "roles": {
            "type": "array",
            "description": "The users roles on the study, only set when returned as part of the user studies route.",
            "items": {
              "id": "/StudyAccess",
              "properties": {
                "id": {"type": ["object", "null"]},
                "firstName": {"type": "string"},
                "lastName": {"type": "string"},
                "userId": {"type": "object"},
                "email": {"type": "string"},
                "roleName": {"type": "string"},
                "roleCode": {"type": "string", "enum": ["readOnly"]},
                "source": {"type": "string", "enum": ["stream", "local", "system"]},
                "status": {"type": "string", "enum": ["active", "deleted"]},
                "deletedDt": {"type": "date"},
                "institutionId": {"type": "object"},
                "institutionName": {"type": "string"},
                "updateDt": {"type": "date"},
                "createDt": {"type": "date"}
              },
              "required": [
                "id",
                "firstName",
                "lastName",
                "userId",
                "email",
                "source",
                "status",
                "updateDt",
                "createDt"
              ]
            }
          },
          "createDt": {"type": "date"},
          "updateDt": {"type": "date"}
        },
        "required": [
          "id",
          "isInvestigatorInitiatedStudy",
          "ohrp",
          "fda",
          "observational",
          "provincialStatus",
          "expiryDt",
          "studyDisplayName",
          "shortTitle",
          "title",
          "reviewerLink",
          "applicantLink",
          "reb",
          "projectIdNumber",
          "createDt",
          "updateDt"
        ]
      }
    }
  }
}
```



        Gets a list of all the studies in the system that the currently authenticated user can access. 
        Uses list pagination to limit the results.
        

### HTTP Request

`GET /study/`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
institution | member | N/A|User has a collaborator role for the target study.
institution | admin | N/A|Study has a participating site application for the target institution of the privilege.                        Study where the lead applicant institution matches the target institution, and the study has been approved by the BoR
committee | member | N/A|Study REB is set to the target of the privilege.

## StudyProfile - <em>Get Study</em>


```shell
curl "https://ctoregistry.com/api/v1/study/:studyId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/StudyParams",
    "type": "object",
    "properties": {"studyId": {"type": "string"}},
    "required": ["studyId"]
  }
}
```


> Response Schema

```json
{
  "id": "/StudyProfileResponse",
  "type": "object",
  "properties": {
    "study": {
      "id": "/StudyFull",
      "type": "object",
      "properties": {
        "id": {"type": "object"},
        "isInvestigatorInitiatedStudy": {"type": "boolean"},
        "sponsor": {
          "type": ["string", "null"],
          "description": "@Deprecated: Use studySponsor.name instead."
        },
        "studySponsor": {
          "type": "object",
          "properties": {
            "id": {"type": "object"},
            "name": {"type": ["string", "null"]},
            "contact": {
              "properties": {
                "userId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]}
              },
              "required": ["firstName", "lastName", "email"]
            }
          },
          "required": ["name"]
        },
        "studyCro": {
          "type": "object",
          "properties": {
            "id": {"type": "object"},
            "name": {"type": ["string", "null"]},
            "contact": {
              "properties": {
                "userId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]}
              },
              "required": ["firstName", "lastName", "email"]
            }
          },
          "required": ["name", "contact"]
        },
        "approvedSharedQuestionsReviewReference": {"type": "string"},
        "ctaita": {"type": "boolean"},
        "ctaitaTypes": {
          "type": "array",
          "items": {"type": "string", "enum": ["ctaFda", "ctaNhp", "itaMedDevices"]},
          "description": "Dictionary: Clinical Trial CTA/ITA Types"
        },
        "phi": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "address",
              "admissionDate",
              "age",
              "deviceIdentifier",
              "dischargeDate",
              "driversLicense",
              "email",
              "email2",
              "family",
              "fax",
              "postalFirst3",
              "dateOfBirth",
              "dateOfDeath",
              "photo",
              "initials",
              "fullName",
              "postal",
              "healthCardNumber",
              "ipAddress",
              "medicalDeviceIdentifier",
              "medicalRecordNumber",
              "none",
              "other",
              "otherInformation",
              "dateOfBirthPartial",
              "dateOfDeathPartial",
              "initialsPartial",
              "specimenNumber",
              "race",
              "sexGender",
              "sex",
              "sin",
              "phone",
              "voice"
            ]
          },
          "description": "Dictionary: Clinical Trial PHI Types"
        },
        "waiverOfConsent": {"type": "boolean"},
        "waiverOfConsentType": {
          "type": "string",
          "enum": ["all", "some", "someSDM"],
          "description": "Dictionary: Clinical Trial Waiver of Consent Types"
        },
        "waiverOfConsentDesc": {"type": ["string", "null"]},
        "informedConsent": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "thirdParty",
              "deferred",
              "waiver",
              "waiverObs",
              "previousObs",
              "incapacitated"
            ]
          },
          "description": "Dictionary: Clinical Trial Informed Consent Types"
        },
        "withdrawData": {"type": "boolean"},
        "studyDataSource": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "medicalCharts",
              "directCollection",
              "ices",
              "biospecimens",
              "registry",
              "existingDataset",
              "observation",
              "other"
            ]
          },
          "description": "Dictionary: Clinical Trial Study Data Source Types"
        },
        "ohrp": {"type": "boolean"},
        "fda": {"type": "boolean"},
        "observational": {"type": "boolean"},
        "provincialStatus": {
          "type": "string",
          "enum": [
            "Active",
            "Completed",
            "Expired",
            "None",
            "Not Approved",
            "Pending",
            "Suspended",
            "Terminated",
            "Withdrawn"
          ]
        },
        "expiryDt": {"type": ["date", "null"]},
        "studyDisplayName": {"type": ["string", "number"]},
        "studyIdentifier": {"type": ["string", "null"]},
        "shortTitle": {"type": "string"},
        "studyAcronym": {"type": "string"},
        "title": {"type": ["string", "null"]},
        "reviewerLink": {"type": "string"},
        "applicantLink": {"type": "string"},
        "reb": {
          "type": "object",
          "properties": {"id": {"type": "object"}, "name": {"type": "string"}},
          "required": ["name"]
        },
        "projectIdNumber": {"type": "number"},
        "createDt": {"type": "date"},
        "updateDt": {"type": "date"},
        "initialSubmitDt": {"type": "date"},
        "rebAcceptDt": {"type": "date"},
        "initialApprovalDt": {"type": "date"},
        "initialReviewDt": {"type": "date"},
        "initialReviewType": {
          "type": ["string"],
          "enum": ["Full Board Review", "Delegated Review", "Admin Review"]
        },
        "summary": {"type": ["string", "null"]},
        "interventions": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["drugs", "health", "devices", "specimen", "radiation", "surveys", "other"]
          },
          "description": "Dictionary: Clinical Trial Interventions"
        },
        "funding": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "charity",
              "government",
              "governmentFundingAgency",
              "grantingAgency",
              "industry",
              "internal",
              "none",
              "other",
              "usFederalFunds",
              "triCouncil"
            ]
          },
          "description": "Dictionary: Clinical Trial Funding Types"
        },
        "fundingOther": {"type": "string"},
        "mta": {"type": "boolean"},
        "overallSampleSize": {"type": ["string", "null"]},
        "populations": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "patients",
              "healthyVolunteers",
              "students",
              "staff",
              "mentalHealth",
              "institutionalized",
              "prisoners",
              "poverty",
              "educationalDisadvantaged",
              "illiterate",
              "children",
              "emergency",
              "lackConsentCapacity",
              "cognitivelyImpaired",
              "physicalDisabilities",
              "speechImpaired",
              "lackConsentTemporary",
              "pregnant",
              "elderly",
              "palliativeCare",
              "longTermCare",
              "minorities",
              "other"
            ]
          },
          "description": "Dictionary: Clinical Trial Populations"
        },
        "populationsOther": {"type": "string"},
        "phase": {"type": "string"},
        "phaseOther": {"type": "string"},
        "dsmb": {"type": "boolean"},
        "ctaApproved": {"type": "boolean"},
        "ctaInvestigational": {"type": "boolean"},
        "recruitmentMaterials": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "referral",
              "referralObs",
              "communityPartner",
              "advertisements",
              "recruitmentDatabase",
              "thirdParty",
              "website",
              "socialMedia",
              "video",
              "surveyPanel",
              "snowball",
              "investigator",
              "other"
            ],
            "description": "Dictionary: Clinical Trial Recruitment Materials"
          }
        },
        "recruitmentMaterialsOther": {"type": ["string", "null"]},
        "initialContact": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "telephone",
              "email",
              "inPerson",
              "letter",
              "participantContact",
              "notReady",
              "other"
            ],
            "description": "Dictionary: Clinical Trial Initial Contact Types"
          }
        },
        "initialContactOther": {"type": ["string", "null"]},
        "informedConsentDiscussion": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["inPerson", "remote", "noDiscussion", "noDiscussionObs"],
            "description": "Dictionary: Clinical Trial Informed Consent Discussion Types"
          }
        },
        "informedConsentDiscussionJustify": {"type": ["string", "null"]},
        "informedConsentDocumentation": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["written", "verbally", "implied", "other"],
            "description": "Dictionary: Clinical Trial Informed Consent Documentation Types"
          }
        },
        "informedConsentDocumentationJustify": {"type": ["string", "null"]},
        "centralEConsentPlatform": {"type": "boolean"},
        "medicalEmergencySDMInformedConsent": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["inPerson", "remote", "noDiscussion", "noDiscussionObs"],
            "description": "Dictionary: Clinical Trial Informed Consent Discussion Types"
          }
        },
        "medicalEmergencySDMInformedConsentJustify": {"type": ["string", "null"]},
        "medicalEmergencyInformedConsentDocumentation": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["written", "verbally", "implied", "other"],
            "description": "Dictionary: Clinical Trial Informed Consent Documentation Types"
          }
        },
        "medicalEmergencyInformedConsentDocumentationOther": {"type": ["string", "null"]},
        "medicalEmergencyParticipantInformedConsent": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["inPerson", "remote", "noDiscussion", "noDiscussionObs"],
            "description": "Dictionary: Clinical Trial Informed Consent Discussion Types"
          }
        },
        "medicalEmergencyParticipantInformedConsentJustify": {"type": ["string", "null"]},
        "medicalEmergencyParticipantInformedConsentDocumentation": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["written", "verbally", "implied", "other"],
            "description": "Dictionary: Clinical Trial Informed Consent Documentation Types"
          }
        },
        "medicalEmergencyParticipantInformedConsentDocumentationOther": {
          "type": ["string", "null"]
        },
        "participantsLoseCapacity": {"type": "boolean"},
        "informedConsentAssentDebriefing": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": ["consentForms", "assentForms", "debriefingMaterials", "other"],
            "description": "Dictionary: Clinical Trial Informed Consent Assent Debriefing Types"
          }
        },
        "secondaryUseInformedConsent": {
          "type": "array",
          "items": {
            "type": "string",
            "enum": [
              "thirdParty",
              "deferred",
              "waiver",
              "waiverObs",
              "previousObs",
              "incapacitated"
            ],
            "description": "Dictionary: Clinical Trial Informed Consent Types"
          }
        },
        "futureUseBroadConsent": {"type": "boolean"},
        "provincialApplication": {
          "type": "object",
          "properties": {
            "studyContact": {
              "id": "/StudyUser",
              "properties": {
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]},
                "organization": {"type": ["string", "null"]},
                "institutionId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "user": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object"},
                    "firstName": {"type": "string"},
                    "lastName": {"type": "string"},
                    "title": {
                      "type": "string",
                      "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                    }
                  },
                  "required": ["id", "firstName", "lastName"]
                }
              },
              "required": ["firstName", "lastName"]
            },
            "projectOwner": {
              "id": "/StudyUser",
              "properties": {
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]},
                "organization": {"type": ["string", "null"]},
                "institutionId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "user": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object"},
                    "firstName": {"type": "string"},
                    "lastName": {"type": "string"},
                    "title": {
                      "type": "string",
                      "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                    }
                  },
                  "required": ["id", "firstName", "lastName"]
                }
              },
              "required": ["firstName", "lastName"]
            },
            "provincialApplicant": {
              "id": "/StudyUser",
              "properties": {
                "email": {"type": ["string", "null"]},
                "phone": {"type": ["string", "null"]},
                "organization": {"type": ["string", "null"]},
                "institutionId": {"type": ["object", "null"]},
                "firstName": {"type": ["string", "null"]},
                "lastName": {"type": ["string", "null"]},
                "user": {
                  "type": "object",
                  "properties": {
                    "id": {"type": "object"},
                    "firstName": {"type": "string"},
                    "lastName": {"type": "string"},
                    "title": {
                      "type": "string",
                      "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                    }
                  },
                  "required": ["id", "firstName", "lastName"]
                }
              },
              "required": ["firstName", "lastName"]
            }
          }
        },
        "centreApplications": {
          "type": "array",
          "items": {
            "type": "object",
            "id": "/CentreApplication",
            "properties": {
              "institutionId": {
                "type": "object",
                "description": "The document Id of the institution.  This may be empty due to a data linking issue."
              },
              "name": {"type": "string"},
              "status": {
                "type": ["string", "null"],
                "enum": [
                  "Active",
                  "Completed",
                  "Expired",
                  "None",
                  "Not Approved",
                  "Pending",
                  "Suspended",
                  "Terminated",
                  "Withdrawn"
                ]
              },
              "startDate": {
                "type": "string",
                "description": "The textual start date for the centre"
              },
              "principalInvestigator": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]},
                  "organization": {"type": ["string", "null"]},
                  "institutionId": {"type": ["object", "null"]},
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object"},
                      "firstName": {"type": "string"},
                      "lastName": {"type": "string"},
                      "title": {
                        "type": "string",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "coInvestigator": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]},
                  "organization": {"type": ["string", "null"]},
                  "institutionId": {"type": ["object", "null"]},
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object"},
                      "firstName": {"type": "string"},
                      "lastName": {"type": "string"},
                      "title": {
                        "type": "string",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "studyContact": {
                "id": "/StudyUser",
                "properties": {
                  "email": {"type": ["string", "null"]},
                  "phone": {"type": ["string", "null"]},
                  "organization": {"type": ["string", "null"]},
                  "institutionId": {"type": ["object", "null"]},
                  "firstName": {"type": ["string", "null"]},
                  "lastName": {"type": ["string", "null"]},
                  "user": {
                    "type": "object",
                    "properties": {
                      "id": {"type": "object"},
                      "firstName": {"type": "string"},
                      "lastName": {"type": "string"},
                      "title": {
                        "type": "string",
                        "enum": ["Dr.", "Prof.", "Miss", "Mrs.", "Ms.", "Mr.", "Mx"]
                      }
                    },
                    "required": ["id", "firstName", "lastName"]
                  }
                },
                "required": ["firstName", "lastName"]
              },
              "centreSampleSize": {
                "type": "string",
                "description": "Textual description of the planned centre sample size"
              },
              "initialSubmitDt": {"type": "date"},
              "initialApprovalDt": {"type": "date"},
              "initialReviewDt": {"type": "date"},
              "initialReviewType": {
                "type": "string",
                "enum": ["Full Board Review", "Delegated Review", "Admin Review"]
              },
              "formIdNumber": {"type": "number"}
            },
            "required": ["name", "status"]
          }
        }
      },
      "required": [
        "id",
        "isInvestigatorInitiatedStudy",
        "sponsor",
        "studyDisplayName",
        "ohrp",
        "fda",
        "observational",
        "provincialStatus",
        "expiryDt",
        "shortTitle",
        "title",
        "reviewerLink",
        "applicantLink",
        "reb",
        "projectIdNumber",
        "createDt",
        "updateDt",
        "summary",
        "interventions",
        "funding",
        "mta",
        "overallSampleSize",
        "populations",
        "dsmb",
        "ctaApproved",
        "ctaInvestigational"
      ]
    }
  }
}
```



        Gets the data record of one study.  Some sections of the data will only be available depending on the authenticated users privileges and participation.
        Refer to the restrictions listed for each authorization privilege.
        

### HTTP Request

`GET /study/:studyId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | * | N/A|N/A
study | applicant | study|Study data is filtered to only contain participating site applications for the target institution.
committee | member | study|N/A
institution | admin | study|Study data is filtered to only contain participating site applications for the target institution.                        Study where the lead applicant institution matches the target institution, and the study has been approved by the BoR