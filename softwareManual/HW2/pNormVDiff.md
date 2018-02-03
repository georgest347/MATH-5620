**Function Name:**         pNormVDiff()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function finds the p norm of a difference of two vectors by using the following equation. In this equation x represents the actual vector, and y represents the estimated vector.

<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;\|&space;d&space;\right&space;\|_{p&space;}=\left&space;(&space;\sum_{i}^{n}\left&space;|&space;x_{i}-y_{i}&space;\right&space;|^{p}&space;\right&space;)^{1/p}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;\|&space;d&space;\right&space;\|_{p&space;}=\left&space;(&space;\sum_{i}^{n}\left&space;|&space;x_{i}-y_{i}&space;\right&space;|^{p}&space;\right&space;)^{1/p}" title="\left \| d \right \|_{p }=\left ( \sum_{i}^{n}\left | x_{i}-y_{i} \right |^{p} \right )^{1/p}" /></a>

When p=infinity, this function uses the following equation to find the norm. This function accesses [maxVectElem](https://georgest347.github.io/MATH-5620/softwareManual/HW2/maxVectElem) to find the absolute max value of the difference of two vectors. 

<a href="https://www.codecogs.com/eqnedit.php?latex=\left&space;\|&space;d&space;\right&space;\|_{\infty&space;}=max_{i}\left&space;|&space;x_{i}-y_{i}&space;\right&space;|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\left&space;\|&space;d&space;\right&space;\|_{\infty&space;}=max_{i}\left&space;|&space;x_{i}-y_{i}&space;\right&space;|" title="\left \| d \right \|_{\infty }=max_{i}\left | x_{i}-y_{i} \right |" /></a>

For the user to access the infinity norm, they must pass the function p=0. For the pNorm p=0 would cause a divide by 0 error, so p=0 is able to access the infinty norm. 

*Input:** This function accepts a vector x which is mx1, and a vector y which is mx1 and a double p which corresponds to the p norm. p=0 for infinity norm.
  
**Output:** This function outputs the norm value

**Usage/Example:** This is an example of using this function

Input vector:
```c++
 x={1,2,-3};
 y={0,1,2};
 p=1;
 p=2;
 p=0;
```
Output on screen:
```c++
   7
   5.19615
   5   
```
**Implimentation/Code:** The following is the code for pNormVDiff():
```c++
double pNormVDiff(vector<double> act, vector<double> est, double p) {
	/*---------------------------------
	This function finds the p norm of the
	difference between two vectors, and 
	returns the value. This function takes
	two vectors, the first is the actual
	value and the second is the estimated
	value of the vector. 
	
	This function uses
	p=0 as the infinity norm because by 
	definition, p=0 would cause	a divide 
	by 0 error. Therefore, p=0 corresponds
	to the infinity norm for this function.

	*/
	double norm = 0;
	int m = act.size();
	vector<double> diff(m);

	//Calculate the absolue difference
	//between the actual value and the estimated value.
	for (int i = 0; i < m; i++) {
		diff[i] =abs( act[i] - est[i]);
	}
	
	// Used for the infinity norm
	if (p == 0) {
		norm = maxVectElem(diff);
		return norm;
	}

	// Used for the p norm where p!=0;
	else {
		for (int i = 0; i < m; i++) {
			norm = norm + pow(diff[i], p);
		}
		//Change p value to use for 1/p of sum
		p = 1 / p;

		norm = pow(norm, p);

		return norm;
	}
}
```
