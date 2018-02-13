**Function Name:**          dotProd()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function computes the dot product of two vectors

**Input:** This function takes two vectors of the same size.
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <cmath> //<-- for the abs value function
  ```

**Output:** This function outputs a double that is the dot product of two vectors.
	
**Usage/Example:**

This function was passed the following vectors:
```c++
  x={1,2,3,4};
  y={7,4,6,3};
```

The results on the screen were as follows:

```c++
 45
```
**Implementation/Code:** The following is the code for dotProd()
```c++
double dotProd(vector<double> x,vector<double> y){
    //Finds the dot product of two vectors
    int m=x.size();
    int n=y.size();
    double sum=0;

    //Check to make sure dot product is valid
    if (m!=n){
        cout<<"NOT A VALID DOT PRODUCT"<<endl;
        return -1;
    }

    for (int i=0;i<m;i++){
        sum=sum+x[i]*y[i];
    }
    return sum;

}
```
