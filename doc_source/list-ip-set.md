# ListIPSets<a name="list-ip-set"></a>

Lists the IPSet of the Amazon GuardDuty service that is specified by the detector ID\. 

**Important**  
If a user from a member account runs this API, the response contains the IPSets uploaded by the master account\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage IPSets\. IPSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="list-ip-set-request-syntax"></a>

**Path parameters:**

```
GET https://<endpoint>/detector/{detectorId}/ipset
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Path Parameters<a name="list-ip-set-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose IPSet objects you want to list\.  
Type: String  
Required: Yes

## Request Parameters<a name="list-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
Indicates the maximum number of items that you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListIPSets` operation\. For subsequent calls to the operation, fill `nextToken` in the request with the value of `NextToken` from the previous response to continue listing data\.  
Type: String  
Required: No

## Response Syntax<a name="list-ip-set-response-syntax"></a>

```
{
    "ipSetIds": [
        "string"
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-ip-set-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**ipSetIds**  
A list of IDs that specify the IPSet objects of the specified GuardDuty service\.  
Type: Array of strings

**nextToken**  
The token that is required for pagination\.  
Type: String

## Errors<a name="list-ip-set-errors"></a>

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

The request is rejected\. The parameter `maxResults` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `maxResults` is out\-of\-bounds\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-ip-set-example"></a>

**Sample Request**

```
GET /detector/26b092acdf3e60c625b69013f7488f7b/ipset HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T001914Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 66
Date: Wed, 24 Jan 2018 00:19:16 GMT
x-amzn-RequestId: 3655f06a-009c-11e8-b1c0-63f7fc930fe2
X-Amzn-Trace-Id: sampled=0;root=1-5a67d104-81ea75e98e2fe32d09842944
X-Cache: Miss from cloudfront
Via: 1.1 5b51f6e8f38342d63beb93a0db7a392b.cloudfront.net (CloudFront)
X-Amz-Cf-Id: RPe-C-TRFt4cMylGV8ux1PCoeG5eK1seeolplZTVhYTtRZLEkDUd6w==
Connection: Keep-alive
{  
   "ipSetId":"0cb0141ab9fbde177613ab9436212e90"
}
```