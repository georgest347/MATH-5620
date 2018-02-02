**Function Name:**          thomasMatrix()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves a tridiagonal symetric matrix of form Au=b. Where A is the tridiagonal symetric matrix. This function uses Jacobi Iteration to find the u values. At the heart of this function is the equation shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=u_{i&plus;1}=D^{-1}(b-(L&plus;U)u_{i})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u_{i&plus;1}=D^{-1}(b-(L&plus;U)u_{i})" title="u_{i+1}=D^{-1}(b-(L+U)u_{i})" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" title="\begin{bmatrix} ad &as &0 \\ al&ad &as \\ 0&al &ad \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} b\\ b\\ b \end{bmatrix}" /></a>

Considering the matrix system above, the components of the equation are defined as follows:

<a href="https://www.codecogs.com/eqnedit.php?latex=u_{i&plus;1}=\begin{bmatrix}&space;u_1\\&space;u_2\\&space;u_3&space;\end{bmatrix}_{i&plus;1}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u_{i&plus;1}=\begin{bmatrix}&space;u_1\\&space;u_2\\&space;u_3&space;\end{bmatrix}_{i&plus;1}" title="u_{i+1}=\begin{bmatrix} u_1\\ u_2\\ u_3 \end{bmatrix}_{i+1}" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=u_{i}=\begin{bmatrix}&space;u_1\\&space;u_2\\&space;u_3&space;\end{bmatrix}_{i}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u_{i}=\begin{bmatrix}&space;u_1\\&space;u_2\\&space;u_3&space;\end{bmatrix}_{i}" title="u_{i}=\begin{bmatrix} u_1\\ u_2\\ u_3 \end{bmatrix}_{i}" /></a>



**Input:** This function takes one vector as defined below. 

vector IV = [as,as,as,ad,ad,ad,al,al,al,b,b,b]
	
The above vector is defined from the below matrix system. These values can be assigned by using the [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital) function.
	
<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" title="\begin{bmatrix} ad &as &0 \\ al&ad &as \\ 0&al &ad \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} b\\ b\\ b \end{bmatrix}" /></a>
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors
  ```
 The following functions must be included:

[multiplyMV()](https://georgest347.github.io/MATH-5620/softwareManual/HW2/multiplyMV) //Used to multiply (L+U)x
[absoluteErrorNormal()](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal) //Used to find the absolute normalized error between xnew and xold
[maxVectElem()](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem) //Used to find the max normalized error value.
	

 

**Output:** This function returns the values of u vector where u is defined as the unknowns in a system of equations of form Au=b. These values can then be used later, or printed to the screen.

**Usage/Example:**

This function is used to solve the problem given below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;-2&space;&1&space;&0&space;\\&space;1&-2&space;&1&space;\\&space;0&space;&1&space;&-2&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;0.00390625\\&space;0.015625\\&space;-0.94844&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;-2&space;&1&space;&0&space;\\&space;1&-2&space;&1&space;\\&space;0&space;&1&space;&-2&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;0.00390625\\&space;0.015625\\&space;-0.94844&space;\end{bmatrix}" title="\begin{bmatrix} -2 &1 &0 \\ 1&-2 &1 \\ 0 &1 &-2 \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} 0.00390625\\ 0.015625\\ -0.94844 \end{bmatrix}" /></a>

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
		
	vector<double> u3(m);
	vector<double>IV(4*m);
		
	IV=ellipticODEInital(a,b,ua,ub,n);
	
	u3=jacobiTri(IV);
	
	//for printing the u3 vector
	for (int i = 0; i < m; i++) {
		cout << u3[i] << endl;
	}
	
```

The results on the screen were as follows:

```c++
	2.93844
	3.40039
	3.90039
	4.43844

```
This result was verified with the following matlab code:
```matlab
%Jacobi Algorithm verification

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


**Implementation/Code:** The following is the code for jacobiTri()
```c++
vector<double> jacobiTri(vector<double> IV) {
	/*----------------------------------------------
	This function solves a system of equations using
	jacobi iteration.
	Au=b
	(L+D+U)u=b <-- Seperate the matrix into the addition
				of three matrices.
	L= lower triangle matrix
	D=Diagonal matrix
	U= uppertriangle matrix

	solve x at k+1 using a guess of x_0 =0

	x_k+1=D^-1*(b-(L+U)x_k)

	*/

	int m = sizeof(IV) / 4;
	vector<double> u(m);
	vector<double> xnew(m);
	vector<double> xold(m);
	vector<double> error(m);
	double maxerror=10000000000;


	//Matrix to hold the LU values
	vector<vector<double> > LU(m, u);
	
	// Initalize the LU Matrix
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			//al
			if (i == j + 1) {
				LU[i][j] = IV[j + 2 * m];
			}
			//as
			if (i == j - 1) {
				LU[i][j] = IV[i];
			}

		}
	}
	
	/*
	//See the LU Matrix
	cout << "LU Jacobi" << endl;
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			cout <<setw(6)<< LU[i][j];
		}
		cout << endl;
	}
	cout << endl;
	*/
	
	// Iterates through finding the x values
	int count = 0;
	//Change the error value to be smaller for better convergance
	while (maxerror > 0.000001) {

		//multiplys (L+U)*x.i-1
		u = multiplyMV(LU, xold);


		//Solves new x values
		for (int i = 0; i < m; i++) {
			xnew[i] = (1/IV[m + i]) * (IV[3 * m + i] - u[i]); // equation used x.i=D^-1*(b-(L+U)x.i-1)
		}

		//cout << "error" << endl;
		//Finds the error
		for (int i = 0; i < m; i++) {
			error[i] = absoluteErrorNormal(xnew[i], xold[i]);
			//cout << error[i] << endl;
		}
		maxerror = maxVectElem(error);
		//Store newx in oldx
		for (int i = 0; i < m; i++) {
			xold[i] = xnew[i];
		}

	}

	u = xnew;
	return u;
}
```
