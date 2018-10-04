# Update instance

It updates a new instance

#### Example:

```
sharedcloud instance update --uuid <uuid_of_the_instance>
                            [--name my_instance] \
                            [--type cpu] \
                            [--ask-price 0.1]
                            [--max-num-parallel-jobs 2]
                            [--gpu-uuid b6fe7910-34f2-4473-aecb-f427fb3cced1]
```

#### Arguments:

* **uuid:** uuid of the instance
* **name:** name of the instance \(Optional\)
* **type**: type of the instance. It can be either "cpu" or "gpu" \(Optional\)
* **ask-price**: the minimum price that the instance owner is willing to accept \(Optional\)
* **max-num-parallel-jobs**: the max number of parallel jobs that can be run in the instance. _It can only be specified to CPU instances \(Optional\)_
* **gpu-uuid**: uuid of the gpu installed in the user's machine \(Optional\)

