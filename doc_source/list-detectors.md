# ListDetectors<a name="list-detectors"></a>

Lists the detector IDs of enabled Amazon GuardDuty detectors in an AWS account\.

**Important**  
Currently, GuardDuty supports only one detector resource per AWS account per region\.

## Request Syntax<a name="list-detector-request-syntax"></a>

```
GET https://<endpoint>/detector
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Request Parameters<a name="list-detectors-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
Indicates the maximum number of items that you want in the response\.   
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListDetectors` operation\. For subsequent calls to the operation, fill `nextToken` in the request with the value of `NextToken` from the previous response to continue listing data\.  
Type: String  
Required: No

## Response Syntax<a name="list-detector-response-syntax"></a>

**Body:**

```
{
    "detectorIds": [list of detector IDs]
}
```

## Response Elements<a name="list-detector-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

 The response is the following data in JSON format\.

**detectorIds**  
The list of all enabled detector IDs\.  
Type: Array of strings

**nextToken**  
The token that is required for pagination\.  
Type: String

## Errors<a name="list-detector-errors"></a>

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

The request is rejected\. The parameter `maxResults` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `maxResults` is out\-of\-bounds\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="list-detectors-example"></a>

**Sample Request**

```
GET /detector HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180123T230745Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 52
Date: Tue, 23 Jan 2018 23:07:46 GMT
x-amzn-RequestId: 397d0549-0092-11e8-a0ee-a7f9aa6e7572
X-Amzn-Trace-Id: sampled=0;root=1-5a67c042-3405ff97a36fd78ee5cce278
X-Cache: Miss from cloudfront
Via: 1.1 bdf69c9338fccde2f01f587a28200671.cloudfront.net (CloudFront)
X-Amz-Cf-Id: 4iF3SMkI1xcf_P7mLPyoj5cCpLdx--TiMJUrVKdNf3lpCdCVJCNLgQ==
Connection: Keep-alive
{  
   "detectorIds":[  
      "12abc34d567e8fa901bc2d34e56789f0"
   ]
}
```