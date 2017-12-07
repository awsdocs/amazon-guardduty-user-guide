# UpdateFindingsFeedback<a name="update-findings-feedback"></a>

Marks specified Amazon GuardDuty findings as useful or not useful\.

## Request Syntax<a name="update-findings-feedback-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/feedback
```

**Body:**

```
{
    "findingIds": [
        "string"
    ],
    "feedback": "[USEFUL|NOT_USEFUL]",
    "comments": "string"
}
```

## Request Parameters<a name="update-findings-feedback-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detector ID of the GuardDuty service whose findings you want to mark as useful or not useful\.  
Type: String

**findingIds**  
IDs of the findings that you want to mark as useful or not useful\.  
Type: Array of strings\. Minimum number of 0 items\. Maximum number of 50  
Required: Yes

**feedback**  
Type: String  
Required: Yes  
Valid values: USEFUL | NOT\_USEFUL

**comments**  
Additional feedback about the GuardDuty findings\.  
Type: String  
Required: No

## Response Elements<a name="update-findings-feedback-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="update-findings-feedback-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information

**InvalidInputException**

The request is rejected because required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because one or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because an invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter detectorId has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request was rejected because the parameter comment has an invalid value\.\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the number of requested finding Ids is out of bounds\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 