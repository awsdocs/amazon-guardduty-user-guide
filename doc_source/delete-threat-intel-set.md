# DeleteThreatIntelSet<a name="delete-threat-intel-set"></a>

Deletes the ThreatIntelSet specified by the ThreatIntelSet ID\. 

## Request Syntax<a name="delete-threat-intel-request-syntax"></a>

```
DELETE https://<endpoint>/detector/{detectorId}/threatintelset/{threatIntelSetId}
```

**Body:**

```
detectorId : "string"
threatIntelSetId : "string"
```

## Request Parameters<a name="delete-threat-intel-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detectorID that specifies the GuardDuty service whose ThreatIntelSet you want to delete\.  
Type: String  
Required: Yes

**threatIntelSetId**  
The unique ID that specifies the ThreatIntelSet that you want to delete\.  
Type: String  
Required: Yes

## Response Syntax<a name="delete-threat-intel-response-syntax"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="delete-threat-intel-errors"></a>

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

The request is rejected because an invalid threatIntelSetId is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because an invalid threatIntelSetId is specified\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected because the caller is not authorized to call this API\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 