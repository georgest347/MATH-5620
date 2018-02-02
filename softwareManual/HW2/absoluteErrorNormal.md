**Function Name:**          absoluteErrorNormal()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes two numbers and finds the normalized abolute error of the two. The following equation is used:

<a href="https://www.codecogs.com/eqnedit.php?latex=e_{n}=\left&space;|&space;\frac{realValue-approxValue}{realValue}&space;\right&space;|" target="_blank"><img src="https://latex.codecogs.com/gif.latex?e_{n}=\left&space;|&space;\frac{realValue-approxValue}{realValue}&space;\right&space;|" title="e_{n}=\left | \frac{realValue-approxValue}{realValue} \right |" /></a>

*Input:** This function accepts two double numbers:
realValue: The real value of the function. If f(x)=x^2 and x=2 the real value would be 4
ApproxValue: The approximation of a function value. If f(x)=x^2 an approximation of x=2 might be 4.1.
  
**Output:** This function outputs the normalized absolute error value.

**Usage/Example:** The following is the code for absoluteErrorNormal():

```c++
double absoluteErrorNormal(double realValue, double approxValue) {
	double absError = abs((realValue - approxValue) / realValue);
	return absError;
}
```
