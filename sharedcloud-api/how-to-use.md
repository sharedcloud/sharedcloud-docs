# How to use

To use the **Sharedcloud API**, you will need an account in **Sharedcloud**. Please make sure that you have one.

If this is the case, then you need to get your personal Token \(careful, it changes every time you update your user account\)

```text
curl -d "username=my_username&password=my_password" -X POST https://sharedcloud.io/api/v1/api-token-auth/
```

{% hint style="info" %}
In this example we used "CURL", but you can use your favourite REST Client.
{% endhint %}

After you have your personal Token, add it to the **HEADER** of any request you do to the **Sharedcloud API**, by following this format:

```text
Authorization: Token <your_token>
```

