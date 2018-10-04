# How to run a tensorflow script in a GPU instance

{% hint style="info" %}
It's strongly recommended to have a look first at the "Getting Started" guide, as some concepts are not going to be explained in detail here.
{% endhint %}

## Creating the function

1\) ****Create a new python file where we'll write the code in:

```
$ touch mnist.py
```

2\) Now, just place the following code inside:

{% code-tabs %}
{% code-tabs-item title="mnist.py" %}
```python
import tensorflow as tf


def handler(event):
    tf.logging.set_verbosity(tf.logging.INFO)
    p1 = int(event[0])
    p2 = float(event[1])
    p3 = int(event[2])
    p4 = int(event[3])
    mnist = tf.keras.datasets.mnist

    (x_train, y_train),(x_test, y_test) = mnist.load_data()
    x_train, x_test = x_train / 255.0, x_test / 255.0

    model = tf.keras.models.Sequential([
      tf.keras.layers.Flatten(),
      tf.keras.layers.Dense(p1, activation=tf.nn.relu),
      tf.keras.layers.Dropout(p2),
      tf.keras.layers.Dense(p3, activation=tf.nn.softmax)
    ])
    model.compile(optimizer='adam',
                  loss='sparse_categorical_crossentropy',
                  metrics=['accuracy'])
    tf.logging.info(model.fit(x_train, y_train, epochs=p4))
    e = model.evaluate(x_test, y_test)
    tf.logging.info(e)
    return e[-1]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% hint style="info" %}
 Pay attention to the name of the function: "**handler**", and the name of the arguments: "**event**".  Every function you create **MUST** use the same name conventions in the signature or otherwise won't be processed properly.
{% endhint %}

{% hint style="info" %}
Learning **Tensorflow** is out of the scope of this tutorial, but if you feel curious, you can learn about this great library here: [https://www.tensorflow.org/tutorials/](https://www.tensorflow.org/tutorials/)
{% endhint %}

3\) Great, lets log in now using the **Sharedcloud CLI** tool:

```text
sharedcloud login --username <your_username> --password <your_password>
```

4\) Now it's when things start getting interesting. As this function requires a GPU, it's important to provide now a "GPU ready" image. Let's list all the images again:

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

If we look at the "**REQUIRES\_GPU**" column, we can see which images are "GPU ready" or not. In this case, we use **Python36** and **Tensorflow**, so the second image seems like a perfect fit. Paste its UUID in the **"--image-uuid"** argument

```text
sharedcloud function create --name mnist \
                            --file mnist.py \
                            --image-uuid 23ca880b-94fe-472c-b9cf-934ed8295872
```

5\) Ok! Now you can see you function with the cli:

```bash
sharedcloud function list
```

```text
UUID                                  NAME         IMAGE                                         NUM_RUNS  WHEN
------------------------------------  -----------  ----------------------------------------    ----------  --------------
4aef65f8-a406-4660-8025-fd660599c83e  mnist        sharedcloud/tensorflow-gpu-python36:latest           0  11 seconds ago
```

6\) The next step would be to define the run. As we explain previously, a run is a configuration object that we can use to specify different things like the list of arguments that we want to pass to the function. Additionally, a pretty interesting feature is the possibility of specifying the "base" GPU that we would like to use. With "base GPU" we refer to minimum GPU that this function will need to be able to run successfully.

For example, if your function trains a neural network with many layers, you might want to select a GPU with plenty of GBs or RAM, otherwise your function might not finish well...

For listing all the GPUs available in a precise point of time, just run:

```text
sharedcloud gpu list
```

```text
UUID                                  NAME                   CODENAME      CUDA_CORES  IS_AVAILABLE
------------------------------------  ---------------------  ----------  ------------  --------------
caf0daeb-ba23-4499-b4f9-8b4965714366  Nvidia Titan V 12GB    titanv              5120  Yes
f856b76d-557c-43a7-a072-b6e1df71fd40  Nvidia Tesla K80 24GB  teslak80            4992  Yes
536457fd-634f-46dd-96d0-009c73d5ca5c  Nvidia Titan Xp 12GB   titanxp             3840  No
6107ee43-9ee1-4180-8d3d-0bef1c450847  Nvidia 1080 ti 11GB    1080_ti             3584  No
0b4a3f93-9e0e-40d6-915a-359d07556035  Nvidia Titan X 12GB    titanx              3072  Yes
13d6e1a2-3151-46c7-9420-3a5b2688ba06  Nvidia 1080 8GB        1080                2560  Yes
56380b69-30eb-43d0-bcc0-e4b5a2b50955  Nvidia 1070 8GB        1070                1920  No
d220b51d-569c-40de-a290-097f6781397f  Nvidia 1060 6GB        1060                1280  No

