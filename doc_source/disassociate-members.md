# DisassociateMembers<a name="disassociate-members"></a>

Disassociates GuardDuty member accounts specified by the account IDs from their master GuardDuty account\.

## Request Syntax<a name="disassociate-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/disassociate
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

## Request Parameters<a name="disassociate-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The unique ID of the detector of the GuardDuty account whose members you want to disassociate from master\.  
Type: String  
Required: Yes

**accountIds**  
A list of account IDs of the GuardDuty member accounts that you want to disassociate from the master account\.  
Type: Array of strings  
Required: Yes    
**accountID**  
AWS account ID\.  
Type: String

## Response Syntax<a name="disassociate-members-response-syntax"></a>

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

## Response Elements<a name="disassociate-members-response-parameters"></a>

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

## Errors<a name="disassociate-members-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected because the current account cannot delete the given member account ID since it is still associated to it\.

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

he request is rejected because the parameter detectorId has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntryException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 