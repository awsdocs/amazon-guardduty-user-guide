# DeleteDetector<a name="delete-detector"></a>

Deletes the Amazon GuardDuty detector that is specified by the detector ID\.

## Request Syntax<a name="delete-detector-request-syntax"></a>

```
DELETE https://<endpoint>/detector/{detectorId}
```

**Body:**

```
detectorId : "string"
```

## Path Parameters<a name="delete-detector-path-parameters"></a>

**detectorId**  
The unique ID that specifies the detector that you want to delete\.  
Type: String  
Required: Yes

## Response Elements<a name="delete-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="delete-detector-errors"></a>

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

The request is rejected\. The current account cannot delete the detector while it has invited or associated members\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="delete-detector-example"></a>

**Sample Request**

```
DELETE /detector/12abc34d567e8fa901bc2d34e56789f0 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180123T232121Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
Date: Tue, 23 Jan 2018 23:21:22 GMT
x-amzn-RequestId: 1fe65a9d-0094-11e8-8344-4bf20881d099
X-Amzn-Trace-Id: sampled=0;root=1-5a67c372-77952f70fa2c7ec0c02de331
X-Cache: Miss from cloudfront
Via: 1.1 840717da68adc4ace0e2050590aef6c5.cloudfront.net (CloudFront)
X-Amz-Cf-Id: 4DHXuXpYnaCtVtK0oZlEy41MbwZkEF2KKjT-m0lMqA8vgghBNIEcGA==
Connection: Keep-alive
```