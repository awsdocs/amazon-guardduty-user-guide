# GetDetector<a name="get-detector"></a>

Returns the properties of the Amazon GuardDuty detector that is specified by the detectorId\.

## Request Syntax<a name="get-detector-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}
```

## Request Parameters<a name="get-detector-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The unique ID of the detector that you want to describe\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-detector-response-syntax"></a>

```
{
    "serviceRole": "string",
    "status": "string",
    "createdAt": "string",
    "updatedAt": "string"
}
```

## Response Elements<a name="get-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

 The response is in following data in JSON format\. 

**serviceRole**  
The service\-linked role that grants GuardDuty access to the AWS account's resources\.   
Type: String

**status**  
The current status of the detector\.  
Type: String\. Valid Values: ENABLED | DISABLED

**createdAt**  
The time at which the detector was created\.  
Type: String

**updatedAt**  
The time at which detector was last updated\.  
Type: String

## Errors<a name="get-detector-errors"></a>

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

The request is rejected because the parameter detectorId has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

Internal server error\.

HTTP Status Code: 500 