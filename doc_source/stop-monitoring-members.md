# StopMonitoringMembers<a name="stop-monitoring-members"></a>

Disables Amazon GuardDuty from monitoring findings of the member accounts that are specified by the account IDs\. After running this command, a master GuardDuty account can run [StartMonitoringMembers](start-monitoring-members.md) to re\-enable GuardDuty to monitor the findings of these members\. 

## Request Syntax<a name="stop-monitoring-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/stop
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

## Path Parameters<a name="stop-monitoring-members-path-parameters"></a>

**detectorID**  
The detector ID of the GuardDuty account that you want to stop from monitoring the findings of member accounts\.  
Type: String  
Required: Yes

## Request Parameters<a name="stop-monitoring-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**accountIds**  
A list of account IDs of the GuardDuty member accounts whose findings you want the master account to stop monitoring\.  
Type: Array of strings  
Required: Yes    
**accountID**  
AWS account ID\.  
Type: String

## Response Syntax<a name="stop-monitoring-members-response-syntax"></a>

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

## Response Elements<a name="stop-monitoring-members-response-parameters"></a>

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

## Errors<a name="stop-monitoring-members-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected\. The specified account ID is not a member of the current account\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected\. The specified handshake role of the specified member account ID cannot be assumed by GuardDuty on behalf of the specified master account ID\.

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

## Example<a name="stop-monitoring-members-example"></a>

**Sample Request**

```
POST /detector/26b092acdf3e60c625b69013f7488f7b/member/stop HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 32
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T215008Z
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
Date: Fri, 09 Feb 2018 21:50:09 GMT
x-amzn-RequestId: 32b833a1-0de3-11e8-b5b7-6ffb530727e9
X-Amzn-Trace-Id: sampled=0;root=1-5a7e1791-5affbdd584be95ecf97cc9f2
X-Cache: Miss from cloudfront
Via: 1.1 4b41f5d4002cf5daabe6e170bd619abc.cloudfront.net (CloudFront)
X-Amz-Cf-Id: KhOTiBOnEjFXmBjANQOjIiYCE2fGOGiaFAKfetjK65Dv16VWeH4ESw==
Connection: Keep-alive
{  
   "unprocessedAccounts":[  

   ]
}
```