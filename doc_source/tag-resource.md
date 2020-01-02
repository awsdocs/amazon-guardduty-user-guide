# TagResource<a name="tag-resource"></a>

Assigns tags to a resource\.

## Request Syntax<a name="tag-resource-request-syntax"></a>

```
POST /tags/{resourceArn}
```

**Body:**

```
{
    "tags": { 
      "string": "string" 
   }
}
```

## Path Parameters<a name="tag-resource-path-parameters"></a>

**resourceArn**  
The ARN of the resource that you want to assign tags to\.  
Type: String  
Required: Yes

## Request Parameters<a name="tag-resource-request-parameters"></a>

The request accepts the following data in JSON format\.

**tags**  
The tags that you want to add to the specified resource\. A tag consists of a key and a value that you define\.   
Type: String to string map  
Required: Yes

## Response Elements<a name="tag-resource-response-parameters"></a>

If the action is successful, the service sends back an HTTP 204 response\.

 The response is the following data in JSON format\.

## Errors<a name="tag-resource-errors"></a>

If the action isn't successful, the service sends back an HTTP error response code along with detailed error information\.

**BadRequestException**

HTTP Status Code: 400 

**InternalServerErrorException**

HTTP Status Code: 500 