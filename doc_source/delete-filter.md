# DeleteFilter<a name="delete-filter"></a>

Deletes the filter specified by the filter name\.

## Request Syntax<a name="delete-filter-request-syntax"></a>

```
DELETE https://<endpoint>/detector/{detectorId}/filter/<filter-name>
```

**Body:**

```
detectorId : "string"
```

## Path Parameters<a name="delete-detector-path-parameters"></a>

**detectorId**  
The unique ID that specifies the detector where you want to delete a filter\.  
Type: String  
Required: Yes

**filterName**  
The name of the filter  
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

The request is rejected\. The parameter `name` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `name` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="delete-filter-example"></a>

**Sample Request**

```
DELETE /detector/12abc34d567e8fa901bc2d34e56789f0/filter/ExampleFilter HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 0
Authorization: AUTHPARAMS
X-Amz-Date: 20180824T212338Z
User-Agent: aws-cli/1.15.85 Python/2.7.9 Windows/8 botocore/1.10.84
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 162
Date: Fri, 24 Aug 2018 21:23:39 GMT
x-amzn-RequestId: f8235579-a7e3-11e8-a743-e1fe1b7e2a7b
x-amz-apigw-id: MJeWVEqovHcFmUw=
X-Amzn-Trace-Id: Root=1-5b80775b-f058eea4b4c412bcfe33c3d1;Sampled=0
X-Cache: Miss from cloudfront
Via: 1.1 6a1e4dd9fa29c61c4b71a53d6bf94267.cloudfront.net (CloudFront)
X-Amz-Cf-Id: jXyk5-8osNMjxzgdEcYjSrMt8MvQYdVHLE6jD1Y70kajJU5u7eMcUQ==
Connection: keep-alive
```