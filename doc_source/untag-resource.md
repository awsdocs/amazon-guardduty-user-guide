# UntagResource<a name="untag-resource"></a>

Removes tags from a resource\.

## Request Syntax<a name="untag-resource-request-syntax"></a>

```
DELETE /tags/{resourceArn}?TagKeys=tag1,tag2,tag3
```

## Path Parameters<a name="untag-resource-path-parameters"></a>

**resourceArn**  
The ARN of the resource whose tags you want to remove\.  
Type: String  
Required: Yes

## Request Parameters<a name="untag-resource-request-parameters"></a>

The request accepts the following data in JSON format\.

**tags**  
The tags that you want to remove from the specified resource\. A tag consists of a key and a value that you define\.   
Type: List of strings  
Required: Yes

## Response Elements<a name="untag-resource-response-parameters"></a>

If the action is successful, the service sends back an HTTP 204 response\.

 The response is the following data in JSON format\.

## Errors<a name="untag-resource-errors"></a>

If the action isn't successful, the service sends back an HTTP error response code along with detailed error information\.

**BadRequestException**

HTTP Status Code: 400 

**InternalServerErrorException**

HTTP Status Code: 500 