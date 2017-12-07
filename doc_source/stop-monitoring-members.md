# StopMonitoringMembers<a name="stop-monitoring-members"></a>

Disables GuardDuty from monitoring findings of the member accounts specified by the account IDs\. After running this command, a master GuardDuty account can run [StartMonitoringMembers](start-monitoring-members.md) to re\-enable GuardDuty to monitor these members’ findings\. 

## Request Syntax<a name="stop-monitoring-members-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/member/stop
```

**Body:**

```
{
    "accountIds": [
        {
            "accountId": "string"
        }
     ]
}
```

## Request Parameters<a name="stop-monitoring-members-request-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty account whom you want to stop from monitoring members accounts' findings\.  
Type: String  
Required: Yes

**accountIds**  
A list of account IDs of the GuardDuty member accounts whose findings you want the master account to stop monitoring\.  
Type: Array of strings  
Required: Yes    
**accountID**  
AWS account ID\.  
Type: String

## Response Syntax<a name="stop-monitoring-members-response-syntax"></a>

```
{
    "unprocessedAccounts": [
        {
            "accountId": "string",
            "result": "string"
        }
    ]
}
```

## Response Elements<a name="stop-monitoring-members-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**unprocessedAccounts**  
A list of account ID and email address pairs of the AWS accounts that could not be processed\.  
Type: Array of strings    
**accountID**  
The ID of the AWS account that could be processed\.  
Type: String  
**result**  
The reason why the AWS account could not be processed\.  
Type: String

## Errors<a name="stop-monitoring-members-errors"></a>

If the action is not successful, the service sends back and HTTP error response code along with detailed error information\.

**InvalidInputException**

The request is rejected because the given account ID is not an associated member of account the current account\.

HTTP Status Code: 200 

**InvalidInputException**

The request is rejected because the given handshake role of the given member account ID cannot be assumed by GuardDuty on behalf of the given master account ID\.

HTTP Status Code: 200 

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

**NoSuchEntityException**

The request is rejected because the input detectorId is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 