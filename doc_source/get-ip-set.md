# GetIPSet<a name="get-ip-set"></a>

Returns the properties of the IPSet specified by the IPSet ID\.

## Request Syntax<a name="get-ip-set-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/ipset/{ipSetId}
```

**Body:**

```
detectorId : "string"
ipSetId : "string"
```

## Request Parameters<a name="get-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detectorID that specifies the GuardDuty service whose properties IPSet you want to return\.  
Type: String  
Required: Yes

**ipSetId**  
The unique ID that specifies the IPSet whose properties you want to return\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-ip-set-response-syntax"></a>

```
{
    "name": "string",
    "location": "string",
    "format": "[TXT|STIX|OTX_CSV|ALIEN_VAULT|PROOF_POINT|FIRE_EYE]",
    "status": "[INACTIVE|ACTIVATING|ACTIVE|DEACTIVATING|ERROR|DELETE_PENDING|DELETED]"
}
```

## Response Elements<a name="get-ip-set-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**name**  
The name of the IPSet\.  
Type: String

**location**  
The URI of the file that contains the IPSet\.  
Type: String

**format**  
The format of the file that contains the IPSet\.  
Type: String  
Values : TXT|STIX|OTX\_CSV|ALIEN\_VAULT|PROOF\_POINT|FIRE\_EYE

**status**  
The current status of the IPSet\.  
Valid values : INACTIVE|ACTIVATING|ACTIVE|DEACTIVATING|ERROR|DELETE\_PENDING|DELETED  
Type: String

## Errors<a name="get-ip-set-errors"></a>

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

The request is rejected because an invalid ipSetId is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because an invalid ipSetId is specified\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 