# Computational Mathematics Software Manual

## Time comparisons between Sequential and Openmp for Eigenvalue Methods

### Power Method

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
250 x 250 | 0.0277161 | 0.005911
500 x 500 | 0.0723235 | 0.011149
750 x 750 | 0.125238 | 0.018288
1000 x 1000 | 0.196064 | 0.033149


### Inverse Power Method

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
250 x 250 | 0.0143384 | 0.002657
500 x 500 | 0.112427| 0.015137
750 x 750 | 0.259831 | 0.035132
1000 x 1000 | 0.464587 | 0.07633


