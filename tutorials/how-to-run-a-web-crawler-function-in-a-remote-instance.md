# How to run a "web crawler" function in a remote instance

{% hint style="warning" %}
We are currently on Beta phase! Therefore, account creation is only **"invitation-based**". Write us if you want to sign up for the beta!
{% endhint %}

{% hint style="info" %}
It's strongly recommended to have a look first at the "Getting Started" guide, as some concepts are not going to be explained in detail here.
{% endhint %}

## 1. Create a file with our Function

We'll start by creating a new python3 file where we'll write the code in:

```
$ touch webcrawler_stackoverflow.py
```

Now, let's place the following code inside:

{% code-tabs %}
{% code-tabs-item title="webcrawler\_stackoverflow.py" %}
```python
import requests
from bs4 import BeautifulSoup

def handler(event):
    url = event[0]

    if(url):
        print('Fetching the number of answers and comments from {}'.format(url))
        code = requests.get(url)
        plain = code.text
        parser = BeautifulSoup(plain, "html.parser")

        num_answers = len(parser.find_all('div', {'class': 'answer'}))
        num_comments = len(parser.find_all('div', {'class': 'comment'}))

        return 'Num Answers: {}, Num Comments: {}'.format(num_answers, num_comments)
    else:
        print('Please type a valid StackOverflow URL')
```
{% endcode-tabs-item %}
{% endcode-tabs %}

In short, this function, by passing a URL of a "Stackoverflow Question Page", will tell us the number of answers and comments in the page.

{% hint style="info" %}
 Pay attention to the name of the function: "**handler**", and the name of the arguments: "**event**".  Every function you create **MUST** use the same name conventions in the signature or otherwise, won't be processed properly.
{% endhint %}

## 2. Log in into Sharedcloud

Next step would be to "log in" into **Sharedcloud:**

```text
sharedcloud login --username <your_username> --password <your_password>
```

## 3. Create a Function

After this, we can create our function:

```text
sharedcloud function create --name webcrawler_stackoverflow \
                            --file webcrawler_stackoverflow.py \
                            --image-uuid 24b3a0f8-c405-4928-954f-d5c93273f88a
```

{% hint style="info" %}
Remember: The **"--image-uuid"** contains the UUID of the image where this function will run. That particular UUID belongs to the image "sharedcloud/web-crawling-python36:latest". If the function would have had different third-party libraries we would have probably chosen a different image.
{% endhint %}

## 4. List the Functions

Perfect, let's list the function we just created:

```bash
sharedcloud function list
```

```text
UUID                                  NAME                      IMAGE                                       NUM_RUNS  WHEN
------------------------------------  ------------------------  ----------------------------------------  ----------  --------------
abe648f3-9240-42e0-86d1-1d2d10bccb94  webcrawler_stackoverflow  sharedcloud/web-crawling-python36:latest           0  2 seconds ago
```

## 5. Create a Run

Now it's the turn to create a run. Let's use 2 random Stackoverflow Questions URLs:

* ​[https://stackoverflow.com/questions/15956952/how-do-i-decrypt-using-hashlib-in-python](https://stackoverflow.com/questions/15956952/how-do-i-decrypt-using-hashlib-in-python/15956972)
* [https://stackoverflow.com/questions/4273466/reversible-hash-function](https://stackoverflow.com/questions/4273466/reversible-hash-function)

```text
sharedcloud run create --parameters "(('​https://stackoverflow.com/questions/15956952/how-do-i-decrypt-using-hashlib-in-python',), ('https://stackoverflow.com/questions/4273466/reversible-hash-function',))" \
                       --function-uuid abe648f3-9240-42e0-86d1-1d2d10bccb94 \
                       --bid-price 0.001
```

{% hint style="info" %}
Some interesting things from the last command:

1. The "**--parameters**" argument NEEDS always to be a tuple of tuple. The reason is simple. Each tuple is going to be passed to the function we defined previously \(don't worry, I'll explain this right away!\), so we want to support passing several arguments, e.g. \(\(1, 2, 3\),\)
2. The "**--bid-price**" argument represents the maximum amount of money \(in dollars\) that you would like to pay for each job, each minute. For example, "0.01" means that if I have 2 jobs, and each task takes 5 minutes, I would pay "0.01 \* 2 \* 5" = $0.10
{% endhint %}

As always, this will generate a certain number of Jobs \(2 in this case\). Let's see what parameters will get assigned to each job

{% code-tabs %}
{% code-tabs-item title="JOB 1" %}
```text
import requests
from bs4 import BeautifulSoup

def handler(event=('​https://stackoverflow.com/questions/15956952/how-do-i-decrypt-using-hashlib-in-python',)):
    url = event[0]
    ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="JOB 2" %}
```text
import requests
from bs4 import BeautifulSoup

def handler(event=('​https://stackoverflow.com/questions/4273466/reversible-hash-function',)):
    url = event[0]
    ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 7. List the Jobs

If we list the jobs, we should see them:

```text
sharedcloud job list
```

```text
UUID                                    ID  STATUS    COST    DURATION    WHEN            RUN_UUID                              FUNCTION
------------------------------------  ----  --------  ------  ----------  --------------  ------------------------------------  -----------------------
0d680b14-3a06-4a2b-9adc-367b729dc687     1  CREATED   $0.000              5 minutes ago  e0fd76e9-3d8d-4bde-80d9-81e8e885fc5e   webcrawler_stackoverflow
0c2ab08f-28f1-4d6d-8f3f-726b8eb1b324     0  CREATED   $0.000              5 minutes ago  e0fd76e9-3d8d-4bde-80d9-81e8e885fc5e   webcrawler_stackoverflow

```

After a few seconds, if the "bid-price" we provided gets matched with another user's "ask-price", we should see how our Jobs were successfully completed:

```text
UUID                                    ID  STATUS      COST    DURATION       WHEN            RUN_UUID                              FUNCTION
------------------------------------  ----  ---------   ------  ------------   --------------  ------------------------------------  ------------------------
0d680b14-3a06-4a2b-9adc-367b729dc687     1  SUCCEEDED   $0.002   2 second/s    17 minutes ago  e0fd76e9-3d8d-4bde-80d9-81e8e885fc5e  webcrawler_stackoverflow
0c2ab08f-28f1-4d6d-8f3f-726b8eb1b324     0  SUCCEEDED   $0.002   2 second/s    17 minutes ago  e0fd76e9-3d8d-4bde-80d9-81e8e885fc5e  webcrawler_stackoverflow
```

## 8. Inspect the results

Finally, for inspecting the results, we can use the following sub-commands. Let's pick as an example the first Job:

```text
sharedcloud job stdout --uuid 0d680b14-3a06-4a2b-9adc-367b729dc687
```

```text
>>> Fetching the number of answers and comments from 'https://stackoverflow.com/questions/15956952/how-do-i-decrypt-using-hashlib-in-python'
```

```text
sharedcloud job stderr --uuid 14804287-76d0-4113-9fc9-6114ca17b098
```

```text
>>>
```

```text
sharedcloud job result --uuid 14804287-76d0-4113-9fc9-6114ca17b098
```

```text
>>> Num Answers: 5, Num Comments: 8
```

{% hint style="success" %}
That's it! It's a pretty basic example, but you can see that the possibilities are endless when it comes to parametrization. With only one function you could crawl the whole Stackoverflow site should you provide enough URLs in the parameters! :\)
{% endhint %}

