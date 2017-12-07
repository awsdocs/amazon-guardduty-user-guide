# CreateMembers<a name="create-members"></a>

Creates member GuardDuty accounts to the current AWS account \(which becomes the master GuardDuty account\) that has GuardDuty enabled\.

## Request Syntax<a name="create-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member
```

**Body:**

```
{
    "accountDetails": [
        {
            "accountId": "string",
            "email": "string"
        }
    ]
}
```

## Request Parameters<a name="create-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty account where you want to create member accounts\.  
Type: String  
Required: Yes

**accountDetails**  
A list of account ID and email address pairs of the accounts that you want to associate with the master GuardDuty account\.  
Type: Array of strings\. Minimum number of items: 1\. Maximum number of items: 50\.  
Required: Yes    
**accountID**  
AWS account ID\.   
Type: String  
Required: Yes  
**email**  
The email address of the AWS account\.  
Type: String  
Required: Yes

## Response Syntax<a name="create-members-response-syntax"></a>

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

## Response Elements<a name="create-members-response-parameters"></a>

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

## Errors<a name="create-members-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information\.

**InvalidInputException**

he request is rejected because the current account cannot create members since it is already an associated member of another master account\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected because an account cannot become a member of itself\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected because the given account ID is already a member or associated member of the current account\.

HTTP Status Code: 200 

**LimitExceededException**

The request is rejected because the current account cannot create anymore members since it cannot exceed the maximum number of allowed members\.

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