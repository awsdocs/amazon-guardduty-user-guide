# ArchiveFindings<a name="archive-findings"></a>

Archives Amazon GuardDuty findings specified by the list of finding IDs\.

## Request Syntax<a name="archive-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/archive
```

**Body:**

```
{
    "findingIds": [
        "string"
    ]
}
```

## Request Parameters<a name="archive-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The ID of the detector that specifies the GuardDuty service whose findings you want to archive\.  
Required: Yes  
Type: String

**findingIds**  
IDs of the findings that you want to archive\.  
Type: Array of strings\. Minimum number of 0 items\. Maximum number of 50 items\.  
Required: Yes

## Response Elements<a name="archive-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="archive-findings-errors"></a>

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

The request is rejected because the number of requested finding Ids is out of bounds\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected because the caller is not authorized to call this API\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 