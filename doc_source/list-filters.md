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