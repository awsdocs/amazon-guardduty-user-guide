# UpdateDetector<a name="update-detector"></a>

Updates the Amazon GuardDuty detector that is specified by the detector ID\.

## Request Syntax<a name="update-detector-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}
```

**Body:**

```
{    
    "enable" : "boolean",
    "findingPublishingFrequency": "[FIFTEEN_MINUTES|ONE_HOUR|SIX_HOURS]"
}
```

## Path Parameters<a name="update-detector-path-parameters"></a>

**detectorID**  
The unique ID of the detector that you want to update\.  
Type: String  
Required: Yes

## Request Parameters<a name="update-detector-request-parameters"></a>

The request accepts the following data in JSON format\.

**enable**  
Specifies whether the detector is enabled\.   
Type: Boolean  
Required: No

**findingPublishingFrequency**  
Specifies the frequency of notifications sent about the subsequent finding occurrences\. For more information, see [Monitoring Amazon GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.  
Type: Enum  
Required: No  
Valid values: FIFTEEN\_MINUTES \| ONE\_HOUR \| SIX\_HOURS  
Default value: SIX\_HOURS

## Response Elements<a name="update-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="update-detector-errors"></a>

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

**AccessDeniedException**

The request is rejected\. You do not have the required `iam:CreateServiceLinkedRole` permission\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="update-detector-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 16
Authorization: AUTHPARAMS
X-Amz-Date: 20180123T231356Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "enable":true
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Tue, 23 Jan 2018 23:13:57 GMT
x-amzn-RequestId: 16c23992-0093-11e8-a33d-67e86e7cc0b9
X-Amzn-Trace-Id: sampled=0;root=1-5a67c1b5-f8ce3625e119d47f2531e4ac
X-Cache: Miss from cloudfront
Via: 1.1 b7b35e3be0ac217c56fb0eb4da9b75bb.cloudfront.net (CloudFront)
X-Amz-Cf-Id: _y_e0gjS2U1RcJ8yknRPGjYB5coSSyeG1vkV9-IKaHGUUBs03-900A==
Connection: Keep-alive
```