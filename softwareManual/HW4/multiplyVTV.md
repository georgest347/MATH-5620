**Function Name:**          multiplyVTV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes transpose vector and multiplies it by another vector.

*Input:** This function accepts two vectors.
  
**Output:** This function outputs scalar

**Usage/Example:**

t={3,3]
v={9,9}

The result printed on the screen was:
```c++
54
```

**Implementation/Code:** The following is the code for multiplyVTV():

```c++
double multiplyVTV(vector<double> T, vector<double> V) {
	/*-----------------------------------------------------------
	This function takes a vector, and multiplies it by a transposed
	vector.
	*/
	int m = V.size();
	double sum=0;

	//Times the rows and columns
	for (int i = 0; i < m; i++) {
		sum=T[i]*V[i]+sum;
	}

	return sum;
}
```


