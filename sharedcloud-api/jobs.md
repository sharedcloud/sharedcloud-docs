# Jobs

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/jobs" %}
{% api-method-summary %}
Get List of Jobs
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of jobs
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
List of jobs successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "71045bdd-843d-401b-8d44-b8c4b4213042",
        "current_server_time": "05-10-2018 16:02:02",
        "function_name": "mnist",
        "duration": 20,
        "started_at": "05-10-2018 13:20:14",
        "assigned_at": "05-10-2018 13:20:14",
        "created_at": "05-10-2018 13:20:13",
        "finished_at": "05-10-2018 13:20:35",
        "incremental_id": 0,
        "status": 3,
        "arguments": "(512, 0.2, 10, 2)",
        "cost": 0.08,
        "build_logs": "...",
        "stdout": "...",
        "stderr": "...",
        "result": "0.9755",
        "instance": "504d2418-4c94-429d-8e4a-ccde12988c8b",
        "run": "9d192068-2201-4aa6-9428-fcb26ee11a35"
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

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/jobs/:uuid" %}
{% api-method-summary %}
Get Job
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a single job
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the job
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
Job successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "710b1bdd-813d-411b-8144-b1c4b7213042",
    "current_server_time": "05-10-2018 16:02:02",
    "function_name": "mnist",
    "duration": 20,
    "started_at": "05-10-2018 13:20:14",
    "assigned_at": "05-10-2018 13:20:14",
    "created_at": "05-10-2018 13:20:13",
    "finished_at": "05-10-2018 13:20:35",
    "incremental_id": 0,
    "status": 3,
    "arguments": "(512, 0.2, 10, 2)",
    "cost": 0.08,
    "build_logs": "...",
    "stdout": "...",
    "stderr": "...",
    "result": "0.9755",
    "instance": "504d1818-9194-419d-8e2a-cbde19988c8b",
    "run": "9d199b68-b211-4a16-9198-fcb26ee11a35"
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
Job not found.
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



