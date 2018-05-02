# GetMasterAccount<a name="get-master-account"></a>

Provides the details for the Amazon GuardDuty master account to the current member account\.

## Request Syntax<a name="get-master-account-request-syntax"></a>

```
POST https://<endpoint>/detector/{detectorId}/master
```

**Body:**

```
detectorId : "string"
```

## Path Parameters<a name="get-master-account-path-parameters"></a>

The request accepts the following data in JSON format\.

**detectorID**  
The detector ID of the GuardDuty member account whose master account details you want to return\.  
Required: Yes  
Type: String

## Response Syntax<a name="get-master-account-response-syntax"></a>

```
{
    "master": [
        {
           "accountId": "string",
           "invitationId": "string",
           "invitedAt": "string",
           "relationshipStatus": "string"
        }
     ]
}
```

## Response Elements<a name="get-master-account-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

The following data is returned in JSON format by the service\.

**master**  
A list of details about the GuardDuty master account for the current member account\.  
Type: Array    
**accountId**  
The account ID of a GuardDuty master account\.  
Type: String  
**invitationId**  
The ID of the invitation sent to the member by the GuardDuty master account\.  
Type: String  
**invitedAt**  
The time stamp at which the invitation was sent to the member by the GuardDuty master account\.  
Type: String  
**relationshipStatus**  
The status of the relationship between the master account and the member account\. Valid values: `STAGED` \| `PENDING` \| `DISABLED` \| `ENABLED` \| `REMOVED` \| `RESIGNED` \| `EMAILVERIFICATIONINPROGRESS` \| `EMAILVERIFICATIONFAILED`  
Type: String

## Errors<a name="get-master-account-errors"></a>

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

**NoSuchEntityException**

The request is rejected\. The input `detectorId` is not owned by the current account\.

HTTP Status Code: 400 

**InternalException**

Internal server error\.

HTTP Status Code: 500 

## Example<a name="get-master-account-example"></a>

**Sample Request**

```
GET /detector/12abc34d567e8fa901bc2d34e56789f0/master HTTP/1.1
Host: guardduty.us-west-2.amazonaws.com
Accept-Encoding: identity
Authorization: AUTHPARAMS
X-Amz-Date: 20180125T203733Z
User-Agent: aws-cli/1.14.29 Python/2.7.9 Windows/8 botocore/1.8.33
```

**Sample Response**

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 161
Date: Thu, 25 Jan 2018 20:37:34 GMT
x-amzn-RequestId: 93058ed0-020f-11e8-9ea1-377499f46311
X-Amzn-Trace-Id: sampled=0;root=1-5a6a400e-0026139dc9abc8eaac805a22
X-Cache: Miss from cloudfront
Via: 1.1 6f1f8362062a31675dde3c27bc22f2ef.cloudfront.net (CloudFront)
X-Amz-Cf-Id: NjMp1e2biYmUYjoe570CqcuDFXL3JO-_xB-8qad7moZvX-cl62iWBQ==
Connection: Keep-alive
{  
   "master":{  
      "accountId":"012345678901",
      "invitationId":"84b097800250d17d1872b34c4daadcf5",
      "invitedAt":"2018-01-25T20:26:25.825Z",
      "relationshipStatus":"Monitored"
   }
}
```