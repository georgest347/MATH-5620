**Function Name:**         pNormVect()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function finds the p norm of a vector by using the following equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;\|&space;x_{p}&space;\right&space;\|=\left&space;(\sum_{i}^{n}&space;\left&space;|x_{i}&space;\right&space;|^{p}&space;\right&space;)^{1/p}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;\|&space;x_{p}&space;\right&space;\|=\left&space;(\sum_{i}^{n}&space;\left&space;|x_{i}&space;\right&space;|^{p}&space;\right&space;)^{1/p}" title="\left \| x_{p} \right \|=\left (\sum_{i}^{n} \left |x_{i} \right |^{p} \right )^{1/p}" /></a>

When p=infinity, this function uses the following equation to find the norm.

<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;\|&space;x&space;\right&space;\|_{\infty&space;}=max_{i}\left&space;|&space;x_{i}&space;\right&space;|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;\|&space;x&space;\right&space;\|_{\infty&space;}=max_{i}\left&space;|&space;x_{i}&space;\right&space;|" title="\left \| x \right \|_{\infty }=max_{i}\left | x_{i} \right |" /></a>

For the user to access the infinity norm, they must pass the function p=0. For the pNorm p=0 would cause a divide by 0 error, so p=0 is able to access the infinty norm. 

*Input:** This function accepts a vector x which is mx1, and a double p which corresponds to the p norm. p=0 for infinity norm.
  
**Output:** This function outputs the norm value

**Usage/Example:** This is an example of using this function

Input vector:
```c++
 x={1,2,-3};
 p=1;
 p=2;
 p=0;
```
Output on screen:
```c++
   6
   3.74166
   3   
```
**Implimentation/Code:** The following is the code for pNormVect():
```c++
double pNormVect(vector<double> x, double p) {
	/*---------------------------------
	This function finds the p norm of a 
	vector, and returns the value. This 
	function uses p=0 as the infinity norm
	because by definition, p=0 would cause
	a divide by 0 error. Therefore, p=0 
	corresponds to the infinity norm for
	this function.

	*/
	double norm = 0;
	int m = x.size();
	

	// Used for the infinity norm
	if (p == 0) {
		norm=absMaxVectElem(x);
		return norm;
	}
	// Used for the p norm where p!=0;
	else {
		for (int i = 0; i < m; i++) {
			norm = norm + pow(abs(x[i]), p);
		}
		//Change p value to use for 1/p of sum
		p = 1 / p;

		norm = pow(norm, p);

		return norm;
	}
}
```
