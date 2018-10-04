# FAQ

## Who can join?

Anyone! Just wait a bit, we are currently in Beta phase :\) If you would like to help out by testing the platform let us know by filling in the form in the front page.

## What does FaaS mean?

FaaS is the acronym of "function as a Service". According to Wikipedia: 

"**Function as a service** \(FaaS\) _is a category of cloud computing services that provides a platform allowing customers to develop, run, and manage application functionalities without the complexity of building and maintaining the infrastructure typically associated with developing and launching an app._"

In short, this paradigm allows you to expose functions for later use. Think of it as if we were assigning a different URL to each function. Therefore, if we wish to run any of those functions, we can do it by just calling to that endpoint and provide the inputs \(arguments\) that the function expects.

Not only this approach allows you to process abundantly amount of data at a minimal cost, but also simplifies the communication between services greatly, as the inputs and outputs of each function are perfectly defined.

## How is Sharedcloud similar to the Stockmarket?

In the Stockmarket you have people who want to buy stocks and people who want  to sell stocks \(it's a bit more complicated than that, but you get the idea\).

A transaction is made when a buyer offers a price \("bid-price"\) that is equal or bigger to the price a seller is asking for \("ask-price"\).

Now consider a buyer as the user who wants to "run a function" and the seller as the user who wants to "share the computing power." Like in the Stockmarket, both the buyer and the seller needs to agree at the price for a transaction to occur. This is why believe that both systems share a fair bit of similarities.

## What type of functions can I create?

Any code can be inside your functions, so any kind, really. Having said that, if you use third party libraries, please make sure to choose an image that includes them, otherwise those libraries might not be available for your function.

## What runtimes can I use for my functions?

As of today, we support Python3.6, Python2.7 and Node.js \(version 8\)

## How much should I set my "bid-price"?

It all depends on how much is your budget, how many parallel Jobs you are running and how long you estimate that each Job is going to take. In a few words, the "bid-price" represents the amount of American dollars that a buyer is willing to pay per job and per minute. So this would be one way to estimate our "bid-price" based on our budget:

_Let's say that your budget is $1 and that you would like to run 10 Jobs in parallel. You estimate that each Job is going to take around 5 minutes, so by doing some maths we can find a good "bid-price": $1 / \(10\*5\) = $0.02_

That's the amount that you should put as your "bid-price". Keep in mind, however, that the total amount of money that you will pay in the end might be bigger than your budget if the Jobs end up taking longer time than the 5 minutes we estimated. This is why it's a good practice to reduce the "bid-price" a few cents to have some room for such cases.

## What type of machines can I share resources from?

We currently support both "Standard/CPU" instances \(e.g., laptops, desktop computers...\) and "GPU" instances \(e.g., gaming computers, mining stations...\)

Please see below the conditions to be eligible.

## What machines are eligible to share their computing power?

In order to guarantee that Jobs are going to be successfully processed, we only accept machines that have at least 8GB RAM and at least 30GB of free disk. Please keep in mind that the CLI is not going to necessarily use all that amount of disk space, is just a safety range to avoid interruptions while processing Jobs.

GPU machines have some special requirements at this time. We only support Nvidia GPUs not older than the GTX 10 Series. If your GPU doesn't qualify, please be patient, we plan to extend the number of supported GPUs in the future.

 Said that, we recommend you double-check with us in case of doubt. 

## What instance "type" should I choose?

That's entirely up to you! However, if you have an eligible GPU, we recommend you chose the "GPU" type for the bigger profit that you might end up making \(users tend to pay more for GPU usage\). Please keep in mind though, that you can only have one active instance per computer.

## How much should I set my "ask-price"? {#how-much-should-i-set-my-bid-price}

It depends on how much money you would like to make out of your machine. In a few words, the "ask-price" represents the amount of American dollars that a seller would like to receive per job and per minute. Here comes an example:

_Let's imagine that you have processed 10 jobs today, and that each took 5 minutes. Previously, you had set an "ask-price" of $0.005.  Therefore, in that time, you would have made: $0.005 \* 10 \* 5 = $0_.25

Some things to keep in mind:

* Jobs will get dispatched to your instance ONLY if the buyer's "bid-price" matches with the "ask-price". Because of this, we recommend that the "ask-price" is not set too high. In case of doubt you can ask us and we can give your some price estimations.
* Users tend to pay much more for GPU instances. Be aware of this while setting your "ask-price". If you don't have a GPU instance it's probably a good idea to be realistic and set a low "ask-price" in the beginning.

