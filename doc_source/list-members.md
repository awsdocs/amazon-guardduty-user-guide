# ListMembers<a name="list-members"></a>

Lists details about all member accounts for the current GuardDuty master account\.

## Request Syntax<a name="list-members-request-syntax"></a>

```
GET https://<endpoint>/detector/{detectorId}/member
```

**Body:**

```
{
    "maxResults": "integer",
    "nextToken": "string",
    "onlyAssociated": "boolean"
}
```

## Request Parameters<a name="list-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty account whose members you want to list\.  
Required: Yes  
Type: String

**maxResults**  
You can use this parameter to indicate the maximum number of items you want in the response\.  
Required: No  
Type: String  
Default: 50  
Constraints: Minimum value is 1\. Maximum value is 50\.

**nextToken**  
You can use this parameter when paginating results\. Set the value of this parameter to null on your first call to the ListMembers action\. Subsequent calls to the action fill nextToken in the request with the value of NextToken from the previous response to continue listing data\.  
Required: No  
Type: String

**onlyAssociated**  
Specifies what member accounts the response is to include based on their relationship status with the master account\. The default value is TRUE\. If onlyAssociated is set to TRUE, the response will include member accounts whose relationship status with the master is set to Enabled or Disabled\. If onlyAssociated is set to FALSE, the response will include all existing member accounts\.  
Required: No  
Type: Boolean  
Default: True

## Response Syntax<a name="list-members-response-syntax"></a>

```
{
    "members": [
        {
            "accountId": "string",
            "detectorId": "string",
            "email": "string",
            "masterId": "string",
            "relationshipStatus": "string",
            "invitedAt": "string",
            "updatedAt": "string"
        }
    ],
    "nextToken": "string"
}
```

## Response Elements<a name="list-members-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**members**  
A list of details about the GuardDuty member accounts\.  
Type: Array    
**accountId**  
AWS account ID\.  
Type: String  
**detectorId**  
The unique ID of the GuardDuty member account\.  
Type: String  
**email**  
The email address of the GuardDuty member account\.  
Type: String  
**masterId**  
The account ID of the master GuardDuty for a member account\.  
Type: String  
**relationshipStatus**  
The status of the relationship between the member account and its master account\. Valid values: Created | Invited | Disabled | Enabled | Removed | Resigned\.  
Type: String  
**invitedAt**  
Timestamp at which the member account was invited to GuardDuty\.  
Type: String  
**updatedAt**  
Timestamp at which this member account was updated\.  
Type: String

**nextToken**  
When a response is generated, if there is more data to be listed, this parameter is present in the response and contains the value to use for the nextToken parameter in a subsequent pagination request\. If there is no more data to be listed, this parameter is set to null\.  
Type: Integer

## Errors<a name="list-members-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information\.

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

The request is rejected because the parameter maxResults has an invalid value\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter maxResults is out\-of\-bounds\.

HTTP Status Code: 400 

**InvalidInputException**

The request is rejected because the parameter onlyAssociated has an invalid value\.

HTTP Status Code: 400 

**NoSuchEntryException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 