# Create run

It creates a new run.

#### Example:

```
sharedcloud run create --function-uuid 79a31c33-397a-4921-8072-7f7e2c76da6c \
                       --parameters "((1, 2, 3), (4, 5, 6))" \
                       --bid-price 0.01 \
                      [--base-gpu-uuid b6fe7910-34f2-4473-aecb-f427fb3cced1]

```

#### Arguments:

* **function-uuid:** uuid of the function
* **parameters**: parameters of the run
* **bid-price**: maximum price the user is willing to pay \(per job and minute\)
* **base-gpu-uuid:** uuid of the minimum required GPU model for this this function \(Optional\)



