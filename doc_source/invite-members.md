# InviteMembers<a name="invite-members"></a>

Invites other AWS accounts to enable Amazon GuardDuty and become GuardDuty member accounts\. When an account accepts the invitation and becomes a member account, the master account can view and manage the GuardDuty findings of the member account\. 

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
        "message": "string",
        "disableEmailNotification": "boolean"
     ]
}
```

## Path Parameters<a name="invite-members-path-parameters"></a>

**detectorID**  
The detector ID of the GuardDuty account that you want to use to invite members\.  
Required: Yes  
Type: String

## Request Parameters<a name="invite-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountIds**  
A list of IDs of the AWS accounts that you want to invite to GuardDuty as members\.  
Type: Array of stings  
Required: Yes    
**accountID**  
The AWS account ID\.  
Type: String

**message**  
The invitation message that gets sent to the accounts that you want to invite to GuardDuty as members\.  
Type: String  
Required: No

**disableEmailNotification**  
Specifies whether an email notification is sent to the accounts that you want to invite to GuardDuty as members\. When set to 'True', email notification is not sent to the invitees\.  
Type: Boolean  
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
The ID of the AWS account that could not be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="invite-members-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. The current account cannot invite other accounts because it is already a member of another master account\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. The current account cannot invite itself\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. The member account's email address is missing\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. The current account has already invited or is already the GuardDuty master account of the specified member account ID\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. One or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `detectorId` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="invite-members-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/member/invite HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 32
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T195805Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "accountIds":[  
      "123456789012"
   ]
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 26
Date: Thu, 25 Jan 2018 19:58:07 GMT
x-amzn-RequestId: 0f8d5826-020a-11e8-9b8e-6f87dff9eb0a
X-Amzn-Trace-Id: sampled=0;root=1-5a6a36ce-a5c2cd953fa214895696b609
X-Cache: Miss from cloudfront
Via: 1.1 202cd4e04661f12af0f4ce368b4e0a6d.cloudfront.net (CloudFront)
X-Amz-Cf-Id: JvaX4jhSDucSDIuL20JewNHkfTE7Gi_Xea14f9KncHhAO5pl7UkyVA==
Connection: Keep-alive
{  
   "unprocessedAccounts":[  

   ]
}
```