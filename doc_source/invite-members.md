# InviteMembers<a name="invite-members"></a>

Invites other AWS accounts to enable GuardDuty and become GuardDuty member accounts, thus allowing the master GuardDuty account to view and manage their GuardDuty findings on their behalf\. 

## Request Syntax<a name="invite-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/invite
```

**Body:**

```
{
    "accountIds": [
        {
            "accountId": "string"
        },
        "message": "string"
     ]
}
```

## Request Parameters<a name="invite-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty account with which you want to invite members\.  
Required: Yes  
Type: String

**accountIds**  
A list of ID of the AWS accounts that you want to invite to GuardDuty as members\.  
Type: Array of stings  
Required: Yes    
**accountID**  
AWS account ID  
Type: String

**message**  
The invitation message that you want to send to the accounts that you’re inviting to GuardDuty as members\.  
Type: String  
Required: No

## Response Syntax<a name="invite-members-response-syntax"></a>

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

## Response Elements<a name="invite-members-response-parameters"></a>

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

## Errors<a name="invite-members-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected because the current account cannot invite other accounts since it is already an associated member of another master account\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected because the current account cannot invite itself\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected because member account's email address is missing\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected because the current account has already invited or is already the GuardDuty master of the given member account ID\.

HTTP Status Code: 200 

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