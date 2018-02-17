**Function Name:**          aLUb()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function is a modified version of the [luDecomposition](https://georgest347.github.io/MATH-5620/softwareManual/HW2/luDecomposition) function. This function takes a matrix of form:

<a href="https://www.codecogs.com/eqnedit.php?latex=A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" title="A=\left [ \left.\begin{matrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} &a_{23} \\ a_{31} &a_{32} &a_{33} \end{matrix}\right| \begin{matrix} b_{1}\\ b_{2}\\ b_{3} \end{matrix} \right ]" /></a>

It then uses LU decomposition to solve the system of equations Ax=b

**Input:** This function takes a mxn matrix A where the last column of A is the b vector.
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
  ```

**Output:** This function outputs a vector that corresponds to the x vector in Ax=b.
	
**Usage/Example:**

This function was initalized with the following driving code:
```c++
    double dx,dy;
    vector<double> xb(2);
    vector<double> yb(2);
    vector<double> uxb(2);
    vector<double> uyb(2);
    dx=0.25;
    dy=0.25;
    //These specify the bounds of the interval 0 index corresponds
    // to the lower bound, 1 index corresponds to the upper bound
    xb[0]=0.0;
    xb[1]=1.0;
    yb[0]=0.0;
    yb[1]=1.0;
    //These specify the boundry conditions 0 index corresponds
    // to the lower bound, 1 index corresponds to the upper bound
    uxb[0]=0;
    uxb[1]=0;
    uyb[0]=0;
    uyb[1]=0;

    //mesher2D(dx,dy,xb,yb);
    aLUb(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));

    return 0;
```

The results on the screen were as follows:

```c++
MESH
X     0  0.25   0.5  0.75     1
Y     0  0.25   0.5  0.75     1
function
         0         0         0         0         0
         0 0.0624593  0.124675  0.186403  0.247404
         0  0.124675  0.247404  0.366273  0.479426
         0  0.186403  0.366273  0.533303  0.681639
         0  0.247404  0.479426  0.681639  0.841471
A MATRIX
       -64        16         0        16         0         0         0         0         0 0.0624593
        16       -64        16         0        16         0         0         0         0  0.124675
         0        16       -64         0         0        16         0         0         0  0.186403
        16         0         0       -64        16         0        16         0         0  0.124675
         0        16         0        16       -64        16         0        16         0  0.247404
         0         0        16         0        16       -64         0         0        16  0.366273
         0         0         0        16         0         0       -64        16         0  0.186403
         0         0         0         0        16         0        16       -64        16  0.366273
         0         0         0         0         0        16         0        16       -64  0.533303
These are the x values
-0.00606555
-0.0101793
-0.00960623
-0.0101793
-0.0172531
-0.0165955
-0.00960623
-0.0165955
-0.0166306
```
**Implementation/Code:** The following is the code for aLUb()
```c++
vector<double> aLUb(vector<vector<double> > A){
	/*---------------------------------------------------------
	This function accepts a matrix of the form:

	a a a | b
	a a a | b
	a a a | b

    Where the b vector is the last column of the matrix.
	----------------------------------------------------------*/
	int am=A.size();
	int an=A[0].size();
	vector<double> a(am);
	vector<vector<double> > U(am, a);
	vector<vector<double> > L(am, a);
	vector<double> y(am);

	// Decomposing matrix into Upper and Lower
	// triangular matrix
	for (int i = 0; i < am; i++) {

		// Upper Triangular
		for (int k = i; k < am; k++) {

			// Summation of L(i, j) * U(j, k)
			double sum = 0;
			for (int j = 0; j < i; j++)
				sum += (L[i][j] * U[j][k]);

			// Evaluating U(i, k)
			U[i][k] = A[i][k] - sum;
		}

		// Lower Triangular
		for (int k = i; k < am; k++) {
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
	// setw is for displaying
	cout << setw(6) << "      Lower Triangular"
		 << setw(32) << "Upper Triangular" << endl;

	// Displaying the result :
	for (int i = 0; i < am; i++) {
		// Lower
		for (int j = 0; j < am; j++)
			cout << setw(6) << L[i][j] << "\t";
		cout << "\t";

		// Upper
		for (int j = 0; j < am; j++)
			cout << setw(6) << U[i][j] << "\t";
		cout << endl;
	}
	*/


	// Lower back substitution
	for (int i = 0; i < am; i++) {
		double s = 0;
		for (int j = 0; j < i; j++) {
			s = s + L[i][j] * y[j];
		}
		y[i] = (A[i][an-1] - s) / L[i][i];
	}

	/*
	//Print out y vector
	for (int i = 0; i < am; i++) {
		cout << y[i] << endl;
	}
	*/

	//Upper back substition
	for (int i = am-1; i >= 0; i--) {
		double s = 0;
		for (int j = am-1; j > i; j--) {
			s = s + U[i][j] * y[j];
		}
		y[i] = (y[i] - s) / U[i][i];
	}


	//Print out y vector
	cout << "These are the x values " << endl;
	for (int i = 0; i < am; i++) {
		cout << y[i] << endl;
	}


	return y;
}
```
