
**Problem 2:**  Chapter 4: Exercise 5 and 7

Below is a counterexample for the statement in exercise 5. The routines, Mnorm1 and MnormInf, are taken from a previous homework assingmetn and used to compute the norms for a matrix A. The software manual entries for these routines can be found attached at the end of this problem. 

```C++
double Mnorm1 (vector<vector<double>> matrix){
double norm=0.0;
for (int i=0; i<matrix.size(); i++){
double sum=0.0;
for (int j=0; j< matrix[i].size(); j++){
sum+=abs(matrix[j][i]);
}
if (sum > norm) norm = sum;
}
return norm;
}



double MnormInf (vector<vector<double>> matrix){
double norm=0.0;
for (int i=0; i<matrix.size(); i++){
double sum=0.0;
for (int j=0; j< matrix[i].size(); j++){
sum+=abs(matrix[i][j]);
}
if (sum > norm) norm = sum;
}
return norm;
}

int main(){
// (1 Norm of A)^-1
cout<< "||A||_1 ^-1 = " << pow(Mnorm1({{1,2},{3,4}}),-1) << endl;
// 1 Norm of A^-1
cout << "||A^-1||_1 = " << Mnorm1({{-2, 1}, {1.5, -.5}}) << endl;
// (Inf Norm of A)^-1
cout << "||A||_Inf ^-1 = " << pow(MnormInf({{1,2},{3,4}}), -1) << endl;
// Inf Norm of A^-1
cout << "||A^-1||_Inf = " << MnormInf({{-2, 1}, {1.5, -.5}}) << endl;
}
```

The output to the code is:

```C++
||A||_1 ^-1 = 0.166667
||A^-1||_1 = 3.5
||A||_Inf ^-1 = 0.142857
||A^-1||_Inf = 3
```

Clearly, 0.166667 is not equal to 3.5 and 0.142857 is not equal to 3. Thus, we have found a counterexample for the statement proving it to be false. An analytical proof can be found on the next page. 




