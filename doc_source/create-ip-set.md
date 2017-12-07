# CreateIPSet<a name="create-ip-set"></a>

Creates a new IPSet \- a list of trusted IP addresses that have been whitelisted for secure communication with your AWS environment\.

## Request Syntax<a name="create-ip-set-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/ipset
```

**Body:**

```
{
    "name": "string",
    "location": "string",
    "format": "[TXT|STIX|OTX_CSV|ALIEN_VAULT|PROOF_POINT|FIRE_EYE]",
    "activate": "boolean"
}
```

## Request Parameters<a name="create-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detectorID that specifies the GuardDuty service for which an IPSet is to be created\.   
Type: String  
Required: Yes

**name**  
The user friendly name to identify the IPSet\. This name is displayed in all findings that are triggered by activity that involves IP addresses included in this IPSet\.  
Type: String  
Required: Yes

**format**  
The format of the file that contains the IPSet\.  
Type: String, valid values are: TXT|STIX|OTX\_CSV|ALIEN\_VAULT|PROOF\_POINT|FIRE\_EYE  
Required: Yes

**location**  
The URI of the file that contains the IPSet\.  
Type: String  
Required: Yes

**activate**  
A boolean value that indicates whether GuardDuty is to start using the uploaded IPSet\.  
Type: Boolean  
Required: Yes

## Response Syntax<a name="create-ip-set-response-syntax"></a>

```
{
    "ipSetId": "string"
}
```

## Response Elements<a name="create-ip-set-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**ipSetId**  
The unique ID that specifies the newly created IPSet\.  
Type: String

## Errors<a name="create-ip-set-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information

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

The request is rejected because the parameter name has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter location has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter format has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because an invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

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