# AcceptInvitation<a name="accept-invitation"></a>

Accepts the invitation to be monitored by a master GuardDuty account\.

## Request Syntax<a name="accept-invitation-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/master
```

**Body:**

```
{
    "detectorId": string",
    "masterId": "string",
    "invitationId": "string"
}
```

## Request Parameters<a name="accept-invitation-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the AWS account that is accepting an invitation to become a GuardDuty member account\.  
Type: String  
Required: Yes

**masterId**  
The account ID of the master GuardDuty account whose invitation you're accepting\.  
Type: String  
Required: Yes

**invitationId**  
The ID of the invitation sent to the AWS account by the GuardDuty master account\.  
Type: String  
Required: Yes

## Response Elements<a name="accept-invitation-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="accept-invitation-errors"></a>

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

The request is rejected because the current account cannot accept invitation from the given account ID since the latter is an associated member of another master account\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the current account cannot accept invitations since it still has created, invited or associated members\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the current account cannot accept invitations since it is already an associated member of some master account\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the current account has no pending invitation from the given master account ID or is already an associated member of another master account\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the given handshake role of the given member account ID cannot be assumed by GuardDuty on behalf of the given master account ID\.

HTTP Status Code: 400 

**LimitExceededException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 