```

How lucky we are! The **Nvidia Titan V** seems to be available in the market, let's try to bid for that one!

```text
sharedcloud run create --function-uuid 4aef65f8-a406-4660-8025-fd660599c83e \
                       --parameters "((512, 0.2, 10, 2), (512, 0.2, 10, 3))" \
                       --bid-price 0.05 \
                       --gpu-uuid caf0daeb-ba23-4499-b4f9-8b4965714366
```

{% hint style="info" %}
Some interesting things from the last command:

1. The "**--parameters**" argument NEEDS to always be a tuple of tuple. The reason is simple. Each tuple is going to be passed to the function we defined previously, so we want to support passing several arguments e.g., \(\(1, 2, 3\),\)
2. The "**--bid-price**" argument represents the maximum amount of money \(in dollars\) that you would like to pay for each job, each minute. For example, "0.1" means that if I have 2 jobs, and each task takes 5 minutes, I would pay "0.05 \* 2 \* 5" = $0.5
{% endhint %}

6\) As we saw in the "Getting Started" guide, this created as many jobs as many internal tuples has the **"--parameters"** argument \(2 in this case!\) Let's see how they would be applied to our function:

{% code-tabs %}
{% code-tabs-item title="JOB 1" %}
```text
import tensorflow as tf


def handler(event):
    tf.logging.set_verbosity(tf.logging.INFO)
    p1 = int("512") # <----
    p2 = float("0.2") # <----
    p3 = int("10") # <----
    p4 = int("2") # <----
    mnist = tf.keras.datasets.mnist

    (x_train, y_train),(x_test, y_test) = mnist.load_data()
    x_train, x_test = x_train / 255.0, x_test / 255.0

    model = tf.keras.models.Sequential([
      tf.keras.layers.Flatten(),
      tf.keras.layers.Dense(p1, activation=tf.nn.relu),
      tf.keras.layers.Dropout(p2),
      tf.keras.layers.Dense(p3, activation=tf.nn.softmax)
    ])
    model.compile(optimizer='adam',
                  loss='sparse_categorical_crossentropy',
                  metrics=['accuracy'])
    tf.logging.info(model.fit(x_train, y_train, epochs=p4))
    e = model.evaluate(x_test, y_test)
    tf.logging.info(e)
    return e[-1]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="JOB 2" %}
```text
import tensorflow as tf


def handler(event):
    tf.logging.set_verbosity(tf.logging.INFO)
    p1 = int("512") # <----
    p2 = float("0.2") # <----
    p3 = int("10") # <----
    p4 = int("3") # <----
    mnist = tf.keras.datasets.mnist

    (x_train, y_train),(x_test, y_test) = mnist.load_data()
    x_train, x_test = x_train / 255.0, x_test / 255.0

    model = tf.keras.models.Sequential([
      tf.keras.layers.Flatten(),
      tf.keras.layers.Dense(p1, activation=tf.nn.relu),
      tf.keras.layers.Dropout(p2),
      tf.keras.layers.Dense(p3, activation=tf.nn.softmax)
    ])
    model.compile(optimizer='adam',
                  loss='sparse_categorical_crossentropy',
                  metrics=['accuracy'])
    tf.logging.info(model.fit(x_train, y_train, epochs=p4))
    e = model.evaluate(x_test, y_test)
    tf.logging.info(e)
    return e[-1]
```
{% endcode-tabs-item %}
{% endcode-tabs %}

8\) Alright, let's see now how our jobs are doing:

```text
sharedcloud job list
```

```text
UUID                                    ID  STATUS    COST    DURATION    WHEN            RUN_UUID                              FUNCTION
------------------------------------  ----  --------  ------  ----------  --------------  ------------------------------------  -----------
fd68a431-ff23-4176-aba6-982d428aaab0     1  CREATED   $0.000              9 minutes ago  49485391-3a73-42d8-87ee-466a170bc7a4   mnist
4e49e9fe-e5bd-4259-af18-dbfb04ec4bfe     0  CREATED   $0.000              9 minutes ago  49485391-3a73-42d8-87ee-466a170bc7a4   mnist

```

9\) After a few seconds, if the "bid-price" we provided gets matched with the Titan V user's "ask-price", we should see how our Jobs were successfully completed:

```text
UUID                                    ID  STATUS      COST    DURATION       WHEN            RUN_UUID                              FUNCTION
------------------------------------  ----  ---------   ------  ------------   --------------  ------------------------------------  -----------
fd68a431-ff23-4176-aba6-982d428aaab0     1  SUCCEEDED   $0.05   60 second/s    12 minutes ago  49485391-3a73-42d8-87ee-466a170bc7a4  mnist
4e49e9fe-e5bd-4259-af18-dbfb04ec4bfe     0  SUCCEEDED   $0.05   60 second/s    12 minutes ago  49485391-3a73-42d8-87ee-466a170bc7a4  mnist
```

