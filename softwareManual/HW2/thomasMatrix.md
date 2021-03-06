**Function Name:**          thomasMatrix()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves a tridiagonal symetric matrix of form Au=b. Where A is the tridiagonal symetric matrix.

**Input:** This function takes a vector as defined below.

vector IV = [as,as,as,ad,ad,ad,al,al,al,b,b,b]
	
The above vector is defined from the below matrix system. These values can be assigned by using the [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital) function.
	
<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" title="\begin{bmatrix} ad &as &0 \\ al&ad &as \\ 0&al &ad \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} b\\ b\\ b \end{bmatrix}" /></a>
  
The following headers must also be included:
  ```c++
      #include <iostream> <-- to show the number on screen
      #include <vector>  <-- to define the aformentioned vectors
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
		
	vector<double> u1(m);
	vector<double>IV(4*m);
		
	IV=ellipticODEInital(a,b,ua,ub,n);
	
	u1=thomasMatrix(IV);
	
	//for printing the u1 vector
	for (int i = 0; i < m; i++) {
		cout << u1[i] << endl;
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
```matlab
%Thomas Algorithm verification

A=[-2,1,0,0;1,-2,1,0;0,1,-2,1;0,0,1,-2]
b=[-2.47649;0.0380423;0.0380423;-4.97649]

x=A\b
```
results:
```matlab
x =

    2.93845
    3.4004
    3.9004
    4.43845
```


**Implementation/Code:** The following is the code for thomasMatrix()
```c++
vector<double> thomasMatrix(vector<double> IV) {
	int m = sizeof(IV)/4;
	vector<double> u(m);
	vector<double> as(m);
	vector<double> ad(m);
	vector<double> al(m);
	vector<double> b(m);

	//Expand the IV vector to components
	for (int i = 0; i < m; i++) {
		as[i]=IV[i];
	}
	for (int i = m; i < 2 * m; i++) {
		ad[i - m]=IV[i];
	}
	for (int i = 2 * m; i < 3 * m; i++) {
		al[i - 2 * m]=IV[i];
	}
	for (int i = 3 * m; i < 4 * m; i++) {
		b[i - 3 * m]=IV[i];
	}
	
	for (int i = 1; i<m; i++) {

		double ratio = al[i - 1] / ad[i - 1];
		ad[i] -= ratio * as[i - 1];
		b[i] -= ratio * b[i - 1];
	}

	/*
	//See the vectors ad al as
	cout << "ad " << endl;
	for (int i = 0; i < m; i++) {
		cout << ad[i] << endl;
	}
	cout << endl;

	cout << "al " << endl;
	for (int i = 0; i < m; i++) {
		cout << ad[i] << endl;
	}
	cout << endl;

	cout << "as " << endl;
	for (int i = 0; i < m; i++) {
		cout << ad[i] << endl;
	}
	cout << endl;
	*/

	// solve for last x value
	u[m - 1] = b[m - 1] / ad[m - 1];

	// solve for remaining x values by back substitution
	for (int i = m - 2; i >= 0; i--) {
		u[i] = (b[i] - as[i] * u[i + 1]) / ad[i];
	}

	return u;
}
```
