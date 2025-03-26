
# Metrics


## CommitteeReviewReport - <em>Review Report for one Committee</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/committee/:committeeId/review-report"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/MetricsCommitteeReviewQuery",
    "type": "object",
    "properties": {
      "csv": {
        "type": "boolean",
        "description": "Return the report as CSV content instead of the default JSON"
      },
      "startDt": {"type": "string", "format": "date-time"},
      "endDt": {"type": "string", "format": "date-time"},
      "delegatedOnly": {"type": "boolean"}
    },
    "required": ["startDt", "endDt"]
  },
  "params": {
    "id": "/MetricsCommitteeReviewParams",
    "properties": {
      "committeeId": {"type": "string", "description": "The committee ID to get the report for"}
    },
    "required": ["committeeId"]
  }
}
```


> Response Schema

```json
{
  "id": "/MetricsCommitteeReviewResponse",
  "type": "object",
  "properties": {
    "data": {
      "type": "array",
      "items": {
        "id": "/MetricsCommitteeReviewData",
        "type": "object",
        "properties": {
          "committeeName": {"type": "string"},
          "committeeId": {"type": "object"},
          "applicationType": {"type": "string"},
          "studyId": {"type": "object"},
          "projectIdNumber": {"type": "number"},
          "shortTitle": {"type": "string"},
          "studyIdentifier": {"type": ["string", "null"]},
          "centre": {"type": "string"},
          "reviewReference": {"type": "string"},
          "assignedReviewer": {"type": "string"},
          "reviewStatus": {"type": "string"},
          "approvalStatus": {"type": "string"},
          "approvalStatusDt": {"type": "date"},
          "delegatedOnly": {"type": "boolean"},
          "title": {"type": "string"}
        },
        "required": [
          "committeeName",
          "committeeId",
          "applicationType",
          "studyId",
          "projectIdNumber",
          "shortTitle",
          "centre",
          "reviewReference",
          "reviewStatus",
          "approvalStatus",
          "approvalStatusDt",
          "delegatedOnly",
          "title"
        ]
      }
    }
  },
  "required": ["data"]
}
```


Gets a report of all studies that had a specified review action in the time period for the specified committee

### HTTP Request

`GET /metrics/committee/:committeeId/review-report`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
committee | admin | committee|N/A

## FundingMasterReport - <em>Funding Master Report</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/funding/master"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/MetricsFundingMasterQuery",
    "type": "object",
    "properties": {
      "includeCommitteeIds": {
        "type": ["string", "array"],
        "description": "an array of committee IDs to include"
      },
      "excludeCommitteeIds": {
        "type": ["string", "array"],
        "description": "an array of committee IDs to exclude"
      },
      "csv": {
        "type": "string",
        "description": "Return the report as CSV content instead of the default JSON"
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/MetricsFundingMasterResponse",
  "type": "object",
  "properties": {
    "totals": {
      "id": "/MetricsFundingMasterTotals",
      "type": "object",
      "properties": {
        "subTotal": {"type": "number"},
        "subTotalReceived": {"type": ["number", "string"]},
        "subTotalDifference": {"type": "number"},
        "hst": {"type": "number"},
        "hstReceived": {"type": "number"},
        "hstDifference": {"type": "number"},
        "rebPaymentAmountDue": {"type": ["number", "string"]},
        "rebPaymentAmountSent": {"type": ["number", "string"]},
        "rebPaymentAmountDifference": {"type": "number"},
        "sitePaymentAmountDue": {"type": ["number", "string"]},
        "sitePaymentAmountSent": {"type": ["number", "string"]},
        "sitePaymentAmountDifference": {"type": "number"}
      },
      "required": [
        "subTotal",
        "subTotalReceived",
        "subTotalDifference",
        "hst",
        "hstReceived",
        "hstDifference",
        "rebPaymentAmountDue",
        "rebPaymentAmountSent",
        "rebPaymentAmountDifference",
        "sitePaymentAmountDue",
        "sitePaymentAmountSent",
        "sitePaymentAmountDifference"
      ]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "/MetricsFundingMasterData",
        "type": "object",
        "properties": {
          "projectIdNumber": {"type": "number"},
          "studyId": {"type": "object"},
          "studyFundingId": {"type": "object"},
          "committeeName": {"type": "string"},
          "committeeId": {"type": "object"},
          "applicationType": {"type": "string"},
          "centreName": {"type": "string"},
          "institutionId": {"type": ["null", "object"]},
          "invoiceDt": {"type": "date"},
          "invoiceLastSentDt": {"type": ["date", "null"]},
          "invoiceLastPaymentDt": {"type": ["date", "null"]},
          "invoiceNumber": {"type": "string"},
          "invoiceShortNumber": {"type": "integer"},
          "invoiceId": {"type": "object"},
          "subTotal": {"type": ["number", "string"]},
          "subTotalReceived": {"type": ["number", "string"]},
          "subTotalDifference": {"type": ["number", "string"]},
          "taxExempt": {"type": "string", "description": "boolean (true/false) changed to Y/N"},
          "hst": {"type": ["number", "string"]},
          "hstReceived": {"type": ["number", "string"]},
          "hstDifference": {"type": ["number", "string"]},
          "rebPaymentDt": {"type": ["date", "null"]},
          "rebPaymentAmountDue": {"type": ["number", "string"]},
          "rebPaymentAmountSent": {"type": ["number", "string"]},
          "rebPaymentAmountDifference": {"type": ["number", "string"]},
          "sitePaymentDt": {"type": ["date", "null"]},
          "sitePaymentAmountDue": {"type": ["number", "string"]},
          "sitePaymentAmountSent": {"type": ["number", "string"]},
          "sitePaymentAmountDifference": {"type": ["number", "string"]}
        },
        "required": [
          "projectIdNumber",
          "studyId",
          "studyFundingId",
          "committeeName",
          "applicationType",
          "centreName",
          "invoiceNumber",
          "invoiceShortNumber",
          "invoiceId",
          "invoiceDt",
          "subTotal",
          "subTotalReceived",
          "subTotalDifference",
          "taxExempt",
          "hst",
          "hstReceived",
          "hstDifference"
        ]
      }
    }
  },
  "required": ["totals", "data"]
}
```


