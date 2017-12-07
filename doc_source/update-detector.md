# UpdateDetector<a name="update-detector"></a>

Updates the Amazon GuardDuty detector specified by the detectorId\.

## Request Syntax<a name="update-detector-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}
```

**Body:**

```
{    
    "enable" : "boolean"
}
```

## Request Parameters<a name="update-detector-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The unique ID of the detector that you want to update\.  
Type: String  
Required: Yes

**enable**  
Updated boolean value for the detector that specifies whether the detector is enabled\.   
Type: Boolean  
Required: No

## Response Elements<a name="update-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="update-detector-errors"></a>

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

**AccessDeniedException**

The request was rejected because you do not have the required iam:CreateServiceLinkedRole permission\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 