# CreateFilter<a name="create-filter"></a>

Creates a GuardDuty findings filter using the specified finding criteria\. 

## Request Syntax<a name="create-filter-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/filter
```

**Body:**

```
{
    "name": "string",
    "description": "string",
    "findingCriteria": {
    "criterion": [
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
    ],
    "action": "[NOOP|ARCHIVE]",
    "rank": "integer",
    "tags": {
            "string": "string"
    }
}
```

## Path Parameters<a name="create-filter-path-parameters"></a>

**detectorId**  
The ID of the detector that specifies the GuardDuty service whose findings you want to filter\.  
Type: String  
Required: Yes

## Request Parameters<a name="create-filter-request-parameters"></a>

The request accepts the following data in JSON format\.

**name**  
The name of the filter\.  
Type: String  
Required: Yes

**description**  
The description of the filter\.  
Type: String  
Required: No

**tags**  
The tags that you want to add to the Filter resource\. A tag consists of a key and a value that you define\.   
Type: String to string map  
Required: No

**findingCriteria**  
Represents the criteria to be used in the filter for querying findings\.   
Type: FindingCriteria  
Required: Yes  
You can only use the following attributes to query findings:       
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/guardduty/latest/ug/create-filter.html)  
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
Default: NOOP

**rank**  
Specifies the position of the filter in the list of current filters\. Also specifies the order in which this filter is applied to the findings\.  
Type: Integer  
Required: No  
Constraints: Minimum value is 1 and maximum value is equal to the increment of the total number of current filters\.  
Default: 1

## Response Syntax<a name="create-filter-response-syntax"></a>

```
{
       "name": "string",
}
```

## Response Elements<a name="create-filter-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**name**  
The name of the successfully created filter\.  
Type: String

## Errors<a name="create-filter-errors"></a>

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

**LimitExceededException**

The request is rejected because filter limit has exceeded\.

HTTP Status Code: 400 

**EntityAlreadyExistsException**

The request is rejected because a filter with the given name already exists\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="create-filter-example"></a>

**Sample Request**

```
GET /detector/12abc34d567e8fa901bc2d34e56789f0 HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180123T220712Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33

POST /detector/12abc34d567e8fa901bc2d34e56789f0/filter HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Content-Length: 179
Authorization: AUTHPARAMS
X-Amz-Date: 20180824T205429Z
User-Agent: aws-cli/1.15.85 Python/2.7.9 Windows/8 botocore/1.10.84
{
   "findingCriteria": {
      "criterion": {
         "resource.instanceDetails.instanceId": {
            "eq": [
               "i-49113b93"
            ]
         }
      }
   },
   "name": "ExampleFilter"
}
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 24
Date: Fri, 24 Aug 2018 20:54:31 GMT
x-amzn-RequestId: e5cd1bbc-a7df-11e8-9be9-751fcb56efc9
x-amz-apigw-id: MJaFFEoJPHcFrrQ=
X-Amzn-Trace-Id: Root=1-5b807086-aa465aeb2b382d7254eb28b5;Sampled=0
X-Cache: Miss from cloudfront
Via: 1.1 88eb066576c1b47cd896ab0019b9f25f.cloudfront.net (CloudFront)
X-Amz-Cf-Id: BtfJWcoxlH6ZblhQncoPu7ozBJU7etV8RO8veE8l3vBYOUM22SsyrQ==
Connection: keep-alive
{
   "name": "ExampleFilter"
}
```