**Function Name:**          functInital()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function is used by [ellipticODEInital](https://georgest347.github.io/MATH-5620/softwareManual/HW2/ellipticODEInital) to find the f(x) values for a user defined function.

**Input:** This function accepts a vector of x values, and n an integer specifying the length of x
  
**Output:** This function ouputs the f(x) values

**Usage/Example:** The following is the code for functInital() given that:

<a href="https://www.codecogs.com/eqnedit.php?latex=f(x)=x^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?f(x)=x^2" title="f(x)=x^2" /></a>

```c++
vector<double> functInital(vector<double> x, int n) {
	// Function that initalizes the f(x) values for the b vector
	for (int i = 0; i <= n; i++) {
		x[i] = x[i] * x[i];
	}
	return x;
}
```


