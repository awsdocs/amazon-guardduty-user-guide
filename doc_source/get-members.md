# GetMembers<a name="get-members"></a>

Returns the details on the GuardDuty member accounts specified by the account IDs\.

## Request Syntax<a name="get-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/get
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

## Request Parameters<a name="get-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty account on whose members you want to return the details\.  
Type: String  
Required: Yes

**accountIds**  
A list of account IDs for the GuardDuty member accounts on which you want to return the details\.  
Type: Array of strings  
Required: Yes    
**accountID**  
AWS account ID\.  
Type: String

## Response Syntax<a name="get-members-response-syntax"></a>

```
{
    "members": [
        {
            "accountId": "string",
            "detectorId": "string",
            "email": "string",
            "masterId": "string",
            "relationshipStatus": "string",
            "invitedAt": "string",
            "updatedAt": "string"
        }
    ],
    "unprocessedAccounts": [
        {
            "accountId": "string",
            "result": "string"
        }
    ]
}
```

## Response Elements<a name="get-members-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**members**  
A list of details about the GuardDuty member accounts\.  
Type: Array    
**accountId**  
AWS account ID\.  
Type: String  
**detectorId**  
The unique ID of the GuardDuty member account\.  
Type: String  
**email**  
The email address of the GuardDuty member account\.  
Type: String  
**masterId**  
The account ID of the master GuardDuty for a member account\.  
Type: String  
**relationshipStatus**  
The status of the relationship between the member account and its master account\. Valid values: Created | Invited | Disabled | Enabled | Removed | Resigned\.  
Type: String  
**invitedAt**  
Timestamp at which the member account was invited to GuardDuty\.  
Type: String  
**updatedAt**  
Timestamp at which this member account was updated\.  
Type: String

**unprocessedAccounts**  
A list of account ID and email address pairs of the AWS accounts that could not be processed\.  
Type: Array of strings    
**accountID**  
The ID of the AWS account that could be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="describe-members-errors"></a>

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