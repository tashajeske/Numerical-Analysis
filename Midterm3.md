**Problem 3:**  Chapter 5: Exercise 2

The program below uses the Gauss-Jordan method to solve the matrix for a given b.

```C++
vector <double> GaussJordan(Matrix matrix1, vector <double> b){
// flopsCnt will tell us how many floating point operations there are in the routine for given matrix and vector
int flopsCnt=0;
// this set of for loops performs Gauss-elimination
for (int k=0; k<matrix1.size()-1; k++){
for(int i=k+1; i<matrix1.size(); i++){
double lik=matrix1[i][k]/matrix1[k][k];
flopsCnt++;
// does not worry about the lower diagonals, we know they go to zero we won't make the computer do it
for (int j=k+1; j<matrix1[0].size(); j++){
matrix1[i][j]=matrix1[i][j]-lik*matrix1[k][j];
flopsCnt+=2;
}
// since we augment b, perform the row operations on b vector also
b[i]=b[i]-lik*b[k];
flopsCnt+=2;
}
}
cout << "Gauss Elimination flops count = " << flopsCnt << endl;
// this for loop performs gauss-jordan and reduces the matrix to a diagonal
for (int k=matrix1.size()-1; k>0; k--){
for (int i=k-1; i>=0; i--){
double lik2=matrix1[i][k]/matrix1[k][k];
flopsCnt++;
// we only perform the operation on the b vector because we know the upper diag is now zero
b[i]=b[i]-lik2*b[k];
flopsCnt+=2;
// cout << b[i] << "  ";
}
}
cout << "Gauss-Jordan flops count = " << flopsCnt << endl;

// x_i=b_i/a_i,i since the matrix is diagonal
vector <double> x;
for (int i=0; i<b.size(); i++){
x.push_back(b[i]/matrix1[i][i]);
}
return x;
}
```

Then the program is tested using the following matrix and vector b.

```C++
void Printx(vector <double> vec1){
for (int i=0; i<vec1.size(); i++){
cout<< "x" << i << " = " << vec1[i] << "  ";
}
cout << endl;
}

int main(){
Matrix matrix1={{1,2.0,3}, {2,3,2},{-1,0,0}};
vector<double> b1={1.0,0,-4};
Printx(GaussJordan(matrix1,b1));
}
```

The output is recorded below. It shows the number of floating point operations for the Gaussian elimination part and for the Gauss-Jordan. 

```C++
Gauss Elimination flops count = 19
Gauss-Jordan flops count = 28
x0 = 4  x1 = -3.6  x2 = 1.4  
```

This code fits the required n^3 + O(n^2) floating point operations. The floating point operations are roughly 50% more for the Gauss-Jordan than just the Gauss-elimination. 

 

