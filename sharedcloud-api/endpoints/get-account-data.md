# User Accounts

{% api-method method="get" host="https://sharedcloud.io" path="/api/v1/users/account/" %}
{% api-method-summary %}
Get Account data
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to get the account data
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
User account successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "uuid": "3a7e1abe-c26e-43a8-8a1b-574cdf1fb851",
    "username": "johndoe",
    "email": "johndow@example.com",
    "last_login": None,
    "date_joined": "22-03-2017 22:11:32",
    "balance": 0.02,
    "current_server_time": "27-05-2018 23:21:55"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials
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

{% api-method method="post" host="https://sharedcloud.io" path="/api/v1/users/" %}
{% api-method-summary %}
Create User Account
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to create a new user account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
email of the user
{% endapi-method-parameter %}

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
User account successfully created.
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "49aee734-018f-5947-a1d5-2750ba20f845",
        "username": "johndoe",
        "email": "johndoe@example.com",
        "last_login": "04-10-2018 16:02:28",
        "date_joined": "26-09-2018 17:51:07",
        "balance": 0.08,
        "current_server_time": "05-10-2018 14:12:37"
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials
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

{% api-method method="put" host="https://sharedcloud.io" path="/api/v1/users/account/" %}
{% api-method-summary %}
Update User Account
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you update a user account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=true %}
email of the user
{% endapi-method-parameter %}

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
Account successfully updated
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "29aee732-518f-4944-a1d5-17e0baa0f845",
        "username": "johndoe",
        "email": "johndoe@example.com",
        "last_login": "04-10-2018 16:02:28",
        "date_joined": "26-09-2018 17:51:07",
        "balance": 0.08,
        "current_server_time": "05-10-2018 14:12:37"
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials
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

{% api-method method="patch" host="https://sharedcloud.io" path="/api/v1/users/account/" %}
{% api-method-summary %}
Partially update User Account
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows to partially update a user account
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
Authentication token
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-body-parameters %}
{% api-method-parameter name="email" type="string" required=false %}
email of the user
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=false %}
password of the user
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=false %}
username of the user
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Account successfully partially updated
{% endapi-method-response-example-description %}

```javascript
[
    {
        "uuid": "29aee734-218f-6947-a7d5-27e07aa0f845",
        "username": "johndoe",
        "email": "johndoe@example.com",
        "last_login": "04-10-2018 16:02:28",
        "date_joined": "26-09-2018 17:51:07",
        "balance": 0.08,
        "current_server_time": "05-10-2018 14:12:37"
    }
]
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials
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

{% api-method method="delete" host="https://sharedcloud.io" path="/api/v1/users/account/" %}
{% api-method-summary %}
Delete User Account
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows you to delete a user account
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
Account successfully deleted
{% endapi-method-response-example-description %}

```javascript
{}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=401 %}
{% api-method-response-example-description %}
Invalid credentials
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



