# Offers

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/offers/" %}
{% api-method-summary %}
Get List of Offers
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the list of Offers
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
List of Offers successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "name": "example",
        "type": 2,
        "gpu_name": "Nvidia Tesla P4 8GB",
        "cuda_cores": 2560,
        "ask_price": 0.34,
        "last_connection": "01-10-2018 18:11:25",
        "current_server_time": "04-10-2018 16:55:19"
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

