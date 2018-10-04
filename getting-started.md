# Getting Started

{% hint style="warning" %}
We are currently on Beta phase! Therefore, account creation is only **"invitation-based**". Write us  if you want to sign up for the beta!
{% endhint %}

## Creating your first function

1\) ****We'll start by creating a new python file where we'll write the code in:

```
$ touch hello_world.py
```

2\) Now, just place the following code inside:

{% code-tabs %}
{% code-tabs-item title="helloworld.py" %}
```python
import time

def handler(event):
    text = event[0]

    print('Sleeping for 6 seconds...')
    time.sleep(6)
    
    return 'Hello {}'.format(text)

```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
 Pay attention to the name of the function: "**handler**", and the name of the arguments: "**event**".  Every function you create **MUST** use the same name conventions in the signature or otherwise won't be processed properly.
{% endhint %}

3\) That's it with regards our code! Let's now head to the **Sharedcloud-cli** tool and schedule the function we just created. The first thing we will do would be to "login" into **Sharedcloud**

```text
sharedcloud login --username <your_username> --password <your_password>
```

4\) If the attempt was successful, you should have seem a message saying "**Login Succeeded**". Great! now, we can finally create our first function:

```text
sharedcloud function create --name hello_world \
                            --file hello_world.py \
                            --image-uuid 24b3a0f8-c405-4928-954f-d5c93273f88a
```

{% hint style="info" %}
Don't pay attention for now to the argument "**--image-uuid**". We'll talk about this soon
{% endhint %}

Nothing out of ordinary right? Just a name and a path to a file containing our code \(let's omit for now the other argument\)

5\) Alright. Now you can see the function you have just created by doing:

```bash
sharedcloud function list
```

```text
UUID                                  NAME         IMAGE                                       NUM_RUNS  WHEN
------------------------------------  -----------  ----------------------------------------  ----------  --------------
a53596a9-3867-413a-9218-5a4bfdbb05eb  hello_world  sharedcloud/web-crawling-python36:latest           0  11 seconds ago
```

6\) Do you remember about the **"--image-uuid"** argument that we intentionally omitted when creating a function? Now we can see what it does. It simply specifies the image "where" this function needs to be run. And what's an image you might ask? It's an isolated environment with many interesting libraries already installed. So it's pretty useful in case your function make use of 3rd parties libraries.

As you will see, there're plenty of images that you can use for your functions \(e.g., for web-crawling, deep learning experiments...\), you can find them in our DockerHub account: [https://hub.docker.com/u/sharedcloud/](https://hub.docker.com/u/sharedcloud/) or by executing:

```text
sharedcloud image list
```

```text
UUID                                  REGISTRY_PATH                               DESCRIPTION                                                                                      REQUIRES_GPU    WHEN
------------------------------------  ------------------------------------------  -----------------------------------------------------------------------------------------------  --------------  ----------
24b3a0f8-c405-4928-954f-d5c93273f88a  sharedcloud/web-crawling-python36:latest    An Image containing Python3.6 and web crawling libraries such as requests, bs4, lxml and Scrapy  False           6 days ago
23ca880b-94fe-472c-b9cf-934ed8295872  sharedcloud/tensorflow-gpu-python36:latest  An Image containing Python3.6 and Tensorflow for GPUs                                            True            6 days ago
a8e496b2-ab15-40ee-a1bf-3a28d7a8a2c3  sharedcloud/web-crawling-python27:latest    An Image containing Python2.7 and web crawling libraries such as requests, bs4, lxml and Scrapy  False           6 days ago
268d1309-0d8c-4bc8-9609-644fc6c9e4b5  sharedcloud/tensorflow-gpu-python27:latest  An Image containing Python2.7 and Tensorflow for GPUs                                            True            6 days ago
1a5111c1-17ee-459f-a4da-9c5272d86b1d  sharedcloud/standard-node8:latest           An Image containing Node8                                                                        False           6 days ago
```

