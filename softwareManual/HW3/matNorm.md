**Function Name:**          matNorm()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function finds the 1 norm and the infinity norm of a matrix.

The 1 norm of a matrix is the max absolute column sum given by equations 1 and 2.[1]

<a href="https://www.codecogs.com/eqnedit.php?latex=A=\begin{bmatrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&&space;a_{23}\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A=\begin{bmatrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&&space;a_{23}\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{bmatrix}" title="A=\begin{bmatrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} & a_{23}\\ a_{31} &a_{32} &a_{33} \end{bmatrix}" /></a> **eq 1**

<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;\|&space;A&space;\right&space;\|_{1}=\max_{1\leq&space;j\leq&space;n}(\sum_{i=1}^{n}\left&space;|&space;a_{ij}&space;\right&space;|&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;\|&space;A&space;\right&space;\|_{1}=\max_{1\leq&space;j\leq&space;n}(\sum_{i=1}^{n}\left&space;|&space;a_{ij}&space;\right&space;|&space;)" title="\left \| A \right \|_{1}=\max_{1\leq j\leq n}(\sum_{i=1}^{n}\left | a_{ij} \right | )" /></a> **eq 2**

The infinity norm of a matrix is the max absolute row sum given by equations 1 and 3.[1]

<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;\|&space;A&space;\right&space;\|_{\infty&space;}=\max_{1\leq&space;i\leq&space;n}(\sum_{j=1}^{n}\left&space;|&space;a_{ij}&space;\right&space;|&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;\|&space;A&space;\right&space;\|_{\infty&space;}=\max_{1\leq&space;i\leq&space;n}(\sum_{j=1}^{n}\left&space;|&space;a_{ij}&space;\right&space;|&space;)" title="\left \| A \right \|_{\infty }=\max_{1\leq i\leq n}(\sum_{j=1}^{n}\left | a_{ij} \right | )" /></a> **eq 3**

This function calls the [maxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem) function to find the max sum of the matrix for each norm.

**Input:** This function takes a mxn matrix A
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
  ```

**Output:** This function outputs a 1x2 vector that contains the 1 norm in the i=0 index and the infinity norm in the i=1 index
	
**Usage/Example:**

This function was initalized with the following driving code:
```c++
a=0;
b=1;
ua=2.5;
ub=5.0;
n=5;
```
The driving code is shown below:
```c++
	int m = 3;
	vector<double> a(m);
	vector<vector<double> > A(m, a);
	double count = 1;

	srand(time(NULL));

	for (int i = 0; i < m; i++) {
		for (int j = 0; j < m; j++) {
			A[i][j] = rand() % 10+1;
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

	//Returns the 1 norm and Infinity norm respectivly
	for (int i = 0; i < 2; i++) {
		cout << matNorm(A)[i] << endl;
	}
  
  return 0;
```
The matrix values were generated with a random number generator. Numbers range from 1 to 10.

The results on the screen were as follows:

```c++
 2     10     2
10     5     2
10     4     8

22
22
```

**Implementation/Code:** The following is the code for matNorm()
```c++
vector<double> matNorm(vector<vector<double> > A) {
	/*--------------------------------------
	This function finds the max abs column sum.
	Which corresponds to the 1 Norm of a matrix
	*/

	int m = A.size(); /* number of rows*/
	int n = A.size(); /* number of columns*/
	
	vector<double> norm(2);
	vector<double> colsum(n);
	vector<double> rowsum(m);

	// Sum cols take abs value of each element for sum
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < n; j++) {
			colsum[j] = colsum[j] + abs(A[i][j]);
		}
	}

	// Places the 1 Norm in the first index value of norm
	norm[0] = maxVectElem(colsum);

	// Sum rows take abs value of each element for sum
	for (int i = 0; i < m; i++) {
		for (int j = 0; j < n; j++) {
			rowsum[i] = rowsum[i] + abs(A[i][j]);
		}
	}

	// Places the 1 Norm in the first index value of norm
	norm[1] = maxVectElem(rowsum);

	return norm;
}
```
**References**
[1]http://www.personal.soton.ac.uk/jav/soton/HELM/workbooks/workbook_30/30_4_matrx_norms.pdf
