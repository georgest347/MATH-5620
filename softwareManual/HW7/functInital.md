**Function Name:**          functInital()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function is used with the RK4 method for solving the heat equation in 1D

**Input:** This function takes the following inputs:\
i=current index number (space).\
dx=spatial incriment.\
k=thermal conductivity.\
u=vector of the temps at current time.\
  
**Output:** This function outputs a single value f which is the numerical result of the function.
	
**Usage/Example:**
Using the following inputs:
```c++
  k=10;
  dx=1;
  u=[0,1,2,3];
  i=1;
```

The code produced:
```c++
  f=0
```

**Implementation/Code:** The following is the code for g1()
```c++
double functInital(int i, double dx, double k,vector<double> u) {
	// Function that initalizes the f(t,y) values
	double f;
    f=(k/(dx*dx))*(u[i+1]-2*u[i]+u[i-1]); //f(P,t) for logistic model of population growth

	return f;
}
```
