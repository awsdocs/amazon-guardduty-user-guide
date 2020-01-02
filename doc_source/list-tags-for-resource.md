# ListTagsForResource<a name="list-tags-for-resource"></a>

Lists tags for a resource\. Tagging is currently supported for detectors, filters, IP sets, and threat intel sets, with a limit of 50 tags per resource\. When invoked, this operation returns all assigned tags for a given resource\.

## Request Syntax<a name="list-tags-for-resource-request-syntax"></a>

```
GET /tags/{resourceArn}
```

## Path Parameters<a name="list-tags-for-resource-request-parameters"></a>

**resourceArn**  
The ARN of the resource whose tags you want to list\.   
Type: String  
Required: Yes

## Response Syntax<a name="list-tags-for-resource-response-syntax"></a>

**Body:**

```
{
  "tags" : {
    "string" : "string"
  }
}
```

## Response Elements<a name="list-tags-for-resource-response-parameters"></a>

If the action is successful, the service sends back an HTTP 200 response\.

 The response is the following data in JSON format\.

**tags**  
The list of all tags \(key/value pairs\) assigned to a resource\.  
Type: Array of strings

## Errors<a name="list-tags-for-resource-errors"></a>

If the action isn't successful, the service sends back an HTTP error response code along with detailed error information\.

**BadRequestException**

HTTP Status Code: 400 

**InternalServerErrorException**

HTTP Status Code: 500 