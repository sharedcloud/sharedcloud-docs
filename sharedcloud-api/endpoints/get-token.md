# Get Token

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/api-token-auth/" %}
{% api-method-summary %}
Get Token
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get a token to query the API
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="password" type="string" required=true %}
password of the user
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=true %}
username of the user
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Token successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "token": "7b0y3603e540b079fc8b3cbf63b13cb760d67161"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=400 %}
{% api-method-response-example-description %}
Invalid credentials.
{% endapi-method-response-example-description %}

```javascript
{
    "non_field_errors": [
        "Unable to log in with provided credentials."
    ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}



