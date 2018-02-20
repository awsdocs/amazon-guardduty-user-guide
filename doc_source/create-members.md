# CreateMembers<a name="create-members"></a>

Creates member Amazon GuardDuty accounts in the current AWS account \(which becomes the master GuardDuty account\) that has GuardDuty enabled\.

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

## Path Parameters<a name="create-members-path-parameters"></a>

**detectorID**  
The detector ID of the GuardDuty account where you want to create member accounts\.  
Type: String  
Required: Yes

## Request Parameters<a name="create-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountDetails**  
A list of account ID and email address pairs of the accounts that you want to associate with the master GuardDuty account\.  
Type: Array of strings\. Minimum number of items: 1\. Maximum number of items: 50\.  
Required: Yes    
**accountID**  
The AWS account ID\.   
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
The ID of the AWS account that could not be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="create-members-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. The current account cannot create members because it is already a member of another master account\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. An account cannot become a member of itself\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. The specified account ID is already a member or associated member of the current account\.

HTTP Status Code: 200 

**LimitExceededException**

The request is rejected\. The current account cannot create more members because it cannot exceed the maximum number of allowed members\.

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

## Example<a name="create-members-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/member HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 84
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T193018Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "accountDetails":[  
      {  
         "email":"guarddutymember@amazon.com",
         "accountId":"123456789012"
      }
   ]
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 26
Date: Thu, 25 Jan 2018 19:30:19 GMT
x-amzn-RequestId: 2ddb8329-0206-11e8-a10a-75feffd08476
X-Amzn-Trace-Id: sampled=0;root=1-5a6a304b-0bc475fb7f9beaf25dc8a6a4
X-Cache: Miss from cloudfront
Via: 1.1 3a9dca02f1ba6ecd49fee9a3ca7fcb81.cloudfront.net (CloudFront)
X-Amz-Cf-Id: nujl7jYlNFfsX25GF6wgrCTyrwmys-SclGlZh2QIZFzxznX53yYYTw==
Connection: Keep-alive
{  
   "unprocessedAccounts":[  

   ]
}
```