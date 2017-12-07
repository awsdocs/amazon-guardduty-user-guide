# GetFindingsStatistics<a name="get-findings-statistics"></a>

Lists Amazon GuardDuty findings' statistics for the specified detector ID\.

## Request Syntax<a name="get-findings-statistics-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/statistics
```

**Body:**

```
{
    "findingCriteria": {
        "criterion": {
            "<field>": {
                "gt": "integer",
                "gte": "integer",
                "lt": "integer",
                "lte": "integer",
                "eq": [
                    "string"
                ],
                "neq": [
                    "string"
                ]
            }
        }
    }
    "findingStatisticTypes": {
		"findingStatisticType": "[COUNT_BY_SEVERITY]"
	}
    
}
```

## Request Parameters<a name="get-findings-statistics-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The ID of the detector that specifies the GuardDuty service whose findings' statistics you want to get\.  
Required: Yes

**findingCriteria**  
Represents the criteria used for querying findings\.   
Type: FindingCriteria  
Required: No    
**gt**  
Represents the 'greater than' condition to be applied to a single field when querying for findings\.  
Required: No  
**gte**  
Represents the 'greater than equal' condition to be applied to a single field when querying for findings\.  
Required: No  
**lt**  
Represents the 'less than' condition to be applied to a single field when querying for findings\.  
Required: No  
**lte**  
Represents the 'less than equal' condition to be applied to a single field when querying for findings\.  
Required: No  
**eq**  
Represents the 'equal to' condition to be applied to a single field when querying for findings\.  
Required: No  
**neq**  
Represents the 'not equal to' condition to be applied to a single field when querying for findings\.  
Required: No

**findingStatisticTypes**  
The list of the finding statistics\.  
Required: Yes  
Type: Array of strings\. Minimum items 1, maximum items 10\.    
**FindingStatisticType**  
The types of finding statistics\.  
Type: String\. Valid values: \[COUNT\_BY\_SEVERITY\]

## Response Syntax<a name="get-findings-statistics-response-syntax"></a>

```
{
    "findingStatistics": [
        {
            "countBySeverity": "integer",
        }
    ]
}
```

## Response Elements<a name="get-findings-statistics-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**findingStatistics**  
Represents a map of severity/count statistic for a set of findings\.  
Type: Integer

## Errors<a name="get-findings-statistics-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information

**InvalidInputException**

The request is rejected because an invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because one or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter detectorId has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request was rejected because the parameter findingCriteria has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because of invalid finding statistic type is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 