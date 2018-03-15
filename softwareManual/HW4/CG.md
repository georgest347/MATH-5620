**Function Name:**          CG()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes a matrix of form:

<a href="https://www.codecogs.com/eqnedit.php?latex=A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" title="A=\left [ \left.\begin{matrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} &a_{23} \\ a_{31} &a_{32} &a_{33} \end{matrix}\right| \begin{matrix} b_{1}\\ b_{2}\\ b_{3} \end{matrix} \right ]" /></a>

It then uses Conjugate Gradient method to solve the system of equations Ax=b

The general formula for the CG Iteration method is:

<a href="https://www.codecogs.com/eqnedit.php?latex=\phi&space;(u)=\frac{1}{2}u^{T}Au-u^{T}f" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\phi&space;(u)=\frac{1}{2}u^{T}Au-u^{T}f" title="\phi (u)=\frac{1}{2}u^{T}Au-u^{T}f" /></a>

This method is an iterative solver that iterates for a given number of iterations, or untill the errror reaches some user specified tolerance. 

This function calls the following functions:
[multiplyMV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/multiplyMV) 
[multiplyVTV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplyVTV) 
[multiplySV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplySV) 
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
    dy=dx;
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

    //aLUb(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));


    //aLUb(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));
    gaussSeidel(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));
    jacobiIter(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));
    CG(lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb));

    return 0;
```

The results on the screen were as follows:

```c++
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

Conjugate Gradient solved in 5 Iterations and 40 operations
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

It can be seen that both solvers find the same values. If a higher degree of accuracy is needed, the tolerance of the mehtod can be changed to be smaller. 

**Implementation/Code:** The following is the code for CG()
```c++
    /*---------------------------------------
    This function uses the Conjugate Gradient
    method to solve the system of equations
    Ax=b. The A matrix passed in has the b
    vector as the last row.
    ---------------------------------------*/
    int am=A.size(); //number of rows
	int an=A[0].size(); //number of columns
	vector<double> xnew(am);
	vector<double> xold(am);
	vector<double> pold(am);
	vector<double> pnew(am);
	vector<double> rold(am);
	vector<double> rnew(am);
	vector<double> w(am);
	double alpha;
	double beta;

    rold=multiplyMV(A,xold);
	for(int i=0;i<am;i++){
        rold[i]=A[i][an-1]-rold[i]; //<--equation used: r=b-Au
	}
	pold=rold;

	int iter=0;
    int maxiter=100000;
	double tol=0.000001;
    double error=10000000000000;
    int p=1;
    int opcount=0;
	while(iter<maxiter&&error>=tol){
        w=multiplyMV(A,pold);
        alpha=(multiplyVTV(pold,rold)/(multiplyVTV(pold,multiplyMV(A,pold))));
        for(int i=0;i<am;i++){
            xnew[i]=xold[i]+multiplySV(alpha,pold)[i];
            rnew[i]=rold[i]-multiplySV(alpha,w)[i];
        }
        error=pNormVect(rnew,p);
        beta=(multiplyVTV(rnew,rnew)/(multiplyVTV(rold,rold)));
        for(int i=0;i<am;i++){
            pnew[i]=rnew[i]+multiplySV(beta,pold)[i];
        }
        xold=xnew;
        pold=pnew;
        rold=rnew;
        opcount=opcount+8;
        iter++;
	}

	//Print out x vector
    cout<<"Conjugate Gradient solved in "<<iter<<" Iterations and "<<opcount<<" operations "<<endl;
	cout << "These are the x values " << endl;
	for (int i = 0; i < am; i++) {
		cout << xnew[i] << endl;
	}
	cout<<endl;

    return  xnew;
}
```
