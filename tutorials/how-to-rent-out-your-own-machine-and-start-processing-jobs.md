# How to rent out your machine resources and start processing jobs

{% hint style="warning" %}
We are currently on Beta phase! Therefore, instance creation is only **"invitation-based**". Write us if you want to sign up for the beta!
{% endhint %}

## 1. Log in into Sharedcloud

The first step would be to log in using the Sharedcloud CLI tool:

```text
sharedcloud login --username <your_username> --password <your_password>
```

## 2. Create an Instance

After this is done, we should be able to create an instance:

```text
sharedcloud instance create --name my_first_instance \
                            --type cpu \
                            --ask-price 0.005
```

{% hint style="info" %}
 We are creating a **CPU** instance here. For creating a **GPU** instance, you would have to provide  **"--type gpu"** instead, and also add an additional argument **"--gpu-uuid"** with the UUID of the GPU model you have installed in your computer \(to find out the UUID you can run the "sharedcloud gpu list" command\)
{% endhint %}

{% hint style="info" %}
Another critical thing to notice is the **"--ask-price".** This decimal number means the minimum amount \(in dollars\) for which you would be willing to rent out your computer per job and minute. For example, if you set "0.005" and you run 3 tasks that take 5 minutes each, you would make "0.005 \* 3 \* 5" = $0.075
{% endhint %}

## 3. List the Instances

If the command ran successfully, we should see an instance after running:

```text
sharedcloud instance list
```

```
UUID                                  NAME               STATUS           ASK_PRICE   TYPE    GPU      RUNNING_JOBS    MAX_NUM_PARALLEL_JOBS  LAST_CONNECTION
------------------------------------  -----------------  -------------  ------------  ------  -----  --------------  -----------------------  -----------------
662d17b0-a46c-4189-bc46-6d358a1b1eb3  my_first_instance  NOT_AVAILABLE         0.005  CPU     n/a                 0                        1

```

If we had a powerful computer, we could even parallelize incoming jobs to increment our profit. To do that, we can pass the argument **"--max-num-parallel-jobs"** when creating or updating an instance.

{% hint style="info" %}
Please notice that due to the own nature of the GPUs, the **"--max-num-parallel-jobs"** argument won't be compatible with such instances.
{% endhint %}

## 4. Download an Image

All right, we are almost there. The next step would be to download some images so we can run jobs from people. This download process is necessary beforehand because this process usually takes a few minutes \(depending on the image\), and we don't want upcoming jobs to wait until this is done.

We don't need to download all the images available! It's completely up to us. Usually, it depends on which kind of jobs you would like to specialize. For example, if we would like to process "web-crawling" jobs, we most likely want to download images in that area. In this guide, for the sake of simplicity, we'll download only one image **"sharedcloud/web-crawling-python36:latest":**

```text
sharedcloud image download --registry-path=sharedcloud/web-crawling-python36:latest
```

{% hint style="info" %}
Please keep in mind that **CPU** and **GPU** instances won't be able to use the same images. There're images specialized for each type, so don't be scared if you encounter a warning message preventing you from downloading a certain image ;\)
{% endhint %}

{% hint style="info" %}
If at some point you would like to "remove' an image to free some space up, you can run the command:

 sharedcloud image clean --registry-path=&lt;registry\_path&gt;
{% endhint %}

{% hint style="warning" %}
**Important**: Always "download" and "clean" images using those commands. Otherwise, our servers won't be aware of this change, and you won't receive the right jobs.
{% endhint %}

## 5. Start the Instance

Ok, enough talking, it's time to run our instance!

```text
sharedcloud instance start
```

We should start seeing some text in our screen, something like:

```text
[INFO] Updating all downloaded images...
latest: Pulling from sharedcloud/web-crawling-python36
Digest: sha256:de9d5c8ccd4ef24842567ca2195f7a43609fda10dcfa5ebd67372f3ce466a4a0
Status: Image is up to date for sharedcloud/web-crawling-python36


[INFO] Ready to take Jobs...
```

This means that the instance is waiting to receive jobs from the dispatcher. Two conditions need to occur for this to happen:

1. **The "bid-price" and "ask-price" match.**
2. **The image required by the Job is already present in the instance.**

If both conditions apply, we should start seeing soon an output like this one:

```text
[INFO] 2 job/s arrived, please be patient...
[INFO] Starting Job 25dab85e-c6fc-45ce-90ff-c089a7e555aa...
[INFO] Starting Job ad7c78cd-766e-4051-9c2e-ce9d9ef6491a...
[INFO] All jobs were completed.
```

{% hint style="success" %}
Congratulations! We made some money today! To find out how much we made, head to the account details.
{% endhint %}

## 6. See Account Balance

```text
sharedcloud account list
```

```text
UUID                                  EMAIL              USERNAME    BALANCE    DATE_JOINED    LAST_LOGIN
------------------------------------  -----------------  ----------  ---------  -------------  ------------
49485391-3a73-42d8-87ee-466a170bc7a4  email@example.com  username    $0.20      2 days ago     2 days ago

```

Cool! Of course, depending on how long the jobs ran, and how much was the asking price, the amount would vary, but now we know how to process jobs :\)

{% hint style="danger" %}
Please, NEVER stop the server while jobs are being processed. You won't receive payment, and you might get penalized in the algorithm.
{% endhint %}



