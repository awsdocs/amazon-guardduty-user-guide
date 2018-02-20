# CreateIPSet<a name="create-ip-set"></a>

Creates an IPSet, which is a list of trusted IP addresses that have been whitelisted for highly secure communication with your AWS environment\.

**Important**  
Users from GuardDuty member accounts cannot run this API\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage IPSets\. IPSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing AWS Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="create-ip-set-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/ipset
```

**Body:**

```
{
    "name": "string",
    "location": "string",
    "format": "[TXT|STIX|OTX_CSV|ALIEN_VAULT|PROOF_POINT|FIRE_EYE]",
    "activate": "boolean"
}
```

## Path Parameters<a name="create-ip-set-path-parameters"></a>

**detectorId**  
The detector ID that specifies the GuardDuty service for which an IPSet is to be created\.   
Type: String  
Required: Yes

## Request Parameters<a name="create-ip-set-request-parameters"></a>

The request accepts the following data in JSON format\.

**name**  
The friendly name to identify the IPSet\. This name is displayed in all findings that are triggered by activity that involves IP addresses included in this IPSet\.  
Type: String  
Required: Yes

**format**  
The format of the file that contains the IPSet\.  
Type: String\. Valid values: `TXT` | `STIX` | `OTX_CSV` | `ALIEN_VAULT` | `PROOF_POINT` | `FIRE_EYE`  
In your trusted IP lists and threat lists, IP addresses and CIDR ranges must appear one per line\.  
The following is a sample list in Plaintext format:  

```
54.20.175.217
205.0.0.0/8
```
For more information, see [Uploading Trusted IP Lists and Threat Lists](guardduty_upload_lists.md)
Required: Yes

**location**  
The URI of the file that contains the IPSet\.  
Type: String  
Required: Yes

**activate**  
Specifies whether GuardDuty is to start using the uploaded IPSet\.  
Type: Boolean  
Required: Yes

## Response Syntax<a name="create-ip-set-response-syntax"></a>

```
{
    "ipSetId": "string"
}
```

## Response Elements<a name="create-ip-set-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**ipSetId**  
The unique ID that specifies the newly created IPSet\.  
Type: String

## Errors<a name="create-ip-set-errors"></a>

If the action is not successful, the service returns an HTTP error response code along with detailed error information\.

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

The request is rejected\. The parameter `name` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `location` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `format` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. An invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. Member accounts cannot manage IPSets or ThreatIntelSets\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

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

The request is rejected\. The specified service role is not a service\-linked role\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="create-ip-set-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/ipset HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 125
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T000824Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "format":"TXT",
   "activate":true,
   "location":"https://s3.amazonaws.com/guarddutylists/sample.txt",
   "name":"ExampleIPSet"
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 46
Date: Wed, 24 Jan 2018 00:08:34 GMT
x-amzn-RequestId: b2890dcb-009a-11e8-b847-0dd5f510dc2a
X-Amzn-Trace-Id: sampled=0;root=1-5a67ce79-a478009a74d2b2b17cba97f3
X-Cache: Miss from cloudfront
Via: 1.1 97c5dcf9c391508cdebbbfdcf304912f.cloudfront.net (CloudFront)
X-Amz-Cf-Id: F6a_zK56EOZU_GODJVrzv94U9bH9ckLWXa0bCeHSbdaivK-WkTb77Q==
Connection: Keep-alive
{  
   "ipSetId":"0cb0141ab9fbde177613ab9436212e90"
}
```