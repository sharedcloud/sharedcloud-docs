# Create instance

It creates a new instance

#### Example:

```
sharedcloud instance create --name my_instance \
                            --type cpu \
                            --ask-price 0.1
                            [--max-num-parallel-jobs 2]
                            [--gpu-uuid b6fe7910-34f2-4473-aecb-f427fb3cced1]
```

#### Arguments:

* **name:** name of the instance
* **type**: type of the instance. It can be either "cpu" or "gpu"
* **ask-price**: the minimum price that the instance owner is willing to accept
* **max-num-parallel-jobs**: the max number of parallel jobs that can be run in the instance. _It can only be specified to CPU instances \(Defaults to 1\)_
* **gpu-uuid**: uuid of the gpu installed in the user's machine \(Only required for GPU instances\)



