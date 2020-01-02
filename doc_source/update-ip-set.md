# UpdateIPSet<a name="update-ip-set"></a>

Updates the IPSet that is specified by the IPSet ID\. 

**Important**  
Users from GuardDuty member accounts cannot run this API\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage IPSets\. IPSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="update-ip-set-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/ipset/{ipSetId}
```

**Body:**

```
{
    "name": "string",
    "location": "string",
    "activate": "boolean"
}
```

## Path Parameters<a name="delete-ip-set-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service whose IPSet you want to update\.  
Type: String  
Required: Yes

**ipSetId**  
The unique ID that specifies the IPSet that you want to update\.  
Type: String  
Required: Yes

## Request Parameters<a name="delete-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**name**  
The updated friendly name for the IPSet\.  
Type: String  
Required: No

**location**  
The updated URI of the file that contains the IPSet\.  
Type: String  
Required: No

**activate**  
Specifies whether the IPSet is active or not\.  
Type: Boolean  
Required: No

## Response Syntax<a name="update-ip-set-response-syntax"></a>

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

**InvalidInputException**

The request is rejected\. Member accounts cannot manage IPSets or ThreatIntelSets\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. An invalid `ipSetId` is specified\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. The caller is not authorized to call this API\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. No role was found\.

HTTP Status Code: 400 

**BadRequestException**

The request is rejected\. The service can't assume the service role\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. You do not have the required `iam:PutRolePolicy` permission\.

HTTP Status Code: 400 

**BadRequestException**

The request is rejected\. The specified service role is not a service role\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-ip-set-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/ipset/0cb0141ab9fbde177613ab9436212e90 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 19
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T002823Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "activate":false
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Wed, 24 Jan 2018 00:28:25 GMT
x-amzn-RequestId: 7d04eb7e-009d-11e8-9150-9b7ab09573a9
X-Amzn-Trace-Id: sampled=0;root=1-5a67d328-1f5cd901719c010f77e58ee3
X-Cache: Miss from cloudfront
Via: 1.1 2d8af5cc5befc5d35bb54b4a5b6494c9.cloudfront.net (CloudFront)
X-Amz-Cf-Id: 9yHsYLUD63GBTsSwOGPBRRDtoU5m_Ncv9LAJ-EmknNTNxi9wzC0zew==
Connection: Keep-alive
```