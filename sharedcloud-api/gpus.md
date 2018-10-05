# GPUs

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/gpus" %}
{% api-method-summary %}
Get List of GPUs
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of GPUs
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
List of GPUs successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "caf01aeb-ba13-4499-14f9-8b4961714366",
        "current_server_time": "05-10-2018 16:51:18",
        "is_available": false,
        "created_at": "25-09-2018 12:07:42",
        "name": "Nvidia Titan V 12GB",
        "codename": "titanv",
        "cuda_cores": 5120
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

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/gpus/:uuid" %}
{% api-method-summary %}
Get GPU
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a single GPU
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the GPU
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
List of GPUs successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "c1f0daeb-ba13-4199-b1f9-814965714366",
    "current_server_time": "05-10-2018 16:51:18",
    "is_available": false,
    "created_at": "25-09-2018 12:07:42",
    "name": "Nvidia Titan V 12GB",
    "codename": "titanv",
    "cuda_cores": 5120
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
GPU not found.
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

