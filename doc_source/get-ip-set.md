# GetIPSet<a name="get-ip-set"></a>

Returns the properties of the IPSet that is specified by the IPSet ID\.

**Important**  
If a user from a member account runs this API, the response contains the IPSets uploaded by the master account\. Currently in GuardDuty, users from member accounts CANNOT upload and further manage IPSets\. IPSets that are uploaded by the master account are imposed on GuardDuty functionality in its member accounts\. For more information, see [Managing Accounts in Amazon GuardDuty](guardduty_accounts.md)\.

## Request Syntax<a name="get-ip-set-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/ipset/{ipSetId}
```

**Body:**

```
detectorId : "string"
ipSetId : "string"
```

## Path Parameters<a name="get-ip-set-path-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The detector ID that specifies the GuardDuty service whose IPSet properties you want to return\.  
Type: String  
Required: Yes

**ipSetId**  
The unique ID that specifies the IPSet whose properties you want to return\.  
Type: String  
Required: Yes

## Response Syntax<a name="get-ip-set-response-syntax"></a>

```
{
    "name": "string",
    "location": "string",
    "format": "[TXT|STIX|OTX_CSV|ALIEN_VAULT|PROOF_POINT|FIRE_EYE]",
    "status": "[INACTIVE|ACTIVATING|ACTIVE|DEACTIVATING|ERROR|DELETE_PENDING|DELETED]",
    "tags": {
            "string": "string"
     }
}
```

## Response Elements<a name="get-ip-set-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**name**  
The name of the IPSet\.  
Type: String

**location**  
The URI of the file that contains the IPSet\.  
Type: String

**format**  
The format of the file that contains the IPSet\.  
Type: String  
Values : TXT \| STIX \| OTX\_CSV \| ALIEN\_VAULT \| PROOF\_POINT \| FIRE\_EYE

**status**  
The current status of the IPSet\.  
Valid values : INACTIVE \| ACTIVATING \| ACTIVE \| DEACTIVATING \| ERROR \| DELETE\_PENDING \| DELETED  
Type: String

**tags**  
The tags associated with the IPSet resource\. A tag consists of a key and a value that you define\.   
Type: String to string map

## Errors<a name="get-ip-set-errors"></a>

If the action is not successful, the service returns an HTTP error response code along with detailed error information\.

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

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. An invalid `ipSetId` is specified\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-ip-set-example"></a>

**Sample Request**

```
GET /detector/12abc34d567e8fa901bc2d34e56789f0/ipset/0cb0141ab9fbde177613ab9436212e90 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180124T001448Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 120
Date: Wed, 24 Jan 2018 00:14:49 GMT
x-amzn-RequestId: 976b1bdd-009b-11e8-adf3-757264fd7e81
X-Amzn-Trace-Id: sampled=0;root=1-5a67cff9-297a6d6a145fae5f3111b2d2
X-Cache: Miss from cloudfront
Via: 1.1 b2532cb29a55e8fe8106a4a9a9241592.cloudfront.net (CloudFront)
X-Amz-Cf-Id: Mibb3YLLQGISFxiVKVFAt6h_yPIRSC6F55XvF7SLOXeDQ_lNSIZdgw==
Connection: Keep-alive
{  
   "name":"ExampleIPSet",
   "location":"https://s3.amazonaws.com/guarddutylists/exampleipset.txt",
   "format":"TXT",
   "status":"ACTIVE"
}
```