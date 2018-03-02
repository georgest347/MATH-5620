**Function Name:**          jacobiIter()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes a matrix of form:

<a href="https://www.codecogs.com/eqnedit.php?latex=A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" title="A=\left [ \left.\begin{matrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} &a_{23} \\ a_{31} &a_{32} &a_{33} \end{matrix}\right| \begin{matrix} b_{1}\\ b_{2}\\ b_{3} \end{matrix} \right ]" /></a>

It then uses Jacobi Iteration to solve the system of equations Ax=b

The general formula for the Jacobi Iteration method is:

<a href="https://www.codecogs.com/eqnedit.php?latex=x_{i&plus;1}=(D)^{-1}(b-(L&plus;U)x_{i})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{i&plus;1}=(D)^{-1}(b-(L&plus;U)x_{i})" title="x_{i+1}=(D)^{-1}(b-(L+U)x_{i})" /></a>

This method is an iterative solver that iterates for a given number of iterations, or untill the errror reaches some user specified tolerance. 

This function calls the following functions for computing the error:

[absoluteErrorNormal](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal)

[pNormVect](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVect)


**Input:** This function takes a mxn matrix A where the last column of A is the b vector.
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <iomanip> //<-- to view the output data
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

    aLUb(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));

    gaussSeidel(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));

    jacobiIter(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));

    return 0;
```

The results on the screen were as follows:

```c++
LU decomposition
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

Gauss-Seidel solved in 38 Iterations
These are the x values
-0.00606553
-0.0101792
-0.00960622
-0.0101792
-0.017253
-0.0165955
-0.00960622
-0.0165955
-0.0166306

Jacobi solved in 38 Iterations
These are the x values
-0.00606553
-0.0101792
-0.00960622
-0.0101792
-0.017253
-0.0165955
-0.00960622
-0.0165955
-0.0166306

```

It can be seen that All three solvers find the same values. If a higher degree of accuracy is needed, the tolerance of the mehtod can be changed to be smaller. 

**Implementation/Code:** The following is the code for jacobiIter()
```c++
vector<double> jacobiIter(vector<vector<double> > A) {
	/*----------------------------------------------
	This function solves a system of equations using
	jacobi iteration.
	Au=b
	(L+D+U)u=b <-- Seperate the matrix into the addition
				of three matrices.
	L= lower triangle matrix
	D=Diagonal matrix
	U= upper-triangle matrix

	solve x at k+1 using a guess of x_0 =0

	x_k+1=D^-1*(b-(L+U)x_k)

	*/
    int am=A.size(); //number of rows
	int an=A[0].size(); //number of columns
	vector<double> xnew(am);
	vector<double> xold(am);

	//Matrix to hold the LU values
	vector<vector<double> > LU(am, xnew);

	// Initalize the LU Matrix
	for (int i = 0; i < am; i++) {
		for (int j = 0; j < am; j++) {
			if (i==j)
            continue;
			LU[i][j]=A[i][j];
		}
	}

    /*
	//See the LU Matrix
	cout << "LU Jacobi" << endl;
	for (int i = 0; i < am; i++) {
		for (int j = 0; j < am; j++) {
			cout <<setw(6)<< LU[i][j];
		}
		cout << endl;
	}
	cout << endl;
	*/


	// Iterates through finding the x values
	//int count = 0;
	//Change the error value to be smaller for better convergence
	double error=10000000000;
	int iter=0;
	int maxiter=10000;
	double tol=0.000001;
	int p=1; //<-- Use to find the p norm of the vectors for error. Use 0 for infinity norm.

	while (error >= tol && iter<=maxiter) {

		//multiplies (L+U)*x.i-1
		xnew = multiplyMV(LU, xold);

        //cout<<"XVECTOR"<<endl;
		//Solves new x values
		for (int i = 0; i < am; i++) {
			xnew[i] = (1/A[i][i]) * (A[i][an-1] - xnew[i]); // equation used x.i=D^-1*(b-(L+U)x.i-1)
            //cout<<xnew[i]<<endl;
		}
		//cout<<endl;

		error=absoluteErrorNormal(pNormVect(xnew,p),pNormVect(xold,p));

		xold=xnew;
		iter++;
	}

    //Print out x vector
    cout<<"Jacobi solved in "<<iter<<" Iterations"<<endl;
	cout << "These are the x values " << endl;
	for (int i = 0; i < am; i++) {
		cout << xnew[i] << endl;
	}
	cout<<endl;
	return xnew;
}
```
