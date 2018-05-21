# GetFilter<a name="get-filter"></a>

Returns the details of the filter specified by the filter name\.

## Request Syntax<a name="get-filter-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/filter/<filterName>
```

## Path Parameters<a name="get-filger-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service where you want to list the details of the specified filter\.  
Type: String  
Required: Yes

**filterName**  
The name of the filter whose details you want to get\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-filter-response-syntax"></a>

```
{
        "name": "string",
        "description": "string",
        "findingCriteria":  [
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
        ],
        "action": "[NOOP|ARCHIVE]",
        "rank": "integer"    
}
```

## Response Elements<a name="get-filter-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**filter**  
The returned details of the filter\.    
**name**  
The name of the filter\.  
Type: String  
**description**  
The description of the filter\.  
Type: String  
**findingCriteria**  
Represents the criteria to be used in the filter for querying findings\.   
Type: FindingCriteria  
Required: No  
You can only use the following attributes to query findings:   
+ accountId
+ id 
+ region 
+ resource\.instanceDetails\.instanceId 
+ resource\.resourceType 
+ service\.archived 
**Note**  
When this attribute is set to TRUE, only archived findings are listed\. When it's set to FALSE, only unarchived findings are listed\. When this attribute is not set, all existing findings are listed\.
+ service\.action\.networkConnectionAction\.blocked 
+ service\.action\.networkConnectionAction\.connectionDirection 
+ service\.action\.networkConnectionAction\.localPortDetails\.port 
+ service\.action\.networkConnectionAction\.protocol 
+ service\.action\.networkConnectionAction\.remoteIpDetails\.ipAddressV4 
+ service\.action\.networkConnectionAction\.remotePortDetails\.port 
+ service\.action\.actionType 
+ service\.additionalInfo\.threatListName 
+ severity
+ type
+ updatedAt

  Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.  
**Gt**  
Represents the "greater than" condition to be applied to a single field when querying for findings\.  
Required: No  
**Gte**  
Represents the "greater than equal" condition to be applied to a single field when querying for findings\.  
Required: No  
**Lt**  
Represents the "less than" condition to be applied to a single field when querying for findings\.  
Required: No  
**Lte**  
Represents the "less than equal" condition to be applied to a single field when querying for findings\.  
Required: No  
**Eq**  
Represents the "equal to" condition to be applied to a single field when querying for findings\.  
Required: No  
**Neq**  
Represents the "not equal to" condition to be applied to a single field when querying for findings\.  
Required: No  
**rank**  
Specifies the position of the filter in the list of current filters\. Also specifies the order in which this filter is applied to the findings\.  
Type: Integer  
**action**  
Specifies the action that is to be applied to the findings that match the filter\.

## Errors<a name="get-filter-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. One or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `detectorId` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `name` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `name` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 