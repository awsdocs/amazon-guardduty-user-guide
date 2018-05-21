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
		]
	}
	"action": "[NOOP|ARCHIVE]",
	"rank": "integer"
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