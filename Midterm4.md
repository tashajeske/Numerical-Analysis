**Problem 4:**  Chapter 5: Exercise 17 and 18

The program below solves tridiagonal systems of equations of size n. 

```C++
vector <double> tridiag(vector <double> subdiag, vector <double> maindiag, 
vector <double> supdiag, vector <double> b){
for (int i=0; i < subdiag.size(); i++){
double lik=subdiag[i]/maindiag[i];
//   subdiag[i]=subdiag[i]-lik*maindiag[i];
maindiag[i+1]=maindiag[i+1]-lik*supdiag[i];
b[i+1]=b[i+1]-lik*b[i];
}
for (int i = maindiag.size()-1; i>0; i--){
double lik2=supdiag[i-1]/maindiag[i];
//    supdiag[i-1]=supdiag[i-1]-lik2*maindiag[i];
//    maindiag]i-1]=maindiag[i-1]-lik*subdiag[i]
b[i-1]=b[i-1]-lik2*b[i];
}
vector <double> x;
for (int i=0; i < maindiag.size(); i++){
x.push_back(b[i]/maindiag[i]);
}
return x;
}
```

Below the program is tested on a matrix given in exercise 17 with an invented vector b.

```C++
void Printx(vector <double> vec1){
for (int i=0; i<vec1.size(); i++){
cout<< "x" << i << " = " << vec1[i] << endl;
}
cout << endl;
}
int main(){
Printx(tridiag({-1, -2, -3, -4, -5, -6, -7, -8, -9}, {3,6,9,12,15,18,21,24,27,30}, 
{-1, -2, -3, -4, -5, -6, -7, -8, -9}, {1,2,3,4,5,6,7,8,9,10}));
}
```

The output is below. 

```C++
x0 = 0.558733  
x1 = 0.6762  
x2 = 0.749233  
x3 = 0.796898  
x4 = 0.828771  
x5 = 0.848794  
x6 = 0.855739  
x7 = 0.839679  
x8 = 0.770265  
x9 = 0.564413  
```

Below the program is tested on the given boundary conditions for g  in exercise 18. 

```C++
//print vector v
void Printv(vector <double> vec1){
for (int i=0; i<vec1.size(); i++){
cout<< "v" << i+1 << " = " << vec1[i] << "  ";
}
cout << endl;
}

//returns max value for the VerrorInf function
double maxEntry (vector <double> vec){
double current=max(abs(vec[0]), abs(vec[1]));
for (int i=2; i < vec.size(); i++){
current=max(current, abs(vec[i]));
}
return current;
}

// from previous homework, finds vector infinity norm
double VerrorInf (vector <double> vec1,  vector <double> vec2){
vector <double> vecdiff;
for (int i=0; i<vec1.size(); i++){
vecdiff.push_back(vec1[i]-vec2[i]);
}
double maximum= maxEntry(vecdiff);
return maximum;
}

int main(){

vector <double> Asup;
vector <double> Asub;
for (int i=1; i<=99; i++){
Asup.push_back(-10000);
Asub.push_back(-10000);
}
vector <double> Adiag;
for (int i=1; i<=100; i++){
Adiag.push_back(20000);
}
vector <double> gvector;
for (double i=0; i<1; i+=.01){
double g=(pow(3.1415926535897932/2.0,2)*sin(3.1415926535897932/2.0*i));
gvector.push_back(g);
}
vector <double> vvector=tridiag(Asub, Adiag, Asup, gvector);
Printv(tridiag(Asub, Adiag, Asup, gvector));

vector <double> uvector;
for (int i=1; i<=100; i++){
double u=sin(3.1415926535897932/2.0*.01*i);
uvector.push_back(u);
}
cout<< "||U-V||_Inf = " << VerrorInf(uvector,vvector) << endl;
}
```

The VerrorInf and getmax functions were taken from a previous homework and the software manual entry for these routines are attached at the end of this problem. The output is below.

```C++
v1 = 0.00565093
v2 = 0.0113019
v3 = 0.0169489
v4 = 0.0225882
v5 = 0.0282159
v6 = 0.0338281
v7 = 0.0394209
v8 = 0.0449905
v9 = 0.050533
v10 = 0.0560446
v11 = 0.0615215
v12 = 0.0669597
v13 = 0.0723555
v14 = 0.0777051
v15 = 0.0830046
v16 = 0.0882504
v17 = 0.0934385
v18 = 0.0985652
v19 = 0.103627
v20 = 0.10862
v21 = 0.11354
v22 = 0.118384
v23 = 0.123148
v24 = 0.127829
v25 = 0.132422
v26 = 0.136924
v27 = 0.141332
v28 = 0.145642
v29 = 0.149851
v30 = 0.153954
v31 = 0.157949
v32 = 0.161832
v33 = 0.1656
v34 = 0.169248
v35 = 0.172775
v36 = 0.176175
v37 = 0.179447
v38 = 0.182587
v39 = 0.185591
v40 = 0.188456
v41 = 0.19118
v42 = 0.193758
v43 = 0.196189
v44 = 0.198468
v45 = 0.200593
v46 = 0.20256
v47 = 0.204368
v48 = 0.206012
v49 = 0.20749
v50 = 0.208799
v51 = 0.209937
v52 = 0.2109
v53 = 0.211685
v54 = 0.212291
v55 = 0.212715
v56 = 0.212953
v57 = 0.213004
v58 = 0.212865
v59 = 0.212533
v60 = 0.212006
v61 = 0.211282
v62 = 0.210358
v63 = 0.209232
v64 = 0.207902
v65 = 0.206366
v66 = 0.204622
v67 = 0.202667
v68 = 0.2005
v69 = 0.198119
v70 = 0.195521
v71 = 0.192706
v72 = 0.18967
v73 = 0.186413
v74 = 0.182933
v75 = 0.179228
v76 = 0.175296
v77 = 0.171136
v78 = 0.166747
v79 = 0.162127
v80 = 0.157275
v81 = 0.15219
v82 = 0.14687
v83 = 0.141314
v84 = 0.135521
v85 = 0.12949
v86 = 0.12322
v87 = 0.11671
v88 = 0.10996
v89 = 0.102967
v90 = 0.0957329
v91 = 0.0882552
v92 = 0.0805339
v93 = 0.0725683
v94 = 0.0643578
v95 = 0.0559022
v96 = 0.0472008
v97 = 0.0382535
v98 = 0.02906
v99 = 0.01962
v100 = 0.00993334

||U-V||_Inf = 0.990067
```
