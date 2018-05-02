# ListFindings<a name="list-findings"></a>

Lists Amazon GuardDuty findings for the specified detector ID\.

## Request Syntax<a name="list-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings
```

**Body:**

```
{
    "findingCriteria": {
        "criterion": {
            "<field>": {
                "Gt": "integer",
                "Gte": "integer",
                "Lt": "integer",
                "Lte": "integer",
                "Eq": [
                    "string"
                ],
                "Neq": [
                    "string"
                ]
            }
        }
    },
    "sortCriteria": {
        "attributeName": "string",
        "orderBy": "[ASC|DESC]"
    },
    "maxResults": "integer",
    "nextToken": "string"
}
```

## Path Parameters<a name="list-findings-path-parameters"></a>

**detectorId**  
The ID of the detector that specifies the GuardDuty service whose findings you want to list\.  
Type: String  
Required: Yes

## Request Parameters<a name="list-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**maxResults**  
Indicates the maximum number of items that you want in the response\.  
Type: Integer  
Required: No  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
Paginates results\. Set the value of this parameter to NULL on your first call to the `ListFindings` operation\. For subsequent calls to the operation, fill `nextToken` in the request with the value of `nextToken` from the previous response to continue listing data\.  
Type: String  
Required: No

**findingCriteria**  
Represents the criteria used for querying findings\.   
Type: FindingCriteria  
Required: No  
You can only use the following attributes to query findings:   
+ accountId
+ id 
+ region 
+ resource\.instanceDetails\.instanceId 
+ resource\.resourceType 
+ service\.archived 
**Note**  
When this attribute is set to TRUE, only archived findings are listed\. When it's set to FALSE, only unarchived findings are listed\. When this attribute is not set, all existing findings are listed\.
+ service\.action\.networkConnectionAction\.blocked 
+ service\.action\.networkConnectionAction\.connectionDirection 
+ service\.action\.networkConnectionAction\.localPortDetails\.port 
+ service\.action\.networkConnectionAction\.protocol 
+ service\.action\.networkConnectionAction\.remoteIpDetails\.ipAddressV4 
+ service\.action\.networkConnectionAction\.remotePortDetails\.port 
+ service\.action\.actionType 
+ service\.additionalInfo\.threatListName 
+ severity
+ type
+ updatedAt

  Type: ISO 8601 string format: YYYY\-MM\-DDTHH:MM:SS\.SSSZ or YYYY\-MM\-DDTHH:MM:SSZ depending on whether the value contains milliseconds\.  
**Gt**  
Represents the "greater than" condition to be applied to a single field when querying for findings\.  
Required: No  
**Gte**  
Represents the "greater than equal" condition to be applied to a single field when querying for findings\.  
Required: No  
**Lt**  
Represents the "less than" condition to be applied to a single field when querying for findings\.  
Required: No  
**Lte**  
Represents the "less than equal" condition to be applied to a single field when querying for findings\.  
Required: No  
**Eq**  
Represents the "equal to" condition to be applied to a single field when querying for findings\.  
Required: No  
**Neq**  
Represents the "not equal to" condition to be applied to a single field when querying for findings\.  
Required: No

**sortCriteria**  
Represents the criteria used for sorting findings\.  
Type: SortCriteria  
Required: No    
**attributeName**  
Represents the parameter in a finding that can be queried\.  
Type: String  
Required: No  
**orderBy**  
Represents the order of the sorting request\.  
Valid values: ASC \| DESC  
Type: String  
Required: No

## Response Syntax<a name="list-findings-response-syntax"></a>

```
{
    "findingIds": [
        "string"
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**findingIds**  
A list of IDs that specify the findings that are returned by the operation\.  
Type: Array of strings

**nextToken**  
The token that is required for pagination\.  
Type: String

## Errors<a name="list-findings-errors"></a>

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

The request is rejected\. The parameter `findingCriteria` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `sortCriteria` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="list-findings-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/findings HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 70
Authorization: AUTHPARAMS
X-Amz-Date: 20180212T223938Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "findingCriteria":{  
      "criterion":{  
         "updatedAt":{  
            "gte":1486685375
         }
      }
   }
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1746
Date: Mon, 12 Feb 2018 22:39:39 GMT
x-amzn-RequestId: 9c063378-1045-11e8-912b-55dcb9d58ea1
X-Amzn-Trace-Id: sampled=0;root=1-5a8217ab-91c20067a9d784bf259099f2
X-Cache: Miss from cloudfront
Via: 1.1 1a1272478361d8461b68eec8a4e3b072.cloudfront.net (CloudFront)
X-Amz-Cf-Id: hJB2P8k3QOSuLXimNeOn2EuBvz_ixcnsaOHW1pBZ7KNnPYPdTE0rEA==
Connection: Keep-alive
{
   "findingIds":[
      "d4b0be682aeeb94e06ff046f3b720aaf",
      "40b0be6cfea750c084aae20c21ace107",
      "cab0be7a06e5ebe1d8911cadbfbd51c8",
      "d0b0c39ae57fb67f9edbd2622961771d",
      "14b0be677c07323d61d7006cce074238",
      "6eb0be66d03c7b27037f8609875c9bf7",
      "c4b0be6e6177dd4e269da24de95c933e",
      "64b0c3bb2da01d83eb306d067ea73e67",
      "3ab0c0e7734ccbda8f7074952063a45f",
      "38b0c0ce04f29861dc6331631a233b6b",
      "4cb0c28afacdfc4bb5577b224e0e52ae",
      "94b0c2305c7d6ff1e3d483e7f36a5238",
      "72b0c1f80a23ca9082133c46c7558666",
      "d6b0c1910d5faeb6e89fe40bd78a35e6",
      "14b0c18efa4f2981d44b2131a560b73a",
      "9cb0be64df8ba1df249c45eb8a0bf584",
      "08b0be64df8b46440d718fc5e33e449c",
      "70b0be64df8b3342472e966717a5f2d8",
      "86b0be64df8ae19c13c4d55080b48e6a",
      "e6b0be64df8ae6744746c151aebbef4c",
      "36b0be64df8a1f72cbc32e723c2d8b89",
      "4cb0be64df8a20484f3a1f7ad816ca96",
      "5cb0be64df8a6b5c3da491b5599fc8ae",
      "44b0be64df89360da7c31819b3f515fa",
      "76b0be64df89cc6ffa31a5d34888368c",
      "0eb0be64df890a043aef0b1b807ddfc7",
      "ceb0be64df894fdef2500c7ffcc44b84",
      "32b0be64df88b6c6e8bbc29a798739ca",
      "50b0be64df88991e0221f80f4288441d",
      "72b0be64df88753b1aa9146729bc2fcc",
      "fab0be64df887026d806b6553d67bacb",
      "2ab0be64df878810cbe619a0ba7ef05d",
      "78b0be64df87ab9eb027d0c0820433d6",
      "3eb0be64df872fa74d318e6e31d03728",
      "40b0be64df8746cdecf990d3f89fe633",
      "56b0be64df86ad5f22e15c17b381bd8c",
      "9eb0be64df8693f01ade916097512133",
      "d2b0be64df86145bbafa2f2ea9e05dba",
      "d8b0be64df85da2fb107ee60013fef4d",
      "f0b0be64df864f7d6c70d0adc21ec430",
      "aeb0be64df85d6365eb815b1bef28dff",
      "ccb0be64df85e42caf8e33b916eaf7d1",
      "2cb0be64df852627bbb68f63749b36e0",
      "90b0be64df8513c19d6864ea3a02b91f",
      "7ab0be64df84dd2cb89e38547264e956",
      "94b0be64df84c4e7ce9f49f95b58b4ac",
      "92b0be64df846c83bd36dca0d7cd8271",
      "ccb0be64df845a4ed9258957024d0a5b",
      "50b0be64df83e63bb9693bb63b2e9faa"
   ],
   "nextToken":""
}
```