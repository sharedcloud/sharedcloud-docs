# How to use

To use the **Sharedcloud API**, please make sure first that you already have an account.

If this is the case, then you need to get your personal Token \(careful, it changes if you update your user account\)

```text
curl -d "username=my_username&password=my_password" -X POST https://sharedcloud.io/api/v1/api-token-auth/
```

{% hint style="info" %}
For this example we used "CURL", but you can use any other tool that you prefer.
{% endhint %}

After you get your personal Token, add it to the **HEADER** of any request you do to the Sharedcloud API, by following this format:

```text
Authorization: Token <your_token>
```

