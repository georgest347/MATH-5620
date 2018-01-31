**Function Name:**          thomasMatrix()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves a tridiagonal symetric matrix of form Au=b. Where A is the tridiagonal symetric matrix.

**Input:** This function takes four vectors and an integer in the following order:
  ad: The diagonal vector values of the matrix A
  as: The upper or super diagonal of the matrix A
  al: The lower diagonal of the matrix A
  n: An integer value describing the size of A as in A is a nxn matrix.  
  
The following headers must also be included:
  ```
      #include <iostream> <-- to show the number on scree
      #include <vector>  <-- to define the aformentioned vectors
  ```

**Output:** This function returns the values of u vector where u is defined as the unknowns in a system of equations of form Au=b. These values can then be used later, or printed to the screen.

**Usage/Example:**

This function is used to solve the problem given below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;-2&space;&1&space;&0&space;\\&space;1&-2&space;&1&space;\\&space;0&space;&1&space;&-2&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;0.00390625\\&space;0.015625\\&space;-0.94844&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;-2&space;&1&space;&0&space;\\&space;1&-2&space;&1&space;\\&space;0&space;&1&space;&-2&space;\end{bmatrix}\begin{bmatrix}&space;u_{1}\\&space;u_{2}\\&space;u_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;0.00390625\\&space;0.015625\\&space;-0.94844&space;\end{bmatrix}" title="\begin{bmatrix} -2 &1 &0 \\ 1&-2 &1 \\ 0 &1 &-2 \end{bmatrix}\begin{bmatrix} u_{1}\\ u_{2}\\ u_{3} \end{bmatrix}=\begin{bmatrix} 0.00390625\\ 0.015625\\ -0.94844 \end{bmatrix}" /></a>

All vectors were initalized with thomasInital 
```
		double n = 5;
	double x;
	x=factorial(n);

	cout << x << endl;
```

The results on the screen were as follows:

```
	120

```

**Implementation/Code:** The following is the code for factorial()
```
double factorial(double n)
{
	if (n > 1)
		return n * factorial(n - 1);
	else
		return 1;
}
```

