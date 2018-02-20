# GetFindingsStatistics<a name="get-findings-statistics"></a>

Lists the statistics for the findings for the specified detector ID\.

## Request Syntax<a name="get-findings-statistics-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/statistics
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
    }
    "findingStatisticTypes": {
		"findingStatisticType": "[COUNT_BY_SEVERITY]"
	}
    
}
```

## Path Parameters<a name="get-findings-statistics-path-parameters"></a>

**detectorId**  
The ID of the detector whose findings' statistics you want to get\.  
Required: Yes

## Request Parameters<a name="get-findings-statistics-request-parameters"></a>

The request accepts the following data in JSON format\.

**findingCriteria**  
The criteria that is used for querying findings\.   
Type: FindingCriteria  
Required: No    
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

**findingStatisticTypes**  
The list of the finding statistics\.  
Required: Yes  
Type: Array of strings\. Minimum items 1\. Maximum items 10\.    
**FindingStatisticType**  
The types of finding statistics\.  
Type: String\. Valid values: `[COUNT_BY_SEVERITY]`

## Response Syntax<a name="get-findings-statistics-response-syntax"></a>

```
{
    "findingStatistics": [
        {
            "countBySeverity": "integer",
        }
    ]
}
```

## Response Elements<a name="get-findings-statistics-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**findingStatistics**  
Represents a map of severity or count statistics for a set of findings\.  
Type: Integer

## Errors<a name="get-findings-statistics-errors"></a>

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

The request is rejected\. The parameter `findingCriteria` has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected\. An invalid finding statistic type is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-findings-statistics-example"></a>

**Sample Request**

```
POST /detector/26b092acdf3e60c625b69013f7488f7b/findings/statistics HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 48
Authorization: AUTHPARAMS
X-Amz-Date: 20180209T225034Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
{  
   "findingStatisticTypes":[  
      "COUNT_BY_SEVERITY"
   ]
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 52
Date: Fri, 09 Feb 2018 22:50:36 GMT
x-amzn-RequestId: a44aa11e-0deb-11e8-8707-25a841979d1b
X-Amzn-Trace-Id: sampled=0;root=1-5a7e25bb-554e828c4c44bf219cac7cff
X-Cache: Miss from cloudfront
Via: 1.1 e6ed0c52befaa18f2fc5054cafda6db7.cloudfront.net (CloudFront)
X-Amz-Cf-Id: zXlGhggMhDACYc_qMeJLEgyaxPSaVA_vjzdsvaV-bXoAsccJGk_rzw==
Connection: Keep-alive
{  
   "findingStatistics":{  
      "countBySeverity":{  
         "2.0":45
      }
   }
}
```