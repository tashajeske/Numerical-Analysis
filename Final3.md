# Math 4610 Take Home Final

## Nitasha Jeske

## Problem 3:

**Use power method code to verify the results of example 8.2 in the text and compute smallest/largest eigenvalues**

Using routines from previous homework assignments, the absolute error for each iteration of the power method has been recorded (see results section below) for both matrix A and matrix B described in example 8.2. A plot has been attached behind this page that shows a comparison of the two matrices and their convergence (as absolute error decreases). This verifies what we find in the text. When the entry 31 is changed to be 30, the iterations converge to an approximate solution faster. 

The code below also calculates the largest eigenvalues (using power method) and the least eigenvalues (using inverse power method). We see for Matrix A the largest eigenvalue is 31.9986 and tle least eigenvalue is 1.00003. Then for Matrix B the largest eigenvalue is 31.9993 and the least eigenvalue is 1.00003.

Example:
```C++
int main(){
    int n=32;
    Matrix A(n, Vec (n,0));
    Matrix B(n, Vec (n,0));
    for (int i=0; i<n; i++){
        A[i][i]=i+1;
    }
    for (int i=0; i<n; i++){
        if (i==30) B[i][i]=30;
        else B[i][i]=i+1;
    }
    Vec v0(n,1);
    cout << powerM(A,v0, .0001, 1000) << endl;
    cout << powerM(B,v0, .0001, 1000) << endl;
    cout << invPowerM(A,v0, .0001, 1000) << endl << endl;
    cout << invPowerM(B,v0, .0001, 1000) << endl;
}
```

Results: 
```C++
k = 1: 7.63077
k = 2: 4.92735
k = 3: 3.57821
k = 4: 2.77076
k = 5: 2.23417
k = 6: 1.85235
k = 7: 1.56724
k = 8: 1.34662
k = 9: 1.17112
k = 10: 1.02844
k = 11: 0.910371
k = 12: 0.811219
k = 13: 0.726928
k = 14: 0.654521
k = 15: 0.591763
k = 16: 0.536945
k = 17: 0.488737
k = 18: 0.446092
k = 19: 0.408167
k = 20: 0.374283
k = 21: 0.343883
k = 22: 0.316506
k = 23: 0.29177
k = 24: 0.269351
k = 25: 0.248976
k = 26: 0.230414
k = 27: 0.213464
k = 28: 0.197954
k = 29: 0.183735
k = 30: 0.170677
k = 31: 0.158666
k = 32: 0.147602
k = 33: 0.137397
k = 34: 0.127972
k = 35: 0.119258
k = 36: 0.111193
k = 37: 0.10372
k = 38: 0.0967912
k = 39: 0.0903606
k = 40: 0.084388
k = 41: 0.0788368
k = 42: 0.0736738
k = 43: 0.0688689
k = 44: 0.0643948
k = 45: 0.0602264
k = 46: 0.056341
k = 47: 0.0527176
k = 48: 0.0493372
k = 49: 0.0461822
k = 50: 0.0432365
k = 51: 0.0404852
k = 52: 0.0379148
k = 53: 0.0355125
k = 54: 0.0332669
k = 55: 0.031167
k = 56: 0.029203
k = 57: 0.0273657
k = 58: 0.0256465
k = 59: 0.0240375
k = 60: 0.0225314
k = 61: 0.0211214
k = 62: 0.0198011
k = 63: 0.0185646
k = 64: 0.0174065
k = 65: 0.0163216
k = 66: 0.0153052
k = 67: 0.0143528
k = 68: 0.0134604
k = 69: 0.0126241
k = 70: 0.0118402
k = 71: 0.0111054
k = 72: 0.0104167
k = 73: 0.00977097
k = 74: 0.0091656
k = 75: 0.00859799
k = 76: 0.00806576
k = 77: 0.00756668
k = 78: 0.00709866
k = 79: 0.00665974
k = 80: 0.00624809
k = 81: 0.00586201
k = 82: 0.00549989
k = 83: 0.00516023
k = 84: 0.00484163
k = 85: 0.00454277
k = 86: 0.00426241
k = 87: 0.00399942
k = 88: 0.00375269
k = 89: 0.00352123
k = 90: 0.00330408
k = 91: 0.00310036
k = 92: 0.00290922
k = 93: 0.00272989
k = 94: 0.00256164
k = 95: 0.00240378
k = 96: 0.00225566
k = 97: 0.00211668
k = 98: 0.00198628
k = 99: 0.00186392
k = 100: 0.00174911
k = 101: 0.00164138
k = 102: 0.00154029
k = 103: 0.00144543
0.00751107
31.9986
k = 1: 7.74541
k = 2: 5.10342
k = 3: 3.79271
k = 4: 3.00519
k = 5: 2.47419
k = 6: 2.0871
k = 7: 1.78873
k = 8: 1.54918
k = 9: 1.35102
k = 10: 1.1835
k = 11: 1.03966
k = 12: 0.914811
k = 13: 0.805631
k = 14: 0.709692
k = 15: 0.62514
k = 16: 0.550501
k = 17: 0.484567
k = 18: 0.42632
k = 19: 0.374881
k = 20: 0.329481
k = 21: 0.289442
k = 22: 0.254158
k = 23: 0.22309
k = 24: 0.195754
k = 25: 0.171719
k = 26: 0.150601
k = 27: 0.132055
k = 28: 0.115777
k = 29: 0.101494
k = 30: 0.0889676
k = 31: 0.0779838
k = 32: 0.068355
k = 33: 0.0599154
k = 34: 0.0525192
k = 35: 0.0460379
k = 36: 0.0403586
k = 37: 0.0353821
k = 38: 0.0310215
k = 39: 0.0272004
k = 40: 0.023852
k = 41: 0.0209175
k = 42: 0.0183457
k = 43: 0.0160915
k = 44: 0.0141155
k = 45: 0.0123833
k = 46: 0.0108646
k = 47: 0.00953294
k = 48: 0.00836521
k = 49: 0.00734112
k = 50: 0.0064429
k = 51: 0.00565501
k = 52: 0.00496384
k = 53: 0.00435745
k = 54: 0.00382539
k = 55: 0.00335852
k = 56: 0.0029488
k = 57: 0.00258922
k = 58: 0.00227362
k = 59: 0.00199659
k = 60: 0.0017534
k = 61: 0.00153991
k = 62: 0.00135247
k = 63: 0.0011879
k = 64: 0.0010434
k = 65: 0.000916506
k = 66: 0.000805076
k = 67: 0.000707217
0.0373761
31.9993
1.00003
1.00003
```
