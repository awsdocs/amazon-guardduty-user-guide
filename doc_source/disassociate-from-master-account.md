# DisassociateFromMasterAccount<a name="disassociate-from-master-account"></a>

Disassociates the current Amazon GuardDuty member account from its master account\.

## Request Syntax<a name="disassociate-from-master-account-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/master/disassociate
```

**Body:**

```
detectorId : "string"
```

## Path Parameters<a name="disassociate-from-master-account-path-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty member account that wants to disassociate from its GuardDuty master account\.  
Type: String  
Required: Yes

## Response Elements<a name="disassociate-from-master-account-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="disassociate-from-master-account-errors"></a>

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

**InvalidInputException**

The request is rejected\. The parameter `detectorId` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The current account is not associated with a master account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="disassociate-from-master-account-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/master/disassociate HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T204326Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Thu, 25 Jan 2018 20:43:27 GMT
x-amzn-RequestId: 651fdfcb-0210-11e8-acaf-711608dc8498
X-Amzn-Trace-Id: sampled=0;root=1-5a6a416f-a0b7bcb94c74288c20bced1c
X-Cache: Miss from cloudfront
Via: 1.1 16d2657cebef5191828b055567b4efeb.cloudfront.net (CloudFront)
X-Amz-Cf-Id: iMpzmm9iLQIj7_dDe9wu6KZNFFhmGyDMpPYcUZevrJBsNHhbnjxGtA==
Connection: Keep-alive
```