# GetInvitationsCount<a name="get-invitations-count"></a>

Returns the count of all GuardDuty membership invitations that were sent to the current member account, not including the currently accepted invitation\.

## Request Syntax<a name="get-invitations-count-request-syntax"></a>

```
GET https://<endpoint>/invitation/count
```

## Response Syntax<a name="get-invitations-count-response-syntax"></a>

```
{
    "invitationsCount": "integer"
}
```

## Response Elements<a name="get-invitations-count-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**invitationsCount**  
A number of all membership invitations sent to this GuardDuty member account not including the currently accepted invitation\.  
Type: Integer

## Errors<a name="get-invitations-count-errors"></a>

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

**InternalException**

Internal server error\.

HTTP Status Code: 500 