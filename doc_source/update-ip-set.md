# UpdateIPSet<a name="update-ip-set"></a>

Updates the IPSet specified by the IPSet ID\. 

## Request Syntax<a name="update-ip-set-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/ipset/{ipSetId}
```

**Body:**

```
{
    "name": "string",
    "location": "string",
    "activate": "boolean"
}
```

## Request Parameters<a name="delete-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detectorID that specifies the GuardDuty service whose IPSet you want to update\.  
Type: String  
Required: Yes

**ipSetId**  
The unique ID that specifies the IPSet that you want to update\.  
Type: String  
Required: Yes

**name**  
The updated user\-friendly name for the IPSet\.  
Type: String  
Required: No

**location**  
The updated URI of the file that contains the IPSet\.  
Type: String  
Required: No

**activate**  
The updated boolean value that specifies whether the IPSet is active or not\.  
Type: Boolean  
Required: No

## Response Syntax<a name="update-ip-set-response-syntax"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="delete-ip-set-errors"></a>

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

The request is rejected because an invalid ipSetId is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because an invalid ipSetId is specified\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected because the caller is not authorized to call this API\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because no role was found

HTTP Status Code: 400 

**BadRequestException**

The request is rejected because the service can't assume service role\.

HTTP Status Code: 400 

**AccessDeniedException**

The request was rejected because you do not have the required iam:PutRolePolicy permission\.

HTTP Status Code: 400 

**BadRequestException**

The request was rejected because the specified service role is not a service role\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 