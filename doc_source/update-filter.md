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