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