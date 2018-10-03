---
description: >-
  In this guide, we'll see how to create a virtual instance that you can rent
  out for money to other users (15 minutes)
---

# How to rent out your own machine and start processing jobs

{% hint style="warning" %}
We are currently on Beta phase! Therefore, instance creation is only **"invitation-based**". Write us if you want to sign up for the beta!
{% endhint %}

## Creating the instance

1\) The first step would be to log in using the Sharedcloud CLI tool:

```text
sharedcloud login --username <your_username> --password <your_password>
```

2\) After this is done, you will be able to create your instance:

```text
sharedcloud instance create --name my_first_instance \
                            --type cpu \
                            --ask-price 0.005
```

{% hint style="info" %}
 We are creating a **CPU** instance here. For creating a **GPU** instance you would have to provide  **"--type gpu"** instead, and also add an additional argument **"--gpu-uuid"** with the UUID of the GPU model you have installed in your computer \(to find out the UUID you can run the "sharedcloud gpu list" command\)
{% endhint %}

{% hint style="info" %}
Another important thing to notice is the **"--ask-price".** This decimal number means the minimum amount \(in dollars\) for which you would be willing to rent out your computer per job and per minute. For example, if you set "0.005" and you run 3 tasks that take 5 minutes each, you would make "0.005 \* 3 \* 5" = $0.075
{% endhint %}

3\) If the command ran successfully, you should see now an instance after your run:

```text
sharedcloud instance list
```

```
UUID                                  NAME               STATUS           ASK_PRICE   TYPE    GPU      RUNNING_JOBS    MAX_NUM_PARALLEL_JOBS  LAST_CONNECTION
------------------------------------  -----------------  -------------  ------------  ------  -----  --------------  -----------------------  -----------------
662d17b0-a46c-4189-bc46-6d358a1b1eb3  my_first_instance  NOT_AVAILABLE         0.005  CPU     n/a                 0                        1

```

If you have a powerful computer, you can even parallelize incoming jobs to increment your profit. To do that, you can pass the argument **"--max-num-parallel-jobs"** when creating or updating an instance.

{% hint style="info" %}
Please notice that due to the own nature of the GPUs, the **"--max-num-parallel-jobs"** argument won't be compatible with such instances.
{% endhint %}

4\) Alright, we are almost there. The next step would be to download some images so we can run jobs from people. This is necessary beforehand, because this process usually takes a few minutes \(depending on the image\), and we don't want jobs to wait until this is done.

You definitely don't need to download all of them! It's completely up to you. Usually it depends on which kind of jobs you would like to specialize. For example, if you would like to to process "web-crawling" jobs, you most likely will want to download such images. In this guide, for the sake of simplicity, we'll download only one image "sharedcloud/web-crawling-python36:latest":

```text
sharedcloud image download --registry-path=sharedcloud/web-crawling-python36:latest
```

{% hint style="info" %}
Please keep in mind that **CPU** and **GPU** instances won't be able to use the same images. There're images specialized for each type, so don't be scared if you encounter a warning message while downloading ;\)
{% endhint %}

{% hint style="info" %}
If at some point you would like to "remove' it to free some space up, you can run the command "sharedcloud image clean --registry-path=sharedcloud/web-crawling-python36"
{% endhint %}

{% hint style="warning" %}
**Important**: Always "download" and "clean" images using those commands. Otherwise our servers won't realize of this change.
{% endhint %}

5\) Ok, enough talking, it's time to run your instance!

```text
sharedcloud instance start
```

You should start seeing some text in your screen, something like:

```text
[INFO] Updating all downloaded images...
latest: Pulling from sharedcloud/web-crawling-python36
Digest: sha256:de9d5c8ccd4ef24842567ca2195f7a43609fda10dcfa5ebd67372f3ce466a4a0
Status: Image is up to date for sharedcloud/web-crawling-python36


[INFO] Ready to take Jobs...
```

This means that the instance is waiting to receive jobs from the dispatcher. Two conditions need to occur for this to happen:

1. **The "bid-price" and "ask-price" match**
2. **The image required by the Job is already present in the instance**

If both conditions apply, you should start seeing soon an output like this one:

```text
[INFO] 2 job/s arrived, please be patient...
[INFO] Starting Job 25dab85e-c6fc-45ce-90ff-c089a7e555aa...
[INFO] Starting Job ad7c78cd-766e-4051-9c2e-ce9d9ef6491a...
[INFO] All jobs were completed.
```

{% hint style="success" %}
Congratulations! You made money! To find out how much you made, just head to the account details:
{% endhint %}

```text
sharedcloud account list
```

```text
UUID                                  EMAIL              USERNAME    BALANCE    DATE_JOINED    LAST_LOGIN
------------------------------------  -----------------  ----------  ---------  -------------  ------------
49485391-3a73-42d8-87ee-466a170bc7a4  email@example.com  username    $0.20      2 days ago     2 days ago

```

Of course, depending on how long the jobs ran, and how much was the ask price, the amount will definitely vary, but now you know how this works :\)

{% hint style="danger" %}
Please, never stop the server while jobs are being processed. You won't receive payment and you might get penalized in the algorithm
{% endhint %}