Gets the report that includes totals for funding invoices and payments

### HTTP Request

`GET /metrics/funding/master`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | funding | N/A|N/A
system | support | N/A|N/A

## MetricsCommitteeShare - <em>Committee Share Metrics</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/committee/share"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/MetricsCommitteeShareQuery",
    "type": "object",
    "properties": {
      "excludeCommitteeIds": {
        "type": ["string", "array"],
        "description": "an array of committee IDs to exclude"
      },
      "csv": {
        "type": "string",
        "description": "Return the report as CSV content instead of the default JSON"
      }
    }
  }
}
```


> Response Schema

```json
{
  "id": "/MetricsCommitteeShareResponse",
  "type": "object",
  "properties": {
    "totals": {
      "id": "/MetricsCommitteeShareTotals",
      "type": "object",
      "properties": {
        "studyCount": {"type": "integer"},
        "studyCountFunded": {"type": "integer"},
        "centreCount": {"type": "integer"},
        "centreCountFunded": {"type": "integer"}
      },
      "required": ["studyCount", "studyCountFunded", "centreCount", "centreCountFunded"]
    },
    "data": {
      "type": "array",
      "items": {
        "id": "/MetricsCommitteeShareData",
        "type": "object",
        "properties": {
          "committeeId": {"type": "object"},
          "committeeName": {"type": "string"},
          "studyCount": {"type": "integer"},
          "studyCountFunded": {"type": "integer"},
          "centreCount": {"type": "integer"},
          "centreCountFunded": {"type": "integer"},
          "shareOfStudies": {"type": "string"},
          "shareOfCentres": {"type": "string"},
          "joinedVsReviewedPercentDiff": {"type": "string"}
        },
        "required": [
          "committeeId",
          "committeeName",
          "studyCount",
          "studyCountFunded",
          "centreCount",
          "centreCountFunded",
          "shareOfStudies",
          "shareOfCentres",
          "joinedVsReviewedPercentDiff"
        ]
      }
    }
  },
  "required": ["totals", "data"]
}
```


Gets the share metrics report used to determine Committee assigned and for overall review of studies reviewed by board.

### HTTP Request

`GET /metrics/committee/share`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A

## MetricsStudyReview - <em>Study review metrics</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/study-review"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "query": {
    "id": "/MetricsStudyReviewQuery",
    "properties": {
      "isProvincial": {
        "type": "boolean",
        "description": "If true, reports on PIA and OPIA, if false, reports on CIA and OCIA"
      },
      "startDt": {"type": "string", "format": "date-time"},
      "endDt": {"type": "string", "format": "date-time"},
      "committeeIds": {
        "type": ["string", "array"],
        "description": "list of committeeIds to filter by"
      },
      "includeRelatedCommittees": {
        "type": "boolean",
        "description": "if true, finds related committees using the parent committee Id"
      },
      "studyIds": {"type": ["string", "array"], "description": "list of study Ids to filter by"},
      "csv": {
        "type": "boolean",
        "description": "if true, returns the report as a CSV file for download, if false returns the json data"
      },
      "csvType": {
        "type": "string",
        "enum": ["totals", "data", "all"],
        "description": "controls how the CSV  report will be output, defaults to all"
      }
    },
    "required": []
  }
}
```


