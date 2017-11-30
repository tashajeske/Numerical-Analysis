# Computational Mathematics Software Manual

## **Routine Name:** DividedDiffTable

**Author:** Nitasha Jeske

**Language:** C++

**Description:** The Divided Difference Table routine calculates the coefficients of the polynomial on a subdiagonal of a matrix composed of the vectors x and y containing the data set and the divided differences needed to calculate the coefficients. 

**Input:**  Two vectors x and y representing the data set are inputs to the function.

**Output:**  The output is a vector with the coefficients of the polynomial.

**Example:**

```C++
// function to print vector
void Print(Vec x){
    for (int i=0; i<x.size(); i++){
        cout << x[i] << "  " ;
    }
    cout << endl;
}

// divide an interval from -1 to 1 n times
Vec x(int n){
    Vec x(n+1);
    for (int i=0; i<n+1; i++){
        x[i]=-1.0+2.0/n*i;
    }
    return x;
}

// Runge's phenomenon function
Vec func(Vec x){
    Vec y(x.size());
    for (int i=0; i<x.size(); i++){
        y[i]=1/(1+25*pow(x[i],2));
    }
    return y;
}

int main(){
    Print(DividedDiffTable({1,2,4},{1,3,3}));
    Print(DividedDiffTable(x(100),func(x(100))));
}
```

**Code:**
```C++
Vec DividedDiffTable (Vec x, Vec y){
    // initialize size n
    int n=(int)x.size();
    // initialize a vector of vectors to contain the data set and divided differences
    // there will be n rows in the table (i is 0:n) and n+1 columns
    Matrix difftable(n, Vec(n+1,0));
    // loop to add data set to first two columns of table
    for (int i=0; i<n; i++){
        difftable[i][0]=x[i];
        difftable[i][1]=y[i];
    }
    // loop to calculate divided differences for remainng columns
    // from column 2 and on (since first two columns are data set)
    for (int j=2; j<n+1; j++){
        // a counter k to know which divided difference order we are on
        for (int k=1; k<n; k++){
            // using previous values in table calculate higher order divided differences
            for (int i=k; i<n; i++){
                difftable[i][j]=(difftable[i][j-1]-difftable[i-1][j-1])/(difftable[i][0]-difftable[i-k][0]);
            }
        }
    }
    Vec coeff(n);
    // take the diagonal above the main diagonal and make a vector of coefficients
    for (int i=0; i<n; i++){
        coeff[i]=difftable[i][i+1];
    }
    // return this vector
    return coeff;
}
```

**And the output is as follows:**  
```
1  2  -0.666667
0.0384615  0.153846  0.432692  -0.707799  0.5441 
```

**Last Modification Date:**
Nov. 30, 2017
