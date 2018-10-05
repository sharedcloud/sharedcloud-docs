# Images

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/images" %}
{% api-method-summary %}
Get List of Images
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of images
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
List of Images successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "24b310f8-1405-4928-914f-d5c91272f88a",
        "current_server_time": "05-10-2018 16:45:36",
        "num_installations": 3,
        "registry_path": "sharedcloud/web-crawling-python36:latest",
        "updated_at": "22-09-2018 00:45:50",
        "created_at": "22-09-2018 00:45:50",
        "name": "web-crawling",
        "description": "An Image containing Python3.6 and web crawling libraries such as requests, bs4, lxml and Scrapy",
        "requires_gpu": false,
        "runtime": "python36",
        "tag": "latest"
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

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/images/:uuid" %}
{% api-method-summary %}
Get Image
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a single image
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="uuid" type="string" required=true %}
uuid of the image
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
Image successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "2413a0f8-c105-4928-914f-d5c93173f88a",
    "current_server_time": "05-10-2018 16:45:36",
    "num_installations": 3,
    "registry_path": "sharedcloud/web-crawling-python36:latest",
    "updated_at": "22-09-2018 00:45:50",
    "created_at": "22-09-2018 00:45:50",
    "name": "web-crawling",
    "description": "An Image containing Python3.6 and web crawling libraries such as requests, bs4, lxml and Scrapy",
    "requires_gpu": false,
    "runtime": "python36",
    "tag": "latest"
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
Image not found.
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

