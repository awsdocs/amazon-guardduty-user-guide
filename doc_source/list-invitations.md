# ListInvitations<a name="list-invitations"></a>

Lists all GuardDuty membership invitations that were sent to the current AWS account\.

## Request Syntax<a name="list-invitations-request-syntax"></a>

```
GET https://<endpoint>/invitation
```

**Body:**

```
{
    "maxResults" : "integer"
    "nextToken" : "string"
}
```

## Request Parameters<a name="list-invitations-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
You can use this parameter to indicate the maximum number of items you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
You can use this parameter when paginating results\. Set the value of this parameter to null on your first call to the ListInvitations action\. Subsequent calls to the action fill nextToken in the request with the value of NextToken from the previous response to continue listing data\.  
Required: No  
Type: String

## Response Syntax<a name="list-invitations-response-syntax"></a>

```
{
    "invitations": [
        {
           "accountId": "string",
           "invitationId": "string",
           "invitedAt": "string",
           "relationshipStatus": "string"
        }
     ],
     "nextToken": "string"
}
```

## Response Elements<a name="list-invitations-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**invitations**  
A list of details about GuardDuty membership invitations that were sent to this AWS account\.  
Type: Array    
**accountId**  
The ID of the AWS account that sent the invitation\.  
Type: String  
**invitationId**  
The unique ID of the invitation\.  
Type: String  
**invitedAt**  
The timestamp at which the invitation was sent\.  
Type: String  
**relationshipStatus**  
The current relationship status between the inviter and invitee accounts\. Valid values are: Created | Invited | Disabled | Enabled | Removed | Resigned\.  
Type: String

**nextToken**  
When a response is generated, if there is more data to be listed, this parameter is present in the response and contains the value to use for the nextToken parameter in a subsequent pagination request\. If there is no more data to be listed, this parameter is set to null\.  
Type: String

## Errors<a name="list-invitations-errors"></a>

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

The request is rejected because the parameter maxResults has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter maxResults is out\-of\-bounds\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 