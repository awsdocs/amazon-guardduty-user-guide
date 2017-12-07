# CreateDetector<a name="create-detector"></a>

Creates a single Amazon GuardDuty detector\. A detector is an object that represents the GuardDuty service\. A detector must be created in order for GuardDuty to become operational\.

**Important**  
Currently, GuardDuty only supports one detector resource per AWS account\.

## Request Syntax<a name="create-detector-request-syntax"></a>

```
POST https://<endpoint>/detector
```

**Body:**

```
{
    "enable" : "boolean"
}
```

## Request Parameters<a name="create-detector-request-parameters"></a>

The request accepts the following data in JSON format\.

**enable**  
A boolean value that specifies whether the detector is to be enabled\.  
Type: Boolean  
Required: Yes

## Response Syntax<a name="create-detector-response-syntax"></a>

**Body:**

```
{
    "detectorId": "string"
}
```

## Response Elements<a name="create-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**detectorId**  
The unique ID of the created detector\.  
Type: String

## Errors<a name="create-detector-errors"></a>

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

**AccessDeniedException**

The request was rejected because you do not have the required iam:CreateServiceLinkedRole permission\.

HTTP Status Code: 400 

**LimitExceededException**

The request is rejected because a detector already exists for the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 