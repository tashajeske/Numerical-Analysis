# Computational Mathematics Software Manual

## **Routine Name:** OMPmatrixmatrix

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The matrix matrix function takes the product of two matrices by applying the dot product for each of the rows in the first matrix paired with each column in the second matrix. This routine is coded to run in Open MP on multiple processors in order to speed up the computing time. 

**Input:**  The input is two vectors of vectors of doubles, or technically two matrices.

**Output:** The routine provides a vector of vector of doubles which has the dot product values as the entries, and prints out the time it takes to compute the resulting matrix.

**Code:**
```C++
Matrix OMPmatrixmatrix (Matrix matrix1, Matrix matrix2){
    Matrix prod(matrix1[0].size(), Vec (matrix2.size(),1));
    chrono::duration<double> time2;
    auto start = chrono::high_resolution_clock::now();
    for (int i=0; i<prod.size(); i++){
        for (int j=0; j<prod[i].size(); j++){
            prod[i][j]=0.0;
        }
    }
    # pragma omp parallel for
    for (int i=0; i<matrix1.size();i++){
        for (int j=0; j<matrix2[i].size(); j++){
            for (int k=0; k<matrix1[0].size(); k++){
                prod[i][j]+=matrix1[i][k]*matrix2[k][j];
            }
            //   cout << prod[i][j] << "  ";
        }
        //  cout << endl;
    }
    auto end = chrono::high_resolution_clock::now();
    time2 = end-start;
    cout<<time2.count() <<endl;
    return prod;
}
```
**Example:**
```C++
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

int main(){
    OMPmatrixmatrix(initMatrix(2000, 2000), initMatrix(2000, 2000));
}
```

**Results:**  
```
20.7922
```

**Last Modification Date:** Oct. 18, 2017
