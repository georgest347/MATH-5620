**Function Name:**           fdCoeffV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will find the coefficients for a finite difference approximation of arbitrary order of accuracy for a give derivative. The general equation used (eq 1) shows the coefficients c_j, the value the function is appoximated at xbar, and the x_j points. The term on the left side is set to 1 for the k'th derivative. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{1}{(i-1)!}\sum_{j=1}^{n}c_{j}(x_{j}-\bar{x})^{(i-1)}=\left&space;\{&space;\overset{1&space;;&space;(i-1)=k}{0}\right&space;\}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{1}{(i-1)!}\sum_{j=1}^{n}c_{j}(x_{j}-\bar{x})^{(i-1)}=\left&space;\{&space;\overset{1&space;;&space;(i-1)=k}{0}\right&space;\}" title="\frac{1}{(i-1)!}\sum_{j=1}^{n}c_{j}(x_{j}-\bar{x})^{(i-1)}=\left \{ \overset{1 ; (i-1)=k}{0}\right \}" /></a>

**Input:** The function takes four inputs (k,xbar,x[],n)
  k is the k'th derivative to be approximated
  xbar is the point at which the k'th derivative is evaluated
  x[] is a vector of values around xbar 
  n is the number of numbers in x[] or length(x)
  
  This function uses luDecomposition() function to solve the matrix Ax=b. This function must be included for the program to work properly. The following headers must also be included:
  ```
      #include <iostream>
      #include <iomanip>
      #include <vector>
      #include <cmath>
  ```

**Output:** This function returns the c_j coefficients to the function that called it. The coefficients can then be used later, or printed to the screen.

**Usage/Example:**

This function was called using the following code:
```
	double x[5] = { 1,2,3,4,5 }; 	//Define the x vector
	int n = 5;			//number of terms in the x vector
	vector<double> coeff;		// Vector to hold the coeff returned

	coeff=fdCoeffV(2, 5, x, n);	//call the function

	//Prints the coefficients to the screen
	for (int i = 0; i < n; i++) {
		cout << coeff[i] << endl;
	}
```
The results on the screen were as follows:

```
	0.916667
	-4.66667
	9.5
	-8.66667
	2.91667

```
Results have been validated with matlab code from [[1]](http://www.siam.org/books/OT98/) pp 11

**Implementation/Code:** The following is the code for fdCoeffV()

      vector<double> fdCoeffV(int k, double xbar, double x[],int n) {
	//Builds a matrix A, U, L
	vector<double> a(n);
	vector<vector<double> > A(n, a);
	vector<vector<double> > U(n, a);
	vector<vector<double> > L(n, a);
	vector<double> y(n);

	// Builds the b vector and c vector
	vector<double> b(n);
	vector<double> c(n);

	// Varibles
	double fact = 0;
	double g = 0;

	// Initializes the matrix with 0's
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			A[i][j] = 1;
			//cout << A[i][j]; //Unmute to visualize the matrix
		}
		//cout << " " << endl; //Unmute to visualize the matrix	
		b[i] = 0;
		//cout << b[i] << endl; //Unmute to visualize the 'b' vector
	}	

	// Checks to make sure the length of the vector x is greater than k
	if (k >= n) {
		cout << "ERROR, length of x must be greater than k" << endl;
		return b;
	}
	
	// Set the k'th derivative term to 1
	b[k] = 1;
	
	// Enumerates the A matrix
	for (int i = 1; i <= n; i++) {
		g = i - 1;
		fact = factorial(g);
		for (int j = 0; j < n; j++) {
			A[i-1][j] = (A[i-1][j]) * (1 / fact)*pow((x[j] - xbar), g);
		}
	}
	/*
	// To see the A matrix for debugging
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			cout << A[i][j]<<"    "; //Unmute to visualize the matrix
		}
		cout << " " << endl; //Unmute to visualize the matrix		
	}
	*/
	
	y = luDecomposition(A, n, b);
	
		return y;
    }
       
   **References** 
       
	[1] "Finite Difference Methods for Ordinary and Partial Differential Equations", Randall J. LeVeque, 2007
		[www.siam.org/books/OT98](http://www.siam.org/books/OT98/)
