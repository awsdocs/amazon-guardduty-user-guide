# CreateDetector<a name="create-detector"></a>

Creates a single Amazon GuardDuty detector\. A detector is an object that represents the GuardDuty service\. You must create a detector to enable GuardDuty\.

**Important**  
Currently, GuardDuty supports only one detector resource per AWS account per region\.

## Request Syntax<a name="create-detector-request-syntax"></a>

```
POST https://<endpoint>/detector
```

**Body:**

```
{
    "enable" : "boolean",
    "findingPublishingFrequency": "[FIFTEEN_MINUTES|ONE_HOUR|SIX_HOURS]",
    "tags": {
            "string": "string"
    }
}
```

## Request Parameters<a name="create-detector-request-parameters"></a>

The request accepts the following data in JSON format\.

**enable**  
Specifies whether the detector is to be enabled\.  
Type: Boolean  
Required: Yes

**findingPublishingFrequency**  
Specifies the frequency of notifications sent about the subsequent finding occurrences\. For more information, see [Monitoring GuardDuty Findings with Amazon CloudWatch Events](guardduty_findings_cloudwatch.md)\.  
Type: Enum  
Required: No  
Valid values: FIFTEEN\_MINUTES \| ONE\_HOUR \| SIX\_HOURS  
Default value: SIX\_HOURS

**tags**  
The tags that you want to add to the dectector resource\. A tag consists of a key and a value that you define\.   
Type: List of strings  
Required: No

## Response Syntax<a name="create-detector-response-syntax"></a>

**Body:**

```
{
    "detectorId": "string"
}
```

## Response Elements<a name="create-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**detectorId**  
The unique ID of the created detector\.  
Type: String

## Errors<a name="create-detector-errors"></a>

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

**AccessDeniedException**

The request is rejected\. You do not have the required `iam:CreateServiceLinkedRole` permission\.

HTTP Status Code: 400 

**LimitExceededException**

The request is rejected\. A detector already exists for the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="create-detector-example"></a>

**Sample Request**

```
POST /detector HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180123T215330Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 49
Date: Tue, 23 Jan 2018 21:53:32 GMT
x-amzn-RequestId: da9e1c5b-0087-11e8-8012-7985c94ad5ec
X-Amzn-Trace-Id: sampled=0;root=1-5a67aedc-76d97a5c367f2eac94d40825
X-Cache: Miss from cloudfront
Via: 1.1 08df71188a92655a7dcd1bb872797741.cloudfront.net (CloudFront)
X-Amz-Cf-Id: kYGX5j6wkW7fneZ8ee602vqpr3JCuQqBHyyMdpTwG9JV3u0ybcdaNQ==
Connection: Keep-alive
{  
   "detectorId":"12abc34d567e8fa901bc2d34e56789f0"
}
```