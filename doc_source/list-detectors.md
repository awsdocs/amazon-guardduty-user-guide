# ListDetectors<a name="list-detectors"></a>

Lists detectorIds of all existing enabled Amazon GuardDuty detectors in the AWS account\.

**Important**  
Currently, GuardDuty only supports one detector resource per AWS account\.

## Request Syntax<a name="list-detector-request-syntax"></a>

```
GET https://<endpoint>/detector
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Request Parameters<a name="list-detectors-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
You can use this parameter to indicate the maximum number of items that you want in the response\.   
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
You can use this parameter when paginating results\. Set the value of this parameter to null on your first call to the ListDetectors action\. For subsequent calls to the action, fill nextToken in the request with the value of NextToken from the previous response to continue listing data\.  
Type: String  
Required: No

## Response Syntax<a name="list-detector-response-syntax"></a>

**Body:**

```
{
    "detectorIds": [list of detector IDs]
}
```

## Response Elements<a name="list-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

 The response is in following data in JSON format\.

**detectorIds**  
The list of all enabled detector's IDs\.  
Type: Array of strings

**nextToken**  
Token required for pagination  
Type: String

## Errors<a name="list-detector-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information\.

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

The request is rejected because the parameter maxResults has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter maxResults is out\-of\-bounds\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 