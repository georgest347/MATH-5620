**Function Name:**          triLUDecomp()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves a tridiagonal symetric matrix of form Au=b. Where A is the tridiagonal symetric matrix. This function uses LU decomposition, where A=LU. This turns the Au=b equation into LUu=b. This can be broken into Ly=b and Uu=y.

**Input:** This function takes a vector as defined below. 

vector IV = [as,as,as,ad,ad,ad,al,al,al,b,b,b]
	
The above vector is defined from the below matrix system. These values can be assigned by using the [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital) function.
	
<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" title="\begin{bmatrix} ad &as &0 \\ al&ad &as \\ 0&al &ad \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} b\\ b\\ b \end{bmatrix}" /></a>
  
The following headers must also be included:
  ```c++
      #include <iostream> <-- to show the number on screen
      #include <vector>  <-- to define the aformentioned vectors
      #include <iomanip> <-- to view tri matrix
  ```

**Output:** This function returns the values of u vector where u is defined as the unknowns in a system of equations of form Au=b. These values can then be used later, or printed to the screen.

**Usage/Example:**

This function is used to solve the problem given below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;-2&space;&1&space;&0&space;&0&space;\\&space;1&space;&-2&space;&1&space;&0&space;\\&space;0&space;&1&space;&-2&space;&1&space;\\&space;0&&space;0&space;&1&space;&-2&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}\\&space;u_{4}&space;\end{bmatrix}=\begin{bmatrix}&space;-2.47649\\&space;0.0380423\\&space;0.0380423\\&space;-4.97649&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;-2&space;&1&space;&0&space;&0&space;\\&space;1&space;&-2&space;&1&space;&0&space;\\&space;0&space;&1&space;&-2&space;&1&space;\\&space;0&&space;0&space;&1&space;&-2&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}\\&space;u_{4}&space;\end{bmatrix}=\begin{bmatrix}&space;-2.47649\\&space;0.0380423\\&space;0.0380423\\&space;-4.97649&space;\end{bmatrix}" title="\begin{bmatrix} -2 &1 &0 &0 \\ 1 &-2 &1 &0 \\ 0 &1 &-2 &1 \\ 0& 0 &1 &-2 \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3}\\ u_{4} \end{bmatrix}=\begin{bmatrix} -2.47649\\ 0.0380423\\ 0.0380423\\ -4.97649 \end{bmatrix}" /></a>

The driving code is shown below:
```c++
	int n = 5;	
	int m = n - 1;
	double b,a;
	double ua, ub;
	// Values of a to b or range of x values to do finite difference over
	b = 1;
	a = 0;
	//ua and ub are boundary values of the function
	ua = 2.5;
	ub = 5.0;
		
	vector<double> u2(m);
	vector<double>IV(4*m);
		
	IV=ellipticODEInital(a,b,ua,ub,n);

	u2 = triLUDecomp(IV);
	
	//for printing the u2 vector
	for (int i = 0; i < m; i++) {
		cout << u2[i] << endl;
	}
	
```

The results on the screen were as follows:

```c++
	2.93845
	3.4004
	3.9004
	4.43845

```
This result was verified with the following matlab code:
```c++
%LU Algorithm verification

A=[-2,1,0,0;1,-2,1,0;0,1,-2,1;0,0,1,-2]
b=[-2.47649;0.0380423;0.0380423;-4.97649]

x=A\b
```
results:
```c++
x =

  	2.93845
	3.4004
	3.9004
	4.43845

```

**Implementation/Code:** The following is the code for triLUDecomp()
```c++
vector<double> triLUDecomp(vector<double> IV){
	/*----------------------------------------------
	This function takes a vector that has the tri
	diagonals of a matrix and the b vector and 
	solves using LU decomposition. It solves in the
	form of Au=b. Solving for the u vector.
	*/
	
	// Since the input is designed for elliptic ODE, 
	// m is used instead of n because the boundry
	// conditions have been applied and reduce the 
	// matrix.

	int m =IV.size()/4;
	//Set up A matrix
	vector<double> a(m);
	vector<vector<double> > A(m, a);

	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			//ad
			if (i == j){
				A[i][j] = IV[i+m];
			}
			//al
			if (i == j + 1) {
				A[i][j] = IV[j+2*m];
			}
			//as
			if (i == j - 1) {
				A[i][j] = IV[i];
			}
			
		}
	}

	/*
	//see A
	cout << "A triLU" << endl;
	for (int i = 0; i < m; i++) {
	for (int j = 0; j < m; j++) {
	cout << A[i][j] << " ";
	}
	cout << "        " << endl;
	}
	cout << endl;
	*/

	//Set up u vector and B vector
	vector<double> u(m);
	vector<double> b(m);

	for (int i = 0; i < m; i++) {
		b[i] = IV[i + 3*m];
	}

	/*
	cout << "b triLU" << endl;
	for (int i = 0; i < m; i++) {
		cout << b[i] << endl;
	}
	cout << endl;
	*/

	//Set up two matrix for LU decomp
	vector<vector<double> > U(m, a);
	vector<vector<double> > L(m, a);
	
	// Decomposing matrix into Upper and Lower
	// triangular matrix
	for (int i = 0; i < m; i++) {

		// Upper Triangular
		for (int k = i; k < m; k++) {

			// Summation of L(i, j) * U(j, k)
			double sum = 0;
			for (int j = 0; j < i; j++)
				sum += (L[i][j] * U[j][k]);

			// Evaluating U(i, k)
			U[i][k] = A[i][k] - sum;
		}

		// Lower Triangular
		for (int k = i; k < m; k++) {
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
	//Show Lower Tri Matrix
	cout << setw(6) << "      Lower Triangular" << endl;
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			cout << setw(6) << L[i][j];
		}
		cout << endl;
	}
	cout << endl;

	//Show Upper Tri Matrix
	cout<< setw(6) << "Upper Triangular" << endl;
	for (int i = 0; i<m; i++) {
		for (int j = 0; j < m; j++) {
			cout << setw(6) << U[i][j];
		}
		cout << endl;
	}
	cout << endl;
	*/

	// Lower back substitution
	for (int i = 0; i < m; i++) {
		double s = 0;
		for (int j = 0; j < i; j++) {
			s = s + L[i][j] * u[j];
		}
		u[i] = (b[i] - s) / L[i][i];
	}

	/*
	//Print out u vector
	for (int i = 0; i < m; i++) {
	cout << u[i] << endl;
	}
	*/

	//Upper back substition
	for (int i = m - 1; i >= 0; i--) {
		double s = 0;
		for (int j = m - 1; j > i; j--) {
			s = s + U[i][j] * u[j];
		}
		u[i] = (u[i] - s) / U[i][i];
	}

	/*
	//Print out u vector
	cout << "These are the x values " << endl;
	for (int i = 0; i < m; i++) {
	cout << u[i] << endl;
	}
	*/

	return u;

}
```
