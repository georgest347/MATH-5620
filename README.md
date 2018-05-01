# MATH-5620
George Staples
Numerical solutions of Differential Equations

All code for Math 5620:

## INDEX

| Type | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| **:---BASIC---:** |:------------------:| :------------------------------------------: |
| Basic        | [anasol1](https://georgest347.github.io/MATH-5620/softwareManual/HW5/anasol1)          | Provides the analytic solution to u'=xu    |
| Basic        | [anasol2](https://georgest347.github.io/MATH-5620/softwareManual/HW5/anasol2)          | Provides the analytic solution to P'=y*P-B*P^2    |
| Basic        | [compEpsilon](https://georgest347.github.io/MATH-5620/softwareManual/HW1/compEpsilon)          | Finds the Machine Epsilon    |
| Basic        | [factorial](https://georgest347.github.io/MATH-5620/softwareManual/HW2/factorial)          | Finds the factorial of a given number   |
| Basic       | [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/functInital)      | Initalizes the problem u"=f(x) takes care of f(x)    |
| Basic       | [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW3/functInital)                      | Initalizes f(x,y) for laplacian equation           |
| Basic       | [g1](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g1)          | Provides boundry condition for heatEE1D |
| Basic      | [g2](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g2)          | Provides boundry condition for heatEE1D  |
| Basic        | [hyperSoln](https://georgest347.github.io/MATH-5620/softwareManual/HW8/hyperSoln)          | Provides exact solution to the advection PDE   |
| Basic vector        | [absMaxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absMaxVectElem)            | Finds the absolute maximum value of an element in a vector |
| Basic vector        | [maxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem)            | Finds the maximum value of an element in a vector |
| **:---ERROR---:** |:------------------:| :------------------------------------------: |
| Error        | [absoluteError](https://georgest347.github.io/MATH-5620/softwareManual/HW1/absoluteError)      | Returns the aboslute error of two numbers    |
| Error        | [absoluteErrorNormal](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal)            | Finds the absolute normalized error value |
| Error        | [relativeError](https://georgest347.github.io/MATH-5620/softwareManual/HW1/relativeError)      | Returns the relative error of two numbers    |
| Error Mat       | [matNorm](https://georgest347.github.io/MATH-5620/softwareManual/HW3/matNorm)          | Finds the 1 and infinty norms of a Matrix    |
| Error Vect       | [pNormVect](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVect)                      | Finds the p Norm of a vector|
| Error Vect       | [pNormVDiff](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVDiff)                      | Finds the p Norm of the difference of two vectors|
| **:---INITALIZERS---:** |:------------------:| :------------------------------------------: |        
| DEInitalizer        | [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital)      | Initalizes the problem u"=f(x)    |
| DEInitalizer        | [ellipODEcoI](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipODEcoI)                      | Initalizes the problem (d/dx)k(x)(du/dx)=f(x) |
| DEInializer      | [lapInital](https://georgest347.github.io/MATH-5620/softwareManual/HW3/lapInital)            | Initalizes the Laplacian equation (del)u=f(x,y)|
| DEInitalizer        | [lapInital9pt](https://georgest347.github.io/MATH-5620/softwareManual/HW3/lapInital9pt)                      | Initalizes the Laplacian equation (del)u=f(x,y) with 9pt method              |
| PDEInitalizer        | [initalCon](https://georgest347.github.io/MATH-5620/softwareManual/HW8/initalCon)          | Provides inital Conditions to the advection PDE   |
| PDEInitalizer       | [step](https://georgest347.github.io/MATH-5620/softwareManual/HW8/step)          | Provides the boundry conditions for the PDE   |
| MESH       | [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)          | creates a 1D mesh  | 
| MESH        | [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)                      | Makes a 2D mesh                |
| PAR       | [functInial](https://georgest347.github.io/MATH-5620/softwareManual/HW7/functInial)          | Solve the 1D heat equation using RK4  |
| **:---MATRIX/VECTOR MANIPULATION---:** |:------------------:| :------------------------------------------: |
| MAT        | [powerEig](https://georgest347.github.io/MATH-5620/softwareManual/HW3/powerEig)      | Finds the Max eigen value of a Matrix    |
| MAT/VEC       | [multiplyMV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/multiplyMV)            | Multiplies a matrix by a vector |
| VEC        | [dotProd](https://georgest347.github.io/MATH-5620/softwareManual/HW3/dotProd)      | Finds the dot product of two vectors    |
| VEC       | [multiplySV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplySV)          | multiplies a scalar into a vector  | 
| VEC       | [multiplyVTV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplyVTV)          | multiplies a transpose vector by another vector to get a scalar  |
| **:---SOLVERS---:** |:------------------:| :------------------------------------------: |
| DESolver        | [logisticDE](https://georgest347.github.io/MATH-5620/softwareManual/HW1/logisticDE)            | Computes the value of the logistic DE at 't' |
| DESolver        | [SOLDE](https://georgest347.github.io/MATH-5620/softwareManual/HW1/SOLDE)                      | Solves spring mass model LDE                 |
| DESolver        | [fdCoeffV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/fdCoeffV)          | Finds Coefficients for finite Difference    |                |
| HYPER       | [hyperLWM](https://georgest347.github.io/MATH-5620/softwareManual/HW8/hyperLWM)          | Uses Lax-Wendroff method to solve the advection PDE   |
| HYPER      | [hyperWB](https://georgest347.github.io/MATH-5620/softwareManual/HW8/hyperWB)          | Uses WArming and Beam method to solve the advection PDE   |
| HYPER        | [upwind](https://georgest347.github.io/MATH-5620/softwareManual/HW8/upwind)          | Uses Upwind method to solve the advection PDE   |
| LASolver   | [aLUb](https://georgest347.github.io/MATH-5620/softwareManual/HW3/aLUb)      | Solves a matrix with Lu decomposition    |
| LASolver      | [CG](https://georgest347.github.io/MATH-5620/softwareManual/HW4/CG)          | Solves a matrix system using the Conjugate Gradient method  |
| LASolver        | [gaussSeidel](https://georgest347.github.io/MATH-5620/softwareManual/HW4/gaussSeidel)          | Solves a matrix system using Gauss-Seidel method    |                |
| LASolver       | [luDecomposition](https://georgest347.github.io/MATH-5620/softwareManual/HW2/luDecomposition)          | Solves the Ax=b matrix with LU Decomposition    |
| LASolver        | [jacobiIter](https://georgest347.github.io/MATH-5620/softwareManual/HW4/jacobiIter)          | Solves a matrix system using JacobiIteration method  |     
| LASolver TRI        | [jacobiTri](https://georgest347.github.io/MATH-5620/softwareManual/HW2/jacobiTri)            | Solves a tridiagonal symetric matrix using Jacobi Iteration |
| LASolver TRI        | [thomasMatrix](https://georgest347.github.io/MATH-5620/softwareManual/HW2/thomasMatrix)      | Uses the Thomas Algorithm to solve a tridiagonal symetric matrix   |
| LASolver TRI        | [triLUDecomp](https://georgest347.github.io/MATH-5620/softwareManual/HW2/triLUDecomp)            | Solves a tridiagonal symetric matrix using LU decomposition |
| IVP       | [eulerExIV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/eulerExIV)          | Solves an IVP using the explicit euler method  |
| IVP.HW5        | [eulerExIV](https://georgest347.github.io/MATH-5620/softwareManual/HW5/eulerExIV)          | Provides the numerical solution to IVP using Explicit Euler    |
| IVP      | [eulerIMIV](https://georgest347.github.io/MATH-5620/softwareManual/HW5/eulerIMIV)          | Provides the numerical solution to IVP using Implicit Euler    |
| IVP        | [PC3O](https://georgest347.github.io/MATH-5620/softwareManual/HW5/PC3O)          | Provides the numerical solution to IVP using order 3 predictor corrector method    |
| IVP        | [RK2](https://georgest347.github.io/MATH-5620/softwareManual/HW5/RK2)          | Provides the numerical solution to IVP using Runge Kutta order 2    |
| IVP        | [Rk4](https://georgest347.github.io/MATH-5620/softwareManual/HW5/RK4)          | Provides the numerical solution to IVP using Runge Kutta order 4    |
| PAR        | [heatEE1D](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatEE1D)          | Solve the 1D heat equation Explicit Euler   |
| PAR     | [heatIE1D](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatIE1D)          | Solve the 1D heat equation Implicit Euler   |
| PAR        | [heatPC](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatPC)          | Solve the 1D heat equation using PC  |
| PAR       | [heatRK4](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatRK4)          | Solve the 1D heat equation using RK4  |

## HW 1

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 2        | [compEpsilon](https://georgest347.github.io/MATH-5620/softwareManual/HW1/compEpsilon)          | Finds the Machine Epsilon    |                |
| 4        | [absoluteError](https://georgest347.github.io/MATH-5620/softwareManual/HW1/absoluteError)      | Returns the aboslute error of two numbers    |
| 4        | [relativeError](https://georgest347.github.io/MATH-5620/softwareManual/HW1/relativeError)      | Returns the relative error of two numbers    |
| 6        | [logisticDE](https://georgest347.github.io/MATH-5620/softwareManual/HW1/logisticDE)            | Computes the value of the logistic DE at 't' |
| 7        | [SOLDE](https://georgest347.github.io/MATH-5620/softwareManual/HW1/SOLDE)                      | Solves spring mass model LDE                 |

## HW 2

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 1        | [fdCoeffV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/fdCoeffV)          | Finds Coefficients for finite Difference    |                |
| 1.a       | [luDecomposition](https://georgest347.github.io/MATH-5620/softwareManual/HW2/luDecomposition)          | Solves the Ax=b matrix with LU Decomposition    |                |
| 1.b        | [factorial](https://georgest347.github.io/MATH-5620/softwareManual/HW2/factorial)          | Finds the factorial of a given number   |                |
| 3        | [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital)      | Initalizes the problem u"=f(x)    |
| 3.a       | [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/functInital)      | Initalizes the problem u"=f(x) takes care of f(x)    |
| 4        | [thomasMatrix](https://georgest347.github.io/MATH-5620/softwareManual/HW2/thomasMatrix)      | Uses the Thomas Algorithm to solve a tridiagonal symetric matrix   |
| 5        | [triLUDecomp](https://georgest347.github.io/MATH-5620/softwareManual/HW2/triLUDecomp)            | Solves a tridiagonal symetric matrix using LU decomposition |
| 6        | [jacobiTri](https://georgest347.github.io/MATH-5620/softwareManual/HW2/jacobiTri)            | Solves a tridiagonal symetric matrix using Jacobi Iteration |
| 6.a        | [multiplyMV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/multiplyMV)            | Multiplies a matrix by a vector |
| 6.b        | [absoluteErrorNormal](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal)            | Finds the absolute normalized error value |
| 6.c        | [maxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem)            | Finds the maximum value of an element in a vector |
| 6.d        | [absMaxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absMaxVectElem)            | Finds the absolute maximum value of an element in a vector |
| 8        | [pNormVect](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVect)                      | Finds the p Norm of a vector|
| 8.a        | [pNormVDiff](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVDiff)                      | Finds the p Norm of the difference of two vectors|
| 9        | [ellipODEcoI](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipODEcoI)                      | Initalizes the problem (d/dx)k(x)(du/dx)=f(x) |

## HW 3

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 1        | [matNorm](https://georgest347.github.io/MATH-5620/softwareManual/HW3/matNorm)          | Finds the 1 and infinty norms of a Matrix    |                |
| 2        | [powerEig](https://georgest347.github.io/MATH-5620/softwareManual/HW3/powerEig)      | Finds the Max eigen value of a Matrix    |
| 2.a        | [dotProd](https://georgest347.github.io/MATH-5620/softwareManual/HW3/dotProd)      | Finds the dot product of two vectors    |
| 5        | [aLUb](https://georgest347.github.io/MATH-5620/softwareManual/HW3/aLUb)      | Solves a matrix with Lu decomposition    |
| 5.a       | [lapInital](https://georgest347.github.io/MATH-5620/softwareManual/HW3/lapInital)            | Initalizes the Laplacian equation (del)u=f(x,y)|
| 5.b        | [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)                      | Makes a 2D mesh                |
| 5.c        | [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW3/functInital)                      | Initalizes f(x,y) for laplacian equation           |
| 6        | [lapInital9pt](https://georgest347.github.io/MATH-5620/softwareManual/HW3/lapInital9pt)                      | Initalizes the Laplacian equation (del)u=f(x,y) with 9pt method              |

## HW 4

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 1        | [gaussSeidel](https://georgest347.github.io/MATH-5620/softwareManual/HW4/gaussSeidel)          | Solves a matrix system using Gauss-Seidel method    |                
| 1.a        | [jacobiIter](https://georgest347.github.io/MATH-5620/softwareManual/HW4/jacobiIter)          | Solves a matrix system using JacobiIteration method  |                
| 2,3       | [CG](https://georgest347.github.io/MATH-5620/softwareManual/HW4/CG)          | Solves a matrix system using the Conjugate Gradient method  |
| 2.a       | [multiplyVTV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplyVTV)          | multiplies a transpose vector by another vector to get a scalar  | 
| 2.b       | [multiplySV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplySV)          | multiplies a scalar into a vector  |
| 4       | [eulerExIV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/eulerExIV)          | Solves an IVP using the explicit euler method  | 
| 4.a       | [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)          | creates a 1D mesh  | 

## HW 5

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 1        | [anasol1](https://georgest347.github.io/MATH-5620/softwareManual/HW5/anasol1)          | Provides the analytic solution to u'=xu    |
| 1.a        | [anasol2](https://georgest347.github.io/MATH-5620/softwareManual/HW5/anasol2)          | Provides the analytic solution to P'=y*P-B*P^2    |
| 2        | [eulerExIV](https://georgest347.github.io/MATH-5620/softwareManual/HW5/eulerExIV)          | Provides the numerical solution to IVP using Explicit Euler    |
| 3        | [eulerIMIV](https://georgest347.github.io/MATH-5620/softwareManual/HW5/eulerIMIV)          | Provides the numerical solution to IVP using Implicit Euler    |
| 4        | [RK2](https://georgest347.github.io/MATH-5620/softwareManual/HW5/RK2)          | Provides the numerical solution to IVP using Runge Kutta order 2    |
| 4.a        | [Rk4](https://georgest347.github.io/MATH-5620/softwareManual/HW5/RK4)          | Provides the numerical solution to IVP using Runge Kutta order 4    |
| 5        | [PC3O](https://georgest347.github.io/MATH-5620/softwareManual/HW5/PC3O)          | Provides the numerical solution to IVP using order 3 predictor corrector method    |
| data       | [DATA](https://github.com/georgest347/MATH-5620/blob/master/softwareManual/HW5/HW5.xlsx)          | This is the data collected from running all methods to solve two IVP    |

## HW 7

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 1        | [heatEE1D](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatEE1D)          | Solve the 1D heat equation Explicit Euler   |
| 1.a        | [g1](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g1)          | Provides boundry condition for heatEE1D  |
| 1.b        | [g2](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g2)          | Provides boundry condition for heatEE1D  |
| 2        | [heatIE1D](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatIE1D)          | Solve the 1D heat equation Implicit Euler   |
| 4        | [heatPC](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatPC)          | Solve the 1D heat equation using PC  |
| 5        | [heatRK4](https://georgest347.github.io/MATH-5620/softwareManual/HW7/heatRK4)          | Solve the 1D heat equation using RK4  |
| 5.a        | [functInial](https://georgest347.github.io/MATH-5620/softwareManual/HW7/functInial)          | Solve the 1D heat equation using RK4  |

## HW 8

| Problems | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| 1        | [hyperSoln](https://georgest347.github.io/MATH-5620/softwareManual/HW8/hyperSoln)          | Provides exact solution to the advection PDE   |
| 1.a        | [step](https://georgest347.github.io/MATH-5620/softwareManual/HW8/step)          | Provides the boundry conditions for the PDE   |
| 1.b        | [initalCon](https://georgest347.github.io/MATH-5620/softwareManual/HW8/initalCon)          | Provides inital Conditions to the advection PDE   |
| 1.c        | [upwind](https://georgest347.github.io/MATH-5620/softwareManual/HW8/upwind)          | Uses Upwind method to solve the advection PDE   |
| 1.d        | [hyperLWM](https://georgest347.github.io/MATH-5620/softwareManual/HW8/hyperLWM)          | Uses Lax-Wendroff method to solve the advection PDE   |
| 1.e        | [hyperWB](https://georgest347.github.io/MATH-5620/softwareManual/HW8/hyperWB)          | Uses WArming and Beam method to solve the advection PDE   |


