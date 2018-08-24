# UpdateFilter<a name="update-filter"></a>

Updates the filter specified by the filter name\.

## Request Syntax<a name="update-filter-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/filter/<filter-name>
```

**Body:**

```
   {
    "description": "string",
    "criteria":  [
        "criterion": {
            "<field>": {
                "gt": "integer",
                "gte": "integer",
                "lt": "integer",
                "lte": "integer",
                "eq": [
                    "string"
                ],
                "neq": [
                    "string"
                ]
            }
        }
    ],
    "action": "[NOOP|ARCHIVE]",
    "rank": "integer"
  }
```

## Path Parameters<a name="update-filter-path-parameters"></a>

**detectorID**  
The unique ID of the detector that specifies the GuardDuty service where you want to update a filter\.  
Type: String  
Required: Yes

**filterName**  
The name of the filter\.  
Type: String  
Required: Yes

## Request Parameters<a name="update-filter-request-parameters"></a>

The request accepts the following data in JSON format\.

**description**  
The description of the filter\.  
Type: String  
Required: No

**findingCriteria**  
Represents the criteria to be used in the filter for querying findings\.   
Type: FindingCriteria  
Required: No  
You can only use the following attributes to query findings:       
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/update-filter.html)  
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

**action**  
Specifies the action that is to be applied to the findings that match the filter\.  
Type: Enum  
Required: No  
Valid values: NOOP \| ARCHIVE

**rank**  
Specifies the position of the filter in the list of current filters\. Also specifies the order in which this filter is applied to the findings\.  
Type: Integer  
Required: No  
Constraints: Minimum value is 1 and maximum value is equal to the increment of the total number of current filters\.

## Response Syntax<a name="update-filter-response-syntax"></a>

```
{
            "name": "string"
}
```

## Response Elements<a name="update-filter-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

**name**  
The name of the filter\.

## Errors<a name="update-detector-errors"></a>

If the action is not successful, the service sends back an HTTP error response code along with detailed error information\.

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

The request is rejected\. The parameter `description` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `findingCriteria` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `action` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. The parameter `rank` has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**AccessDeniedException**

The request is rejected\. The caller is not authorized to call this API\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `name` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="update-filter-example"></a>

**Sample Request**

```
POST /detector/12abc34d567e8fa901bc2d34e56789f0/filter/Mine HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 11
Authorization: AUTHPARAMSX-Amz-Date: 20180824T213118Z
User-Agent: aws-cli/1.15.85 Python/2.7.9 Windows/8 botocore/1.10.84
{
   "rank": 2
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 15
Date: Fri, 24 Aug 2018 21:31:19 GMT
x-amzn-RequestId: 09e2d517-a7e5-11e8-a517-bf71f53debc8
x-amz-apigw-id: MJfeGEQbPHcFQaQ=
X-Amzn-Trace-Id: Root=1-5b807927-024e2312ffbfa2e2e5a15c68;Sampled=0
X-Cache: Miss from cloudfront
Via: 1.1 2dc84924ce70e874a873764fe1415858.cloudfront.net (CloudFront)
X-Amz-Cf-Id: zyyYOrZUDaCshcl3m7JcNJQAPb8gWBKz9QBGFjqMoWTr0cuhFe3y-A==
Connection: keep-alive
{
   "name": "ExampleFilter"
}
```