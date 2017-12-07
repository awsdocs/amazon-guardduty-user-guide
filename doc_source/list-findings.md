# ListFindings<a name="list-findings"></a>

Lists Amazon GuardDuty findings for the specified detector ID\.

## Request Syntax<a name="list-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings
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
    },
    "sortCriteria": {
        "attributeName": "string",
        "orderBy": "[ASC|DESC]"
    },
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Request Parameters<a name="list-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The ID of the detector that specifies the GuardDuty service whose findings you want to list\.  
Type: String  
Required: Yes

**maxResults**  
You can use this parameter to indicate the maximum number of items you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
You can use this parameter when paginating results\. Set the value of this parameter to null on your first call to the ListFindings action\. For subsequent calls to the action fill nextToken in the request with the value of nextToken from the previous response to continue listing data\.  
Type: String  
Required: No

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

**sortCriteria**  
Represents the criteria used for sorting findings\.  
Type: SortCriteria  
Required: No    
**attributeName**  
Represents the parameter in a finding which can be queried\.  
Type: String  
Required: No  
**orderBy**  
Represents the order of the sorting request\.  
Valid values: ASC | DESC  
Type: String  
Required: No

## Response Syntax<a name="list-findings-response-syntax"></a>

```
{
    "findingIds": [
        "string"
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**findingIds**  
A list of Ids that specify the findings returned by the action\.  
Type: Array of strings

**nextToken**  
Token required for pagination  
Type: String

## Errors<a name="list-findings-errors"></a>

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

The request is rejected because the parameter maxResults has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter maxResults is out\-of\-bounds\.

HTTP Status Code: 400 

**InvalidInputException**

The request was rejected because the parameter findingCriteria has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter sortCriteria has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 