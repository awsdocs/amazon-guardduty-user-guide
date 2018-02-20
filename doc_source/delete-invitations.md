# DeleteInvitations<a name="delete-invitations"></a>

Deletes invitations that are sent to this AWS account \(invitee\) by the AWS accounts \(inviters\) that are specified by their account IDs\.

## Request Syntax<a name="delete-invitations-request-syntax"></a>

```
POST https://<endpoint>/invitation/delete
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

## Request Parameters<a name="delete-invitations-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountIds**  
A list of account IDs specifying accounts whose invitations to GuardDuty you want to delete\.  
Type: Array of strings  
Required: Yes    
**accountID**  
The AWS account ID\.  
Type: String

## Response Syntax<a name="delete-invitations-response-syntax"></a>

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

## Response Elements<a name="delete-invitations-response-parameters"></a>

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

## Errors<a name="delete-invitations-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. The current account cannot delete the invitation from the specified master account ID because it is still associated to it or has not declined the invitation yet\.

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

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="delete-invitations-example"></a>

**Sample Request**

```
POST /invitation/delete HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 32
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T212908Z
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
Date: Fri, 09 Feb 2018 21:29:09 GMT
x-amzn-RequestId: 43a71a1a-0de0-11e8-8dbe-7f113b66b9c1
X-Amzn-Trace-Id: sampled=0;root=1-5a7e12a5-8e3f17ba0cdd7d2a87fe74e8
X-Cache: Miss from cloudfront
Via: 1.1 a2a7227d0a99f50bffb8ba79de64ab0f.cloudfront.net (CloudFront)
X-Amz-Cf-Id: acpQcNsnYmk1zKcvkck5cGCYl-35rw5wZvzlWxRrvzNbYV8oj9RcIg==
Connection: Keep-alive
{  
   "unprocessedAccounts":[  

   ]
}
```