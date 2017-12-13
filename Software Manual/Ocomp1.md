# Computational Mathematics Software Manual

## Time comparisons between Sequential and Openmp for Matrix computations

### Matrix-Vector Multiplication

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
1000 x 1000 | 0.0082919 | 0.000566
2000 x 2000 | 0.0328024 | 0.002358
3000 x 3000 | 0.0816717 | 0.003528
4000 x 4000 | 0.130674 | 0.005687


### Matrix-Matrix Multiplication

Size of matrix | Sequential (sec) |  Openmp (sec)
------------ | ------------- | ------------- 
100 x 100 | 0.0121889 | 0.001169
200 x 200 | 0.163953 | 0.012191
300 x 300 | 0.387446 | 0.020388
400 x 400 | 0.996888 | 0.045458
500 x 500 | 2.20555 | 0.135809
600 x 600 | 3.8685 | 0.166779
700 x 700 | 6.28154 | 0.261312
800 x 800 | 10.1738 | 0.5056
900 x 900 | 14.6607 | 1.10345
1000 x 1000 | 46.9713 | 2.02393
