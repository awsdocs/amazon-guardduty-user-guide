# DeleteDetector<a name="delete-detector"></a>

Deletes the Amazon GuardDuty detector specified by the detector ID\.

## Request Syntax<a name="delete-detector-request-syntax"></a>

```
DELETE https://<endpoint>/detector/{detectorId}
```

**Body:**

```
detectorId : "string"
```

## Request Parameters<a name="delete-detector-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The unique ID that specifies the detector that you want to delete\.  
Type: String  
Required: Yes

## Response Elements<a name="delete-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="delete-detector-errors"></a>

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

**InvalidInputException**

The request is rejected because the current account cannot delete detector while it has invited or associated members\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 