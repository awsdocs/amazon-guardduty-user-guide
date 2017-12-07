# DisassociateFromMasterAccount<a name="disassociate-from-master-account"></a>

Disassociates the current GuardDuty member account from its GuardDuty master account\.

## Request Syntax<a name="disassociate-from-master-account-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/master/disassociate
```

**Body:**

```
detectorId : "string"
```

## Request Parameters<a name="disassociate-from-master-account-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty member account that wants to disassociate from its GuardDuty master account\.  
Type: String  
Required: Yes

## Response Elements<a name="disassociate-from-master-account-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="disassociate-from-master-account-errors"></a>

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

The request is rejected because the current account is not associated to a master account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 