10\) Finally, as we explained in the previous guide, to inspect the results, we can use the following sub-commands:

```text
sharedcloud job stdout --uuid fd68a431-ff23-4176-aba6-982d428aaab0
```

```text
>>> Downloading data from https://storage.googleapis.com/tensorflow/tf-keras-datasets/mnist.npz

    8192/11490434 [..............................] - ETA: 1s
  663552/11490434 [>.............................] - ETA: 0s
 3891200/11490434 [=========>....................] - ETA: 0s
 6987776/11490434 [=================>............] - ETA: 0s
10387456/11490434 [==========================>...] - ETA: 0s
11493376/11490434 [==============================] - 0s 0us/step
Epoch 1/2

   32/60000 [..............................] - ETA: 1:48:04 - loss: 2.2662 - acc: 0.0938
  512/60000 [..............................] - ETA: 6:48 - loss: 1.5624 - acc: 0.5176   
  992/60000 [..............................] - ETA: 3:32 - loss: 1.1609 - acc: 0.6532
 1472/60000 [..............................] - ETA: 2:23 - loss: 0.9847 - acc: 0.7045
 
 ......
 
59136/60000 [============================>.] - ETA: 0s - loss: 0.2194 - acc: 0.9357
59520/60000 [============================>.] - ETA: 0s - loss: 0.2186 - acc: 0.9359
59904/60000 [============================>.] - ETA: 0s - loss: 0.2180 - acc: 0.9360
60000/60000 [==============================] - 12s 198us/step - loss: 0.2179 - acc: 0.9361
Epoch 2/2

   32/60000 [..............................] - ETA: 13s - loss: 0.0633 - acc: 0.9688
  416/60000 [..............................] - ETA: 8s - loss: 0.0968 - acc: 0.9736 
  768/60000 [..............................] - ETA: 8s - loss: 0.0934 - acc: 0.9753
 1152/60000 [..............................] - ETA: 8s - loss: 0.0961 - acc: 0.9740

.......

58848/60000 [============================>.] - ETA: 0s - loss: 0.0970 - acc: 0.9708
59200/60000 [============================>.] - ETA: 0s - loss: 0.0971 - acc: 0.9708
59584/60000 [============================>.] - ETA: 0s - loss: 0.0968 - acc: 0.9709
59936/60000 [============================>.] - ETA: 0s - loss: 0.0965 - acc: 0.9709
60000/60000 [==============================] - 9s 142us/step - loss: 0.0966 - acc: 0.9709

```

```text
sharedcloud job stderr --uuid fd68a431-ff23-4176-aba6-982d428aaab0
```

```text
>>> 2018-09-27 09:44:54.246714: I tensorflow/core/platform/cpu_feature_guard.cc:141] Your CPU supports instructions that this TensorFlow binary was not compiled to use: AVX2 FMA
2018-09-27 09:44:56.963483: I tensorflow/stream_executor/cuda/cuda_gpu_executor.cc:897] successful NUMA node read from SysFS had negative value (-1), but there must be at least one NUMA node, so returning NUMA node zero
2018-09-27 09:44:56.964435: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1405] Found device 0 with properties: 
name: Tesla K80 major: 3 minor: 7 memoryClockRate(GHz): 0.8235
pciBusID: 0000:00:1e.0
totalMemory: 11.17GiB freeMemory: 11.04GiB
2018-09-27 09:44:56.964478: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1484] Adding visible gpu devices: 0
2018-09-27 09:44:57.281495: I tensorflow/core/common_runtime/gpu/gpu_device.cc:965] Device interconnect StreamExecutor with strength 1 edge matrix:
2018-09-27 09:44:57.281542: I tensorflow/core/common_runtime/gpu/gpu_device.cc:971]      0 
2018-09-27 09:44:57.281558: I tensorflow/core/common_runtime/gpu/gpu_device.cc:984] 0:   N 
2018-09-27 09:44:57.291336: I tensorflow/core/common_runtime/gpu/gpu_device.cc:1097] Created TensorFlow device (/job:localhost/replica:0/task:0/device:GPU:0 with 335 MB memory) -> physical GPU (device: 0, name: Tesla K80, pci bus id: 0000:00:1e.0, compute capability: 3.7)
INFO:tensorflow:<tensorflow.python.keras.callbacks.History object at 0x7f62678830b8>
INFO:tensorflow:[0.09256454129191115, 0.9723]
```

```text
sharedcloud job result --uuid 14804287-76d0-4113-9fc9-6114ca17b098
```

```text
>>> 0.9723  # This is the final accuracy that our model achieved
```

{% hint style="success" %}
That's it! We just trained our first neural network model using Tensorflow and Sharedcloud!
{% endhint %}



