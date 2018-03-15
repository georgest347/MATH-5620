**Function Name:**          multiplySV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function takes scalar and multiplies it into a vector

*Input:** This function accepts a scalar and a vector
  
**Output:** This function outputs a vector

**Usage/Example:**
Given the following scalar and vector:

t={3,3]
double s=90;

The result printed on the screen was:
```c++
270
270
```

**Implementation/Code:** The following is the code for multiplySV():

```c++
vector<double> multiplySV(double S, vector<double> V) {
	/*-----------------------------------------------------------
	This function takes a vector, and multiplies it by a scalar
	*/
	int m = V.size();

	for (int i = 0; i < m; i++) {
        V[i]=S*V[i];
    }

	return V;
}
```