> Response Schema

```json
{
  "id": "/MetricsStudyReviewResponse",
  "properties": {
    "totals": {
      "properties": {
        "screeningTimeTotal": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "screeningTimeCTO": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "screeningTimeStudyTeam": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "screeningTimeREB": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "notFullBoardCount": {
          "properties": {
            "all": {"type": "number"},
            "ct": {"type": "number"},
            "obs": {"type": "number"}
          }
        },
        "pendingBoRTime": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "reviewTimeStudyTeam": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "reviewTimeREB": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "reviewTimeTotal": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "applicationIncompleteCount": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "sendReviewLetterCount": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        },
        "submissionCount": {
          "properties": {
            "all": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "ct": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "obs": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "fb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            },
            "nfb": {
              "properties": {
                "count": {"type": "number"},
                "avg": {"type": "number"},
                "med": {"type": "number"},
                "high": {"type": "number"},
                "low": {"type": "number"}
              }
            }
          }
        }
      }
    },
    "data": {
      "type": "array",
      "items": {
        "id": "",
        "properties": {
          "projectIdNumber": {"type": "number"},
          "applicationType": {"type": "string"},
          "formCode": {"type": "string"},
          "reb": {"type": "string"},
          "hasFullBoardReview": {"type": "boolean"},
          "firstReviewType": {"type": "string"},
          "centre": {"type": "string"},
          "applicationIncompleteCount": {"type": "number"},
          "sendReviewLetterCount": {"type": "number"},
          "submissionCount": {"type": "number"},
          "isInvestigatorInitiated": {"type": "boolean"},
          "hasFees": {"type": "string"},
          "dates": {
            "submitDt": {"type": "string", "format": "date"},
            "assignBoRDt": {"type": "string", "format": "date"},
            "acceptBoRDt": {"type": "string", "format": "date"},
            "firstReviewDt": {"type": "string", "format": "date"},
            "completeDt": {"type": "string", "format": "date"},
            "approvalDt": {"type": "string", "format": "date"}
          },
          "times": {
            "screeningTimeTotal": {"type": "number", "description": "in days"},
            "screeningTimeCTO": {"type": "number", "description": "in days"},
            "screeningTimeREB": {"type": "number", "description": "in days"},
            "pendingBoRTime": {"type": "number", "description": "in days"},
            "screeningTimeStudyTeam": {"type": "number", "description": "in days"},
            "reviewTimeTotal": {"type": "number", "description": "in days"},
            "reviewTimeREB": {"type": "number", "description": "in days"},
            "reviewTimeStudyTeam": {"type": "number", "description": "in days"}
          }
        },
        "required": []
      }
    }
  },
  "required": ["totals", "data"]
}
```


Gets a report of study review times and counts of events, includes totals in the output

### HTTP Request

`GET /metrics/study-review`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A

## QuickStartSiteReport - <em>QuickSTART Site Report</em>


```shell
curl "https://ctoregistry.com/api/v1/metrics/quick-start/:quickStartId/sites/:institutionId"  
  -H "Authorization: {{_JWT_TOKEN_}}"  
  -H "Content-Type: application/json"
```

> Request Schema

```json
{
  "params": {
    "id": "/QuickStartSiteParams",
    "type": "object",
    "properties": {"quickStartId": {"type": "string"}, "institutionId": {"type": "string"}},
    "required": ["quickStartId", "institutionId"]
  }
}
```


> Response Schema

```json
undefined
```


gets the Excel report for one QuickSTART site

### HTTP Request

`GET /metrics/quick-start/:quickStartId/sites/:institutionId`



### Authorization
 
    
 Scope      | Role       | Auth Source | Restrictions
------------|------------|-------------|----------------
system | admin | N/A|N/A
system | support | N/A|N/A
system | quickStartAdmin | N/A|N/A