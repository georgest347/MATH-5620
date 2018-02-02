**Function Name:**         maxVectElem()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes a vector x and finds the maximum element value. 

*Input:** This function accepts a vector x which is mx1
  
**Output:** This function outputs the maximum element value

**Usage/Example:** This is an example of using this function

Input vector:
```c++
 x={1,2,3,4};
```

Driving code:
```c++
 int m=4;
  vector<double> x(m);
  for (int i = 0; i < m; i++) {
		x[i] = i + 1;
	}
  cout<<maxVectElem<<endl;
 ```
Output on screen:
```c++
  4
```
**Implimentation/Code:** The following is the code for maxVectElem():
```c++
double maxVectElem(vector<double> x) {
	/*--------------------------------
	This function takes a vector, and 
	finds the max element value.
	*/
	int m = x.size();

	/*
	//See the vector passed
	for (int i = 0; i < m; i++) {
		cout << x[i] << endl;
	}
	*/

	double max=-10000000000000;

	for (int i = 0; i < m; i++) {
		if (x[i]>=max) {
			max = x[i];
		}
	}
	return max;
}
```
