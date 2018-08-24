# ListFilters<a name="list-filters"></a>

Returns a paginated list of the current filters\.

## Request Syntax<a name="list-filters-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/filter?maxResults=&nextToken=
```

**Body:**

```
{
    "filterNames": [
        "string"
    ],
    "nextToken": "string"
}
```

## Path Parameters<a name="list-filters-path-parameters"></a>

**detectorId**  
The ID of the detector that specifies the GuardDuty service where you want to list filters\.  
Type: String  
Required: Yes

**maxResults**  
Indicates the maximum number of items that you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListFilters` operation\. For subsequent calls to the operation, fill `nextToken` in the request with the value of `nextToken` from the previous response to continue listing data\.  
Type: String  
Required: No

## Response Syntax<a name="list-filters-response-syntax"></a>

```
{
    "filterNames": [
        "string"
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**filterNames**  
A list of filter names\.  
Type: Array of strings

**nextToken**  
The token that is required for pagination\.  
Type: String

## Errors<a name="list-filters-errors"></a>

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

**InvalidInputException**

The request is rejected\. The parameter `nextToken` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="list-filters-example"></a>

**Sample Request**

```
GET /detector/c6b0be64463ff852400d8ae5b2353866/filter HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization:AUTHPARAMS
X-Amz-Date: 20180824T211912Z
User-Agent: aws-cli/1.15.85 Python/2.7.9 Windows/8 botocore/1.10.84
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 50
Date: Fri, 24 Aug 2018 21:19:14 GMT
x-amzn-RequestId: 59eab962-a7e3-11e8-8f26-cd857361cad4
x-amz-apigw-id: MJds2FlzvHcF_PA=
X-Amzn-Trace-Id: Root=1-5b807652-7d859257708b3a4004b4dfb9;Sampled=0
X-Cache: Miss from cloudfront
Via: 1.1 fb1574d5a6ba2d77d2a656aba08aa3c3.cloudfront.net (CloudFront)
X-Amz-Cf-Id: cyWCPu_9N3l_pyxqCpGYhCCDcod2Eu71PU6TroKzPPqhKNVtMeh33w==
Connection: keep-alive
{
   "filterNames": [
      "ExampleFilter"
   ],
   "nextToken": null
}
```