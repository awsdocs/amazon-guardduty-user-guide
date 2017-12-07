# GetThreatIntelSet<a name="get-threat-intel-set"></a>

Returns the properties of the ThreatIntelSet that is specified by the ThreatIntelSet ID\. 

## Request Syntax<a name="get-threat-intel-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/threatintelset/{threatIntelSetId}
```

**Body:**

```
detectorId : "string"
threatIntelSetId : "string"
```

## Request Parameters<a name="get-threat-intel-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detectorID that specifies the GuardDuty service whose ThreatIntelSet properties you want to return\.  
Type: String  
Required: Yes

**threatIntelSetId**  
The unique ID that specifies the ThreatIntelSet whose properties you want to return\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-threat-intel-response-syntax"></a>

```
{
    "name": "string",
    "location": "string",
    "format": "[TXT | STIX | OTX_CSV | ALIEN_VAULT | PROOF_POINT | FIRE_EYE]",
    "status": "[INACTIVE | ACTIVATING | ACTIVE | DEACTIVATING | ERROR | DELETE_PENDING | DELETED]"
}
```

## Response Elements<a name="get-threat-intel-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**name**  
The name of the ThreatIntelSet\.  
Type: String

**location**  
The URI of the file that contains the ThreatIntelSet\.  
Type: String

**format**  
The format of the file that contains the ThreatIntelSet\.  
Type: String  
Valid values : TXT | STIX | OTX\_CSV | ALIEN\_VAULT | PROOF\_POINT | FIRE\_EYE

**status**  
The current status of the ThreatIntelSet\.  
Type: String  
Valid values: INACTIVE | ACTIVATING | ACTIVE | DEACTIVATING | ERROR | DELETE\_PENDING | DELETED

## Errors<a name="get-threat-intel-errors"></a>

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

**InternalException**

Internal server error\.

HTTP Status Code: 500 