# Instances

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/instances/" %}
{% api-method-summary %}
Get List of Instances
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of instances
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
List of instances successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "91c34f50-5181-4739-915a-7615a6a72d2f",
        "type": "cpu",
        "gpu": "n/a",
        "gpu_name": "n/a",
        "num_running_jobs": 1,
        "updated_at": "06-10-2018 18:08:02",
        "created_at": "05-10-2018 16:02:04",
        "num_assigned_jobs": 0,
        "current_server_time": "06-10-2018 19:10:01",
        "last_connection": "06-10-2018 18:08:02",
        "name": "instance1",
        "status": 1,
        "ask_price": 0.02,
        "downloaded_images": [],
        "max_num_parallel_jobs": 2
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

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/instances/:uuid/" %}
{% api-method-summary %}
Get Instance
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a single instance
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
UUID of the instance
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
Instance successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
    {
        "uuid": "90c34f50-5c81-4739-955a-7685a6a72d2f",
        "type": "cpu",
        "gpu": "n/a",
        "gpu_name": "n/a",
        "num_running_jobs": 1,
        "updated_at": "06-10-2018 18:08:02",
        "created_at": "05-10-2018 16:02:04",
        "num_assigned_jobs": 0,
        "current_server_time": "06-10-2018 19:10:01",
        "last_connection": "06-10-2018 18:08:02",
        "name": "instance1",
        "status": 1,
        "ask_price": 0.02,
        "downloaded_images": [],
        "max_num_parallel_jobs": 2
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
Instance not found.
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

{% api-method method="post" host="https://sharedcloud.io" path="/api/v1/instances/" %}
{% api-method-summary %}
Create Instance
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to create an instance
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="gpu" type="string" required=false %}
UUID of the GPU of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
type of the instance. It can be "cpu" or "gpu" \(Default: "cpu"\)
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
name of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="ask\_price" type="number" required=true %}
ask price of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="max\_num\_parallel\_jobs" type="string" required=false %}
max number of parallel jobs \(Default: 1\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Instance successfully created.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "6baf15c3-5fb1-4312-b793-fc7d19629a7f",
    "current_server_time": "05-10-2018 16:29:06",
    "num_running_jobs": 0,
    "num_assigned_jobs": 0,
    "gpu_name": "n/a",
    "updated_at": "05-10-2018 16:29:06",
    "created_at": "05-10-2018 16:29:06",
    "last_connection": null,
    "type": 1,
    "name": "instance1",
    "status": 1,
    "ask_price": 0.01,
    "max_num_parallel_jobs": 1,
    "gpu": null,
    "downloaded_images": []
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

{% api-method method="put" host="https://sharedcloud.io" path="/api/v1/instances/:uuid/" %}
{% api-method-summary %}
Update Instance
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to update an instance
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
UUID of the instance
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="gpu" type="string" required=false %}
UUID of the GPU of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
type of the instance. It can be "cpu" or "gpu" \(Default: "cpu"\)
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
name of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="ask\_price" type="number" required=true %}
ask\_price of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="max\_num\_parallel\_jobs" type="string" required=false %}
max number of parallel jobs \(Default: 1\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Instance successfully updated.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "6bafb1c3-5f11-43d2-a713-fc7d19629a7f",
    "current_server_time": "05-10-2018 16:29:06",
    "num_running_jobs": 0,
    "num_assigned_jobs": 0,
    "gpu_name": "n/a",
    "updated_at": "05-10-2018 16:29:06",
    "created_at": "05-10-2018 16:29:06",
    "last_connection": null,
    "type": 1,
    "name": "instance1",
    "status": 1,
    "ask_price": 0.01,
    "max_num_parallel_jobs": 1,
    "gpu": null,
    "downloaded_images": []
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
Instance not found.
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

{% api-method method="patch" host="https://sharedcloud.io" path="/api/v1/instances/:uuid/" %}
{% api-method-summary %}
Partially update Instance
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to partially update an instance
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
UUID of the instance
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="gpu" type="string" required=false %}
UUID of the GPU of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="type" type="string" required=false %}
type of the instance. It can be "cpu" or "gpu" \(Default: "cpu"\)
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}
name of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="ask\_price" type="number" required=false %}
ask\_price of the instance
{% endapi-method-parameter %}

{% api-method-parameter name="max\_num\_parallel\_jobs" type="string" required=false %}
max number of parallel jobs \(Default: 1\)
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Instance partially updated successfully.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "6b1fb5c3-5f11-43d2-a793-fc7d01629a7f",
    "current_server_time": "05-10-2018 16:29:06",
    "num_running_jobs": 0,
    "num_assigned_jobs": 0,
    "gpu_name": "n/a",
    "updated_at": "05-10-2018 16:29:06",
    "created_at": "05-10-2018 16:29:06",
    "last_connection": null,
    "type": 1,
    "name": "instance1",
    "status": 1,
    "ask_price": 0.01,
    "max_num_parallel_jobs": 1,
    "gpu": null,
    "downloaded_images": []
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
Instance not found.
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

{% api-method method="delete" host="https://sharedcloud.io" path="/api/v1/instances/:uuid/" %}
{% api-method-summary %}
Delete Instance
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to delete an instance
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the instance
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
Instance deleted successfully
{% endapi-method-response-example-description %}

```
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
Instance not found.
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

