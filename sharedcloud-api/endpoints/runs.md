# Runs

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/runs" %}
{% api-method-summary %}
Get List of Runs
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of runs
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
List of runs successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "8b199e68-b301-4ba6-9498-f5b2beee2a35",
        "current_server_time": "05-10-2018 15:16:10",
        "base_gpu_name": "Nvidia Tesla P4 8GB",
        "num_jobs": 1,
        "function_name": "mnist",
        "created_at": "05-10-2018 13:20:13",
        "parameters": "((512, 0.2, 10, 2),)",
        "bid_price": 0.3,
        "function": "9a9420da-a848-4523-a138-d3cf47007131",
        "base_gpu": "e4c0d486-d74e-4248-824b-e6dd39464a85"
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

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/runs/:uuid" %}
{% api-method-summary %}
Get Run
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a single run
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the run
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
Run successfully retrieved
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "9d194068-b241-4aa6-9448-f4b26eee1a35",
    "current_server_time": "05-10-2018 15:16:10",
    "base_gpu_name": "Nvidia Tesla P4 8GB",
    "num_jobs": 1,
    "function_name": "mnist",
    "created_at": "05-10-2018 13:20:13",
    "parameters": "((512, 0.2, 10, 2),)",
    "bid_price": 0.3,
    "function": "9a9f20da-a848-4523-a138-ddcf35007131",
    "base_gpu": "e6c0dd86-d7ee-4248-844b-e6dd394aaa85"
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
Run not found
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

{% api-method method="post" host="https://sharedcloud.io" path="/api/v1/runs" %}
{% api-method-summary %}
Create Run
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to create a run
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="base\_gpu" type="string" required=false %}
UUID of the required GPU \(Only for GPU images\)
{% endapi-method-parameter %}

{% api-method-parameter name="function" type="string" required=true %}
UUID of the function
{% endapi-method-parameter %}

{% api-method-parameter name="bid\_price" type="number" required=true %}
bid price of the run
{% endapi-method-parameter %}

{% api-method-parameter name="parameters" type="string" required=true %}
parameters of the run
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Run successfully created
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "ebcc4d16-04b2-45c4-9520-9e50a4931bd6",
    "num_jobs": 1,
    "base_gpu": None,
    "base_gpu_name": 'n/a',
    "bid_price": 1.0,
    "function_name": "mnist",
    "created_at": "05-10-2018 14:51:12",
    "parameters": "((512, 0.2, 10, 2),)",
    "function": "594864fa-d4f4-4cc3-844b-74546a76ce52",
    "current_server_time": "05-10-2018 14:55:12"
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

{% api-method method="delete" host="https://sharedcloud.io" path="/api/v1/runs/:uuid" %}
{% api-method-summary %}
Delete Run
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to delete a run
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the run
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
Run deleted successfully.
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
Run not found
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

