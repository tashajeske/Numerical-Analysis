# Math 4610 Take Home Final

## Nitasha Jeske

## Problem 6:

**#10 on page 326**

Proposed algorithm:

```C++
interpolate ( vector <double> x, vector <double> y, double discontinuity_allowance){
    for(int i=0; i<137; i++){
        if (i==0){
            vector <double> chosen_points={x[0], x[1], x[2], x[3]};
            vector <double> y_points={y[0], y[1], y[2], y[3]};
            // check to see if there are any gaps in this new vector
            for (int k=0; k<3; k++){
                if (abs(chosen_points[k]-chosen_points[k+1])>discontinuity_allowance){
                cout<<"Error: Discontinuity in interval. Not enough points to interpolate interval." << endl;
                }
            }
            // call an interpolation function given the points
            interpolate(chosen_points, y_points);
        }
        if (abs(chosen_points[k]-chosen_points[k+1])>discontinuity_allowance){
            // check to see if i is large enough to have three values prior to it
            if (i<=3) cout << "Error: Not enough points to interpolate interval." << endl;
            vector <double> chosen_points={x[i], x[i-1], x[i-2], x[i-3]};
            vector <double> y_points={y[i], y[i-1], y[i-2], y[i-3]};
            // check to see if there are any gaps in this new vector
            for (int k=0; k<3; k++){
                if (abs(chosen_points[k]-chosen_points[k+1])>discontinuity_allowance){
                    cout<<"Error: Discontinuity in interval. Not enough points to interpolate interval." << endl;
                }
            }
            // check to see if the left end point exists in the chosen points
            for (int k=1; k<=3; k++){
                if (
            // call an interpolation function given the points
            interpolate(chosen_points, y_points);
        }
        if (abs(chosen_points[k]-chosen_points[k-1])>discontinuity_allowance){
            // check to see if i is small enough to have three values after it
            if (i>=134) cout << "Error: Not enough points to interpolate interval." << endl;
            vector <double> chosen_points={x[i], x[i+1], x[i+2], x[i+3]};
            vector <double> y_points={y0, y1, y2, y3};
            // check to see if there are any gaps in this new vector
            for (int k=0; k<3; k++){
                if (abs(chosen_points[k]-chosen_points[k+1])>discontinuity_allowance){
                    cout<<"Error: Discontinuity in interval. Not enough points to interpolate interval." << endl;
                }
            }
            // call an interpolation function given the points
            interpolate(chosen_points, y_points);
        }
        if (i==136){
            vector <double> chosen_points={x[133], x[134], x[135], x[136]};
            vector <double> y_points={y[133], y[134], y[135], y[136]};
            // check to see if there are any gaps in this new vector
            for (int k=0; k<3; k++){
                if (abs(chosen_points[k]-chosen_points[k+1])>discontinuity_allowance){
                    cout<<"Error: Discontinuity in interval. Not enough points to interpolate interval." << endl;
                }
            }
            // call an interpolation function given the points
            interpolate(chosen_points, y_points);
        else{
            vector <double> chosen_points={x[i-1], x[i], x[i+1], x[x+2]};
            vector <double> y_points={y[i-1], y[i], y[i+1], y[x+2]};
            // check to see if there are any gaps in this new vector
            for (int k=0; k<3; k++){
                if (abs(chosen_points[k]-chosen_points[k+1])>discontinuity_allowance){
                    cout<<"Error: Discontinuity in interval. Not enough points to interpolate interval." << endl;
                }
            }
            // check to see if i is small enough to have two values after it
            if (i>=135) cout << "Error: Not enough points to interpolate interval." << endl;
            // call an interpolation function given the points
            interpolate(chosen_points, y_points);
        }
    }
}
```
This algorithm takes into account any discontinuities or endpoints that may arise in the given scenario. For the interval x_i to x_i+1, the function will take those two points and its two adjacent neighbors. If there is a discontinuity or endpoint then the function adjusts and takes values from a different direction. If four consecutive points without a discontinuity or endpoint cannot be found then an error message is printed to let the user know a degree 3 polynomial cannot be interpolated for that interval. Otherwise it creates two vectors, a subset of x and a subset of y with the chosen points for interpolating over the given interval and calls an interpolating function. 
