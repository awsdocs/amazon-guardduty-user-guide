# DeleteIPSet<a name="delete-ip-set"></a>

Deletes the IPSet that is specified by the IPSet ID\. 

**Important**  
Users from GuardDuty member accounts cannot run this API\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage IPSets\. IPSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="delete-ip-set-request-syntax"></a>

```
DELETE https://<endpoint>/detector/{detectorId}/ipset/{ipSetId}
```

**Body:**

```
detectoId : "string"
ipSetId : "string"
```

## Path Parameters<a name="delete-ip-set-path-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detector ID that specifies the GuardDuty service whose IPSet you want to delete\.  
Type: String  
Required: Yes

**ipSetId**  
The unique ID that specifies the IPSet that you want to delete\.  
Type: String  
Required: Yes

## Response Syntax<a name="delete-ip-set-response-syntax"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="delete-ip-set-errors"></a>

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

The request is rejected\. An invalid `ipSetId` is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

**InvalidInputException**

The request is rejected\. Member accounts cannot manage IPSets or ThreatIntelSets\.

HTTP Status Code: 400 

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. An invalid `ipSetId` is specified\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. The caller is not authorized to call this API\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-ip-set-example"></a>

**Sample Request**

```
DELETE /detector/12abc34d567e8fa901bc2d34e56789f0/ipset/0cb0141ab9fbde177613ab9436212e90 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T003336Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Wed, 24 Jan 2018 00:33:38 GMT
x-amzn-RequestId: 37ff4946-009e-11e8-8cd0-dfa2161e90c7
X-Amzn-Trace-Id: sampled=0;root=1-5a67d461-8a28ae442fc2780e9f9db40f
X-Cache: Miss from cloudfront
Via: 1.1 2a7e9ec6f25ccbf79b1adfa129de8f9c.cloudfront.net (CloudFront)
X-Amz-Cf-Id: eMcCNyWbQT9FNOhqD-LG11jGEpaY8YH1kpQW3OYfDM9BQfnlu6uuoA==
Connection: Keep-alive
```