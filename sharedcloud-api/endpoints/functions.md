# Functions

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/functions" %}
{% api-method-summary %}
Get List of Functions
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of functions
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
List of functions successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "8b9420da-a848-4523-a138-ddbf33007631",
        "current_server_time": "05-10-2018 14:51:12",
        "registry_path": "sharedcloud/tensorflow-gpu-python36:latest",
        "runtime": "python36",
        "num_runs": 1,
        "updated_at": "05-10-2018 13:18:53",
        "created_at": "05-10-2018 13:18:53",
        "name": "mnist",
        "code": "...",
        "image": "23ca880b-94fe-472c-b9cf-934ed8295872"
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Invalid token."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/functions/:uuid" %}
{% api-method-summary %}
Get Function
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a single function
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the function
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Function successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "8b94207a-a878-4523-a138-ddc733077131",
    "current_server_time": "05-10-2018 14:51:12",
    "registry_path": "sharedcloud/tensorflow-gpu-python36:latest",
    "runtime": "python36",
    "num_runs": 1,
    "updated_at": "05-10-2018 13:18:53",
    "created_at": "05-10-2018 13:18:53",
    "name": "mnist",
    "code": "...",
    "image": "23ca880b-94fe-472c-b9cf-934ed8295872"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Invalid token."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Function not found.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Not found."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://sharedcloud.io" path="/api/v1/functions" %}
{% api-method-summary %}
Create Function
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to create a function
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="code" type="string" required=true %}
code of the function
{% endapi-method-parameter %}

{% api-method-parameter name="runtime" type="string" required=true %}
runtime of the function
{% endapi-method-parameter %}

{% api-method-parameter name="image" type="string" required=true %}
UUID of the image
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
name of the function
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Function successfully created.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "8b94207a-a878-4523-a128-ddc732077131",
    "current_server_time": "05-10-2018 14:51:12",
    "registry_path": "sharedcloud/tensorflow-gpu-python36:latest",
    "runtime": "python36",
    "num_runs": 1,
    "updated_at": "05-10-2018 13:18:53",
    "created_at": "05-10-2018 13:18:53",
    "name": "mnist",
    "code": "...",
    "image": "23ca880b-94fe-472c-b9cf-934ed8295872"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Invalid token."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://sharedcloud.io" path="/api/v1/functions/:uuid" %}
{% api-method-summary %}
Update Function
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to update a function
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
UUID of the function
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="code" type="string" required=true %}
code of the function
{% endapi-method-parameter %}

{% api-method-parameter name="runtime" type="string" required=true %}
runtime of the function
{% endapi-method-parameter %}

{% api-method-parameter name="image" type="string" required=true %}
UUID of the image
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
name of the function
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Function successfully updated.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "8b94207a-a878-4523-a138-ddc733077131",
    "current_server_time": "05-10-2018 14:51:12",
    "registry_path": "sharedcloud/tensorflow-gpu-python36:latest",
    "runtime": "python36",
    "num_runs": 1,
    "updated_at": "05-10-2018 13:18:53",
    "created_at": "05-10-2018 13:18:53",
    "name": "mnist",
    "code": "...",
    "image": "23ca880b-94fe-472c-b9cf-934ed8295872"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Invalid token."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Function not found.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Not found."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="patch" host="https://sharedcloud.io" path="/api/v1/functions/:uuid" %}
{% api-method-summary %}
Partially update Function
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to partially update a function
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
UUID of the function
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="code" type="string" required=false %}
code of the function
{% endapi-method-parameter %}

{% api-method-parameter name="runtime" type="string" required=false %}
runtime of the function
{% endapi-method-parameter %}

{% api-method-parameter name="image" type="string" required=false %}
UUID of the image
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
name of the function
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Function partially updated successfully.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "8b94207a-a878-4523-a138-ddc733077131",
    "current_server_time": "05-10-2018 14:51:12",
    "registry_path": "sharedcloud/tensorflow-gpu-python36:latest",
    "runtime": "python36",
    "num_runs": 1,
    "updated_at": "05-10-2018 13:18:53",
    "created_at": "05-10-2018 13:18:53",
    "name": "mnist",
    "code": "...",
    "image": "23ca880b-94fe-472c-b9cf-934ed8295872"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Invalid token."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Function not found
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Not found."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://sharedcloud.io" path="/api/v1/functions/:uuid" %}
{% api-method-summary %}
Delete Function
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to delete a function
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the function
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Function deleted successfully.
{% endapi-method-response-example-description %}

```javascript
{}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Invalid token."
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Function not found
{% endapi-method-response-example-description %}

```javascript
{
    "detail": "Not found."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



