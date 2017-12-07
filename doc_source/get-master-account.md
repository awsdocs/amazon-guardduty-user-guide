# GetMasterAccount<a name="get-master-account"></a>

Provides the details for the GuardDuty master account to the current GuardDuty member account\.

## Request Syntax<a name="get-master-account-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/master
```

**Body:**

```
detectorId : "string"
```

## Request Parameters<a name="get-master-account-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty member account whose master account details you want to return\.  
Required: Yes  
Type: String

## Response Syntax<a name="get-master-account-response-syntax"></a>

```
{
    "master": [
        {
           "accountId": "string",
           "invitationId": "string",
           "invitedAt": "string",
           "relationshipStatus": "string"
        }
     ]
}
```

## Response Elements<a name="get-master-account-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**master**  
A list of details about the GuardDuty master account for the current member account\.  
Type: Array    
**accountId**  
The account ID of a GuardDuty master account\.  
Type: String  
**invitationId**  
The ID of the invitation sent to the member by the GuardDuty master account  
Type: String  
**invitedAt**  
The timestamp at which the invitation was sent to the member by the GuardDuty master account\.  
Type: String  
**relationshipStatus**  
The status of the relationship between the master account and the member account\. Valid values are: Staged | Pending | Disabled | Enabled | Removed | Resigned\.  
Type: String

## Errors<a name="get-master-account-errors"></a>

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

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 