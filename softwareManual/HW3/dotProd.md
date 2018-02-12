**Function Name:**          dotProd()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function finds the 2 norm of a matrix, or the Max eigen value.

The 2 norm of a matrix is the max eigen value. Using the power iteration method, this function finds the 2 norm of the matrix. Equation 1 shows the iterative power method. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\lambda_{i&plus;1}&space;\begin{bmatrix}&space;v_{1}\\&space;v_{2}\\&space;v_{3}&space;\end{bmatrix}_{i&plus;1}=A*\lambda_{i}&space;\begin{bmatrix}&space;v_{1}\\&space;v_{2}\\&space;v_{3}&space;\end{bmatrix}_{i}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\lambda_{i&plus;1}&space;\begin{bmatrix}&space;v_{1}\\&space;v_{2}\\&space;v_{3}&space;\end{bmatrix}_{i&plus;1}=A*\lambda_{i}&space;\begin{bmatrix}&space;v_{1}\\&space;v_{2}\\&space;v_{3}&space;\end{bmatrix}_{i}" title="\lambda_{i+1} \begin{bmatrix} v_{1}\\ v_{2}\\ v_{3} \end{bmatrix}_{i+1}=A*\lambda_{i} \begin{bmatrix} v_{1}\\ v_{2}\\ v_{3} \end{bmatrix}_{i}" /></a> **eq 1**[1]

This function calls the following functions:

[maxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem) 
[multiplyMV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/multiplyMV) 
[absoluteErrorNormal](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal) 
[dotProd](https://georgest347.github.io/MATH-5620/softwareManual/HW3/dotProd) 

**Input:** This function takes a nxn matrix A
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <cmath> //<-- for the abs value function
  ```

**Output:** This function outputs a double that is the dominant eigen value.
	
**Usage/Example:**

This function was initalized with the following driving code and created a 3x3 Hilbert Matrix:
```c++
  int m = 3;
	vector<double> a(m);
	vector<vector<double> > A(m, a);
  
    //Initalize a Hilbert matrix of size m
    for (int i=1;i<=m;i++){
        for (int j=1;j<=m;j++){
            A[i-1][j-1]=1.0/(i+j-1);
        }
    }

	//SEE A
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			cout << A[i][j]<<"     ";
		}
		cout << endl;
	}
	cout << endl;
   
  cout<<powerEig(A)<<endl;
    return 0;
```

The results on the screen were as follows:

```c++
 1     0.5     0.333
0.5    0.333   0.25
0.333  0.25    0.2

1.40832
```
This result was verified with [symbolab](https://www.symbolab.com/solver/matrix-eigenvalues-calculator/eigenvalues%20%5Cbegin%7Bpmatrix%7D1%260.5%26%5Cfrac%7B1%7D%7B3%7D%5C%5C%200.5%26%5Cfrac%7B1%7D%7B3%7D%260.25%5C%5C%20%5Cfrac%7B1%7D%7B3%7D%260.25%260.2%5Cend%7Bpmatrix%7D)[2] and produced the following eigen values:

```c++
  0.00269
  0.12233
  1.40832
```

**Implementation/Code:** The following is the code for powerEig()
```c++
double powerEig(vector<vector<double> > A){
    //This function takes the matrix A and finds
    // the max eigen value using the power method
    // the function returns the max eigen value.

    int m = A.size();
    vector<double> lamda(m);
    vector<double> x(m);
    double maxEig;
    double maxEigOld;
    double error=1000000000000;
    double domEig;
    int iter=1;

    //Initalize the eigenvector to be non zero
    for(int i=0;i<m;i++){
        lamda[i]=1;
    }

    // Loops through to find the eigen value
    while (error>0.1||iter<=100){
        lamda=multiplyMV(A,lamda);
        maxEig=maxVectElem(lamda);
        /*cout<<"lamda times"<<endl;
        for(int i=0;i<m;i++){
            cout<<lamda[i]<<endl;
        }
        cout<<"lamda"<<endl;*/
        for(int i=0;i<m;i++){
            lamda[i]=lamda[i]/maxEig;
            //cout<<lamda[i]<<endl;
        }
        //cout<<"MAX"<<endl;

        //cout<<maxEig<<endl;
        error=absoluteErrorNormal(maxEig,maxEigOld);
        //cout<<error<<endl;
        maxEigOld=maxEig;
        iter++;
    }
    if (iter==100){
        cout<<"MAX iterations"<<endl;
    }

    //Find the Rayleigh quotient.
    x=multiplyMV(A,lamda);
    domEig=(dotProd(x,lamda))/(dotProd(lamda,lamda));

    return domEig;

}
```
**References**
[1]http://college.cengage.com/mathematics/larson/elementary_linear/5e/students/ch08-10/chap_10_3.pdf
[2]https://www.symbolab.com/solver/matrix-eigenvalues-calculator
