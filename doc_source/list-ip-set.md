# ListIPSets<a name="list-ip-set"></a>

Lists the IPSets of the GuardDuty service specified by the detector ID\. 

## Request Syntax<a name="list-ip-set-request-syntax"></a>

**Path parameters:**

```
GET https://<endpoint>/detector/{detectorId}/ipset
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Request Parameters<a name="list-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detectorID that specifies the GuardDuty service whose IPSets you want to list\.  
Type: String  
Required: Yes

**maxResults**  
You can use this parameter to indicate the maximum number of items that you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
You can use this parameter when paginating results\. Set the value of this parameter to null on your first call to the ListIPSets action\. For subsequent calls to the action fill nextToken in the request with the value of NextToken from the previous response to continue listing data\.  
Type: String  
Required: No

## Response Syntax<a name="list-ip-set-response-syntax"></a>

```
{
    "ipSetIds": [
        "string"
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-ip-set-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**ipSetIds**  
A list of IDs that specify the IPSets of the specified GuardDuty service\.  
Type: Array of strings

**nextToken**  
Token required for pagination\.  
Type: String

## Errors<a name="list-ip-set-errors"></a>

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

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 