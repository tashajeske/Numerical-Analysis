# Computational Mathematics Software Manual

## Time comparisons between Sequential and Openmp for Matrix computations

### Jacobi 

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
250 x 250 | 0.00446555 | 0.002146
500 x 500 | 0.0239598 | 0.004021
750 x 750 | 0.128437 | 0.008504
1000 x 1000 | 5.40632 | 0.310178


### Gauss-Seidel

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
250 x 250 | 0.00191135 | 0.000689
500 x 500 | 0.00957873| 0.001709
750 x 750 | 0.0271541 | 0.003873
1000 x 1000 | 0.0512795 | 0.007105


### Steepest Descent

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
250 x 250 | 0.00666693 | 0.002698
500 x 500 | 0.0325518 | 0.001738
750 x 750 | 0.0774018 | 0.004568
1000 x 1000 | 0.169234 | 0.006321


### Conjugage Gradient

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
250 x 250 | 0.00444091 | 0.000714
500 x 500 | 0.0170754 | 0.001083
750 x 750 | 0.0388337 | 0.001508
1000 x 1000 | 0.0682001 | 0.002411
