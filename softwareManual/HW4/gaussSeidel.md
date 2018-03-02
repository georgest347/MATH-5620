**Function Name:**          gaussSeidel()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes a matrix of form:

<a href="https://www.codecogs.com/eqnedit.php?latex=A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" title="A=\left [ \left.\begin{matrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} &a_{23} \\ a_{31} &a_{32} &a_{33} \end{matrix}\right| \begin{matrix} b_{1}\\ b_{2}\\ b_{3} \end{matrix} \right ]" /></a>

It then uses Gauss-Seidel to solve the system of equations Ax=b

The general formula for the Gauss-Seidel method is:

<a href="https://www.codecogs.com/eqnedit.php?latex=x_{i&plus;1}=(D&plus;U)^{-1}(b-Lx_{i})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_{i&plus;1}=(D&plus;U)^{-1}(b-Lx_{i})" title="x_{i+1}=(D+U)^{-1}(b-Lx_{i})" /></a>

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

    cout<<endl;
    cout<<"Gauss"<<endl;

    gaussSeidel(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));

    return 0;
```

The results on the screen were as follows:

```c++
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

Gauss
These are the x values
-0.00606555
-0.0101792
-0.00960623
-0.0101792
-0.017253
-0.0165955
-0.00960623
-0.0165955
-0.0166306
```

The upper values were found with [aLUb](), another matrix solver, the lower values were found with the Gauss Seidel method. These results are the same. If the tolerance was changed, the Gauss Seidel would approximate the solution better. 

**Implementation/Code:** The following is the code for gaussSeidel()
```c++
vector<double> gaussSeidel(vector<vector<double> > A){
    /*------------------------------------------------
    This function solves the matrix system of equations
    Ax=b by using Gauss Seidel method.
    using: A=L+U we can obtain the following equation:
    x(k+1)=L^(-1)*(b-U*x(k));
    which is an iterative scheme for solving the x vector

    ------------------------------------------------*/
    int am=A.size(); //number of rows
	int an=A[0].size(); //number of columns
	vector<double> xnew(am);
	vector<double> xold(am);

    //Iterative loop
    int iter=0;
    int maxiter=100;
    double error=10000000000000;
    double tol=0.0000001;
    int p=1; //Use to change which norm you are using for the error calculation, 0=infinity norm.
    while (iter <= maxiter&&error>tol)
    {
        for(int i=0;i<am;i++){
            xnew[i]=A[i][an-1]/A[i][i];
            for(int j=0;j<am;j++){
                if (i==j)
                continue;
                xnew[i]=xnew[i]-((A[i][j]/A[i][i]*xold[j]));
            }
        }
        //Calculate the error and increase the iterations
        error=absoluteErrorNormal(pNormVect(xnew,p),pNormVect(xold,p));
        iter++;
        xold=xnew;
    }

    //Print out x vector
	cout << "These are the x values " << endl;
	for (int i = 0; i < am; i++) {
		cout << xnew[i] << endl;
	}
    return xnew;

}
```
