**Function Name:**         absMaxVectElem()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes a vector x and finds the maximum absolute element value. 

*Input:** This function accepts a vector x which is mx1
  
**Output:** This function outputs the maximum absolute element value

**Usage/Example:** This is an example of using this function

Input vector:
```c++
 x={-1,0,1,-4};
```
Output on screen:
```c++
  4
```
**Implimentation/Code:** The following is the code for absMaxVectElem():
```c++
double absMaxVectElem(vector<double> x) {
	/*--------------------------------
	This function takes a vector, and
	finds the max absolute element value.
	*/
	int m = x.size();

	/*
	//See the vector passed
	for (int i = 0; i < m; i++) {
	cout << x[i] << endl;
	}
	*/

	double max = -10000000000000;

	for (int i = 0; i < m; i++) {
		if (abs(x[i]) >= max) {
			max = abs(x[i]);
		}
	}
	return max;
}
```
