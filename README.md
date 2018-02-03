# MATH-5620
George Staples
Numerical solutions of Differential Equations

All code for Math 5620:

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
| 9        | [Null](https://georgest347.github.io/MATH-5620/softwareManual/HW1/SOLDE)                      | Solves spring mass model LDE                 |

## INDEX

| Type | Function Name      | Description                                  |
| :------: |:------------------:| :------------------------------------------: |
| **:---BASIC---:** |:------------------:| :------------------------------------------: |
| Basic        | [compEpsilon](https://georgest347.github.io/MATH-5620/softwareManual/HW1/compEpsilon)          | Finds the Machine Epsilon    |
| Basic        | [factorial](https://georgest347.github.io/MATH-5620/softwareManual/HW2/factorial)          | Finds the factorial of a given number   |
| Basic       | [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/functInital)      | Initalizes the problem u"=f(x) takes care of f(x)    |
| Basic vector        | [absMaxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absMaxVectElem)            | Finds the absolute maximum value of an element in a vector |
| Basic vector        | [maxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem)            | Finds the maximum value of an element in a vector |
| **:---ERROR---:** |:------------------:| :------------------------------------------: |
| Error        | [absoluteError](https://georgest347.github.io/MATH-5620/softwareManual/HW1/absoluteError)      | Returns the aboslute error of two numbers    |
| Error        | [absoluteErrorNormal](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal)            | Finds the absolute normalized error value |
| Error        | [relativeError](https://georgest347.github.io/MATH-5620/softwareManual/HW1/relativeError)      | Returns the relative error of two numbers    |
| Error Vect       | [pNormVect](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVect)                      | Finds the p Norm of a vector|
| Error Vect       | [pNormVDiff](https://georgest347.github.io/MATH-5620/softwareManual/HW2/pNormVDiff)                      | Finds the p Norm of the difference of two vectors|
| **:---SOLVERS---:** |:------------------:| :------------------------------------------: |
| DESolver        | [logisticDE](https://georgest347.github.io/MATH-5620/softwareManual/HW1/logisticDE)            | Computes the value of the logistic DE at 't' |
| DESolver        | [SOLDE](https://georgest347.github.io/MATH-5620/softwareManual/HW1/SOLDE)                      | Solves spring mass model LDE                 |
| DESolver        | [fdCoeffV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/fdCoeffV)          | Finds Coefficients for finite Difference    |                |
| LASolver       | [luDecomposition](https://georgest347.github.io/MATH-5620/softwareManual/HW2/luDecomposition)          | Solves the Ax=b matrix with LU Decomposition    |
| LASolver        | [multiplyMV](https://georgest347.github.io/MATH-5620/softwareManual/HW2/multiplyMV)            | Multiplies a matrix by a vector |
| LASolver TRI        | [jacobiTri](https://georgest347.github.io/MATH-5620/softwareManual/HW2/jacobiTri)            | Solves a tridiagonal symetric matrix using Jacobi Iteration |
| LASolver TRI        | [thomasMatrix](https://georgest347.github.io/MATH-5620/softwareManual/HW2/thomasMatrix)      | Uses the Thomas Algorithm to solve a tridiagonal symetric matrix   |
| LASolver TRI        | [triLUDecomp](https://georgest347.github.io/MATH-5620/softwareManual/HW2/triLUDecomp)            | Solves a tridiagonal symetric matrix using LU decomposition |
| **:---INITALIZERS---:** |:------------------:| :------------------------------------------: |        
| DEInitalizer        | [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital)      | Initalizes the problem u"=f(x)    |
