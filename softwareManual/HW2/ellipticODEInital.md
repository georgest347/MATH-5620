**Function Name:**          ellipticODEInital()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function initalizes the values needed to solve the following equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\partial^2&space;u}{\partial&space;x^2}=f(x)&space;,&space;x\in&space;(a,b)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\partial^2&space;u}{\partial&space;x^2}=f(x)&space;,&space;x\in&space;(a,b)" title="\frac{\partial^2 u}{\partial x^2}=f(x) , x\in (a,b)" /></a>

With boundary values defined by:

<a href="https://www.codecogs.com/eqnedit.php?latex=u(a)=u_{a},u(b)=u_{b}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(a)=u_{a},u(b)=u_{b}" title="u(a)=u_{a},u(b)=u_{b}" /></a>

This function calls the [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/functInital) function to solve the f(x) values for each x defined on the interval from a to b. The user must include this function, and include the function f(x) from there problem here. 

**Input:** This function takes the values a,b,ua,ub, and n:
a= the lower bound of the interval in intrest
b= the upper bound of the interval in intrest
ua= the boundray value of the function at a
ub= the boundary value of the function at b
n= the number of intervals to break the a-b interval into
  
The following headers must also be included:
  ```c++
      #include <iostream> <-- to show the number on screen
      #include <vector>  <-- to define the aformentioned vectors
  ```

**Output:** This function returns the vector IV. This vector is defined below and is the combination of terms from the A matrix and b vector.

vector IV = [as,as,as,ad,ad,ad,al,al,al,b,b,b]
	
The above vector is defined from the below matrix system.
	
<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;ad&space;&as&space;&0&space;\\&space;al&ad&space;&as&space;\\&space;0&al&space;&ad&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;b\\&space;b\\&space;b&space;\end{bmatrix}" title="\begin{bmatrix} ad &as &0 \\ al&ad &as \\ 0&al &ad \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} b\\ b\\ b \end{bmatrix}" /></a>

**Usage/Example:**

This function was used to initalize a problem with the following values:
```c++
a=0;
b=1;
ua=0;
ub=1;
n=4;
```
The driving code is shown below:
```c++
	int n = 4;
  int m=n-1;
	double b,a;
	double ua, ub;
	// Values of a to b or range of x values to do finite difference over
	b = 1;
	a = 0;
	//ua and ub are boundary values of the function
	ua = 0;
	ub = 1;
		
	vector<double> u1(m);
	vector<double>IV(4*m);
		
	IV=ellipticODEInital(a,b,ua,ub,n);
  for (int i=0;i<4*m;i++){
    cout<<IV[i]<<endl;
   }
```

The results on the screen were as follows:

```c++
  1
  1
  1
  -2
  -2
  -2
  1
  1
  1
  0.00390625
  0.015625
  -0.964844
```

**Implementation/Code:** The following is the code for ellipticODEInital()
```c++
vector<double> ellipticODEInital(double a, double b, double ua, double ub,int n){
	/*-----------------------------------------------------------
	This function needs the functInital() function with the user
	defined f(x) for the problem u"=f(x)
	*/
	double h;
	vector<double> x(n + 1);
	vector<double> f(n + 1);
	int m = n - 1;
	vector<double> ad(m);
	vector<double> as(m);
	vector<double> al(m);
	vector<double> B(m);
	//All the vectors lined up in one vector
	int k = 4 * m;
	vector<double> IV(k);

	// h is the step size of the function broken into n intervals	
	h = (b - a) / n;

	//Finds the values of the x vector
	x[0] = a;
	for (int i = 1; i <= n; i++) {
		x[i] = x[i - 1] + h;
	}

	/* See the x vector
	for (int i = 0; i <= n; i++) {
	cout << x[i] << endl;
	}
	*/

	//Calculates the value of the function f at the x points
	f = functInital(x, n);

	/*
	//See the f vector
	cout << "f" << endl;
	for (int i = 0; i <= n; i++) {
		cout << f[i] << endl;
	}
	cout << endl;
	*/

	// Initialize vectors
	for (int i = 0; i < m; i++) {
		ad[i] = -2;
	}
	for (int i = 0; i < m; i++) {
		as[i] = 1;
		al[i] = 1;
	}
	for (int i = 1; i < n - 2; i++) {
		B[i] = h * h*f[i + 1];
	}

	B[0] = h * h*f[1] - ua;
	B[n - 2] = h * h*f[m] - ub;

	/*
	//See the B vector
	cout << "B" << endl;
	for (int i = 0; i < m; i++) {
		cout << B[i] << endl;
	}
	cout << endl;
	*/

	//Stores the as vector to pass to main
	for (int i = 0; i < m; i++) {
		IV[i] = as[i];
	}

	//Stores the ad vector to pass to main
	for (int i = m; i < 2*m; i++) {
		IV[i]= ad[i-m];
	}

	//Stores the al vector to pass to main
	for (int i = 2*m; i < 3*m; i++) {
		IV[i] = al[i - 2*m];
	}

	//Stores the b vector to pass to main
	for (int i = 3*m; i < 4*m; i++) {
		IV[i] = B[i - 3 * m];
	}
		
	return IV;
}
```
