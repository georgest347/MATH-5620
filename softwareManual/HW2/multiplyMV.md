**Function Name:**          multiplyMV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes a matrix mxm and multiplies it by a vector mx1. It preforms the equivalent operation as shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{bmatrix}\begin{bmatrix}&space;x_{1}\\&space;x_{2}\\&space;x_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;a_{11}*x_{1}&plus;a_{12}*x_{2}&plus;a_{13}*x_{3}\\&space;a_{21}*x_{1}&plus;a_{22}*x_{2}&plus;a_{23}*x_{3}\\&space;a_{31}*x_{1}&plus;a_{32}*x_{2}&plus;a_{33}*x_{3}&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{bmatrix}\begin{bmatrix}&space;x_{1}\\&space;x_{2}\\&space;x_{3}&space;\end{bmatrix}=\begin{bmatrix}&space;a_{11}*x_{1}&plus;a_{12}*x_{2}&plus;a_{13}*x_{3}\\&space;a_{21}*x_{1}&plus;a_{22}*x_{2}&plus;a_{23}*x_{3}\\&space;a_{31}*x_{1}&plus;a_{32}*x_{2}&plus;a_{33}*x_{3}&space;\end{bmatrix}" title="\begin{bmatrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} &a_{23} \\ a_{31} &a_{32} &a_{33} \end{bmatrix}\begin{bmatrix} x_{1}\\ x_{2}\\ x_{3} \end{bmatrix}=\begin{bmatrix} a_{11}*x_{1}+a_{12}*x_{2}+a_{13}*x_{3}\\ a_{21}*x_{1}+a_{22}*x_{2}+a_{23}*x_{3}\\ a_{31}*x_{1}+a_{32}*x_{2}+a_{33}*x_{3} \end{bmatrix}" /></a>

*Input:** This function accepts a mxm matrix, and a mx1 vector.
  
**Output:** This function outputs a vector that is mx1

**Usage/Example:** The following is the code for multiplyMV():

The following matrix was inputed:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;0&space;&1&space;&0&space;\\&space;1&space;&&space;0&space;&&space;1\\&space;0&&space;1&space;&0&space;\end{bmatrix}\begin{bmatrix}&space;1\\&space;1\\&space;1&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;0&space;&1&space;&0&space;\\&space;1&space;&&space;0&space;&&space;1\\&space;0&&space;1&space;&0&space;\end{bmatrix}\begin{bmatrix}&space;1\\&space;1\\&space;1&space;\end{bmatrix}" title="\begin{bmatrix} 0 &1 &0 \\ 1 & 0 & 1\\ 0& 1 &0 \end{bmatrix}\begin{bmatrix} 1\\ 1\\ 1 \end{bmatrix}" /></a>

The result printed on the screen was:
```c++
1
2
1
```

**Implementation/Code:** The following is the code for multiplyMV():

```c++
vector<double> multiplyMV(vector<vector<double > > A, vector<double> x) {
	/*-------------------------------------------------------------------
	This function takes a matrix A and multipllies it by a vector x.
	If A is mxm and x is mx1 the resultat vector b is a mx1 vector.
	*/
	int m = x.size();
	vector<double> b(m);
	
	//Times the rows and columns
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			b[i] = A[i][j] * x[j] + b[i];
		}
	}

	return b;
}
```


