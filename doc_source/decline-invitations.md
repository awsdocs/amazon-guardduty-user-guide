# DeclineInvitations<a name="decline-invitations"></a>

Declines invitations that are sent to this AWS account \(invitee\) by the AWS accounts \(inviters\) that are specified by the account IDs\.

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
The AWS account ID\.  
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
The ID of the AWS account that could not be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="decline-invitations-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. One or more input parameters have invalid values\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="decline-invitations-example"></a>

**Sample Request**

```
POST /invitation/decline HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 32
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T212220Z
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
Date: Fri, 09 Feb 2018 21:22:22 GMT
x-amzn-RequestId: 50d4524e-0ddf-11e8-8662-ef6b8065279d
X-Amzn-Trace-Id: sampled=0;root=1-5a7e110d-59812fd97e6d69b6d0444902
X-Cache: Miss from cloudfront
Via: 1.1 13fbcc8fa3dbc202089a58be1b399e76.cloudfront.net (CloudFront)
X-Amz-Cf-Id: tc1MUaEI2G-yoIMgPEZlgCLmDvwMuJXiJF6LrMoFVjjqcGOEJPdvBQ==
Connection: Keep-alive
{  
   "unprocessedAccounts":[  

   ]
}
```