7\) Perfect. So now that we have the function, the only thing left is to run it. To do that, we'll need to create a run. A run is a configuration object that we can use to specify different things like the list of arguments that we want to pass to the function or which GPU we would like to use to execute it \(only for GPU images, don't worry about it for now!\).

```text
sharedcloud run create --parameters "(('Michael',), ('World',))" \
                       --function-uuid <your_function_uuid> \
                       --bid-price 0.01
```

{% hint style="info" %}
Some interesting things from the last command:

1. The "**--parameters**" argument NEEDS to always be a tuple of tuple. The reason is simple. Each tuple is going to be passed to the function we defined previously \(don't worry, I'll explain this right away!\), so we want to support passing several arguments e.g., \(\(1, 2, 3\),\)
2. The "**--bid-price**" argument represents the maximum amount of money \(in dollars\) that you would like to pay for each job, each minute. For example, "0.01" means that if I have 2 jobs, and each task takes 5 minutes, I would pay "0.01 \* 2 \* 5" = $0.10
{% endhint %}

8\) That's it. The previous command has created 2 jobs. Why? you might ask. Well, because we passed as parameters:

```text
"(('Michael',), ('World',))"
```

This means, literally: _Pass the word "Michael'" to the first Job, and pass the word '"World'" to the second Job_

Now, the most important question, what's a Job? A Job is simply the function that we defined at the first step, but using as arguments the parameters we provided in the run. So it's like doing:

{% code-tabs %}
{% code-tabs-item title="JOB 1" %}
```text
import time

def handler(event):
    text = 'Michael' # <-------

    print('Sleeping for 6 seconds...')
    time.sleep(6)

    print('Hello {}'.format(text))
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="JOB 2" %}
```text
import time

def handler(event):
    text = 'World' # <-------

    print('Sleeping for 6 seconds...')
    time.sleep(6)

    print('Hello {}'.format(text))
```
{% endcode-tabs-item %}
{% endcode-tabs %}

9\) Unsurprisingly, if we list the jobs, we'll see them :\)

```text
sharedcloud job list
```

```text
UUID                                    ID  STATUS    COST    DURATION    WHEN            RUN_UUID                              FUNCTION
------------------------------------  ----  --------  ------  ----------  --------------  ------------------------------------  -----------
14804287-76d0-4113-9fc9-6114ca17b098     1  CREATED   $0.000              17 minutes ago  21e2cd66-24a5-4da8-8a9d-57f76e079dbd  hello_world
3a010085-5d12-467c-b4f3-eabdb3ebc6b6     0  CREATED   $0.000              17 minutes ago  21e2cd66-24a5-4da8-8a9d-57f76e079dbd  hello_world

```

10\) After a few seconds, if the "bid-price" we provided gets matched with another user's "ask-price", we should see how our Jobs were successfully completed:

```text
UUID                                    ID  STATUS      COST    DURATION       WHEN            RUN_UUID                              FUNCTION
------------------------------------  ----  ---------   ------  ------------   --------------  ------------------------------------  -----------
14804287-76d0-4113-9fc9-6114ca17b098     1  SUCCEEDED   $0.001   6 second/s    17 minutes ago  21e2cd66-24a5-4da8-8a9d-57f76e079dbd  hello_world
3a010085-5d12-467c-b4f3-eabdb3ebc6b6     0  SUCCEEDED   $0.001   6 second/s    17 minutes ago  21e2cd66-24a5-4da8-8a9d-57f76e079dbd  hello_world
```

11\) Finally, for inspecting the results, we can use the following sub-commands:

```text
sharedcloud job stdout --uuid 14804287-76d0-4113-9fc9-6114ca17b098
```

```text
>>> Sleeping for 6 seconds...
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
>>> Hello Michael
```

Well, that's our first function :\) We can continue now by building a "real-life" job: **A tensorflow script to train a neural network in GPU**

{% hint style="success" %}
Well, that's our first function! We can continue now by building a "real-life" task: **A tensorflow script to train a neural network in a GPU**
{% endhint %}



