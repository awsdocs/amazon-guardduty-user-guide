# CreateSampleFindings<a name="create-sample-findings"></a>

Creates sample findings of the types specified by a list of GuardDuty finding types\. If 'NULL' is specified for findingTypes, the operation creates sample findings of all supported GuardDuty finding types\. 

## Request Syntax<a name="create-sample-findings-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/findings/create
```

**Body:**

```
{
    "findingTypes": [
        {
            "findingType": "string",
        }
     ]
}
```

## Request Parameters<a name="create-sample-findings-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorId**  
The ID of the GuardDuty service where you want to create sample findings\.  
Required: Yes  
Type: String

**findingTypes**  
The list of GuardDuty finding types that specifies what types of sample findings you want to create\.  
Required: Yes  
Type: Array of strings  
Constraints: Minimum length of 0\. Maximum length of 50\.    
**findingType**  
The type of the GuardDuty finding\.  
Type: String

## Response Elements<a name="create-sample-findings-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

## Errors<a name="create-sample-findings-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information

**InvalidInputException**

The request is rejected because an invalid or out\-of\-range value is specified as an input parameter\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because required query or path parameters are not specified\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because one or more input parameters have invalid values\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter detectorId has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because of invalid finding type is specified\.

HTTP Status Code: 400 

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 