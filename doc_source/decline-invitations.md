# DeclineInvitations<a name="decline-invitations"></a>

Declines invitations sent to this AWS account \(invitee\) by the AWS accounts \(inviters\) specified by the account IDs\.

## Request Syntax<a name="decline-invitations-request-syntax"></a>

```
POST https://<endpoint>/invitation/decline
```

**Body:**

```
{
    "accountIds": [
        {
            "accountId": "string"
        }
     ]
}
```

## Request Parameters<a name="decline-invitations-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountIds**  
A list of account IDs specifying accounts whose invitations to GuardDuty you want to decline\.  
Type: Array of strings  
Required: Yes    
**accountID**  
AWS account ID\.  
Type: String

## Response Syntax<a name="decline-invitations-response-syntax"></a>

```
{
    "unprocessedAccounts": [
        {
            "accountId": "string",
            "result": "string"
        }
    ]
}
```

## Response Elements<a name="decline-invitations-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**unprocessedAccounts**  
A list of account ID and email address pairs of the AWS accounts that could not be processed\.  
Type: Array of strings    
**accountID**  
The ID of the AWS account that could be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="decline-invitations-errors"></a>

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

**InternalException**

Internal server error\.

HTTP Status Code: 500 