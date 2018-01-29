**Function Name:**          luDecomposition()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will take a linear system of equations Ax=b and solve for the vector x. The matrix A is a nxn matrix. The b vector is a nx1 vector and the returned x vector is a nx1 vector.  

**Input:** The function takes the following inputs (A,n,b)
  A is a matrix of type vector<vector<double> > nxn matrix
  n is an integer value for the number of rows and colums in A
  b is a vector of type vector<double>
  
The following headers must also be included:
  ```
      #include <iostream> <-- used if displaying the L and U matrix
      #include <iomanip>  <-- used if displaying the L and U matrix
      #include <vector>
  ```

**Output:** This function can print the L, and U matrix to the screen, it can also print the x vector. The function returns the x vector.
  x is a vector of type vector<double>

**Usage/Example:**

This function is used to solve the problem given below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;3&space;&&space;1\\&space;-6&space;&-4&space;\end{bmatrix}*\begin{bmatrix}&space;x_{1}\\x_{2}&space;\end{bmatrix}=\begin{bmatrix}&space;1\\2&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;3&space;&&space;1\\&space;-6&space;&-4&space;\end{bmatrix}*\begin{bmatrix}&space;x_{1}\\x_{2}&space;\end{bmatrix}=\begin{bmatrix}&space;1\\2&space;\end{bmatrix}" title="\begin{bmatrix} 3 & 1\\ -6 &-4 \end{bmatrix}*\begin{bmatrix} x_{1}\\x_{2} \end{bmatrix}=\begin{bmatrix} 1\\2 \end{bmatrix}" /></a>

The driving code is defined below:
```
	int n = 2;
	vector<double> a(n);
	vector<vector<double> > A(n,a);
	vector<double> b(n);

	A[0][0] = 3;
	A[0][1] = 1;
	A[1][0] = -6;
	A[1][1] = -4;

	b[0] = 1;
	b[1] = 2;

	luDecomposition( A, n, b);
```

The results on the screen were as follows:

```
	Lower Triangular          Upper Triangular
   1      0                  3      1
  -2      1                  0     -2
  These are the x values
  1
  -2

```

**Implementation/Code:** The following is the code for luDecomposition()
```
vector<double> luDecomposition(vector<vector<double> > A, int n,vector<double> b)
{
	/*---------------------------------------------------------
	The value n is the nxn value of the matrix A.

	----------------------------------------------------------*/
	vector<double> a(n);
	vector<vector<double> > U(n, a);
	vector<vector<double> > L(n, a);
	vector<double> y(n);

	// Decomposing matrix into Upper and Lower
	// triangular matrix
	for (int i = 0; i < n; i++) {

		// Upper Triangular
		for (int k = i; k < n; k++) {

			// Summation of L(i, j) * U(j, k)
			double sum = 0;
			for (int j = 0; j < i; j++)
				sum += (L[i][j] * U[j][k]);

			// Evaluating U(i, k)
			U[i][k] = A[i][k] - sum;
		}

		// Lower Triangular
		for (int k = i; k < n; k++) {
			if (i == k)
				L[i][i] = 1; // Diagonal as 1
			else {

				// Summation of L(k, j) * U(j, i)
				double sum = 0;
				for (int j = 0; j < i; j++)
					sum += (L[k][j] * U[j][i]);

				// Evaluating L(k, i)
				L[k][i] = (A[k][i] - sum) / U[i][i];
			}
		}
	}

	/*
	// setw is for displaying nicely
	cout << setw(6) << "      Lower Triangular" 
		 << setw(32) << "Upper Triangular" << endl;

	// Displaying the result :
	for (int i = 0; i < n; i++) {
		// Lower
		for (int j = 0; j < n; j++)
			cout << setw(6) << L[i][j] << "\t";
		cout << "\t";

		// Upper
		for (int j = 0; j < n; j++)
			cout << setw(6) << U[i][j] << "\t";
		cout << endl;
	}
	*/
	

	// Lower back substitution
	for (int i = 0; i < n; i++) {
		double s = 0;
		for (int j = 0; j < i; j++) {
			s = s + L[i][j] * y[j];
		}
		y[i] = (b[i] - s) / L[i][i];
	}

	/*
	//Print out y vector
	for (int i = 0; i < n; i++) {
		cout << y[i] << endl;
	}
	*/

	//Upper back substition
	for (int i = n-1; i >= 0; i--) {
		double s = 0;
		for (int j = n-1; j > i; j--) {
			s = s + U[i][j] * y[j];
		}
		y[i] = (y[i] - s) / U[i][i];
	}

	/*
	//Print out y vector
	cout << "These are the x values " << endl;
	for (int i = 0; i < n; i++) {
		cout << y[i] << endl;
	}
	*/
	
	return y;
}
```
