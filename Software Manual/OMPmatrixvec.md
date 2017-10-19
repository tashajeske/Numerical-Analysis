# Computational Mathematics Software Manual

## **Routine Name:** OMPmatrixvec

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The matrix vector function multiplies a matrix by a vector by running through a nested for loop and in simple terms calculates the dot product for each row in the matrix. This routine is coded to run in Open MP on multiple processors in order to speed up the computing time. 

**Input:**  The input is a vector of vector of doubles, which is a matrix, and a vector of doubles.

**Output:** The routine provides a vector of type double with the dimensions: rows of matrix x 1, and prints out the time it takes to compute the vector.

**Examplet:**
```C++
int main(){
typedef vector <vector <double>> Matrix;
typedef vector <double> Vec;
Matrix initMatrix (int row, int col){
Matrix randmatrix (row, vector <double> (col));
for (int i=0; i<row; i++){
for (int j=0; j<col; j++){
randmatrix[i][j]=rand()%50;
}
}
return randmatrix;
}
Vec initVector (int col){
Vec randvector (col);
for (int i=0; i<col; i++){
randvector[i]=rand()%50;
}
return randvector;
}
OMPmatrixvec(initMatrix(2000, 2000), initVector(2000));
}
```

**Code:**
```C++
Vec OMPmatrixvec (Matrix matrix, Vec vec){
Vec prod;
chrono::duration<double> time1;
auto start = chrono::high_resolution_clock::now();
for (int i=0; i<matrix[0].size(); i++){
prod.push_back(0);
}
# pragma omp parallel for
for (int i=0; i<matrix.size(); i++){
for (int j=0; j< vec.size(); j++){
prod[i]+=matrix[i][j]*vec[j];
}
}
auto end = chrono::high_resolution_clock::now();
time1 = end-start;
cout<<time1.count() <<endl;
return prod;
}
```

**And the output is as follows:**  
```
0.002455  
```

**Last Modification Date:**
Oct. 18, 2017
