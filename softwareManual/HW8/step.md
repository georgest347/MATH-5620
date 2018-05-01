**Function Name:**          step()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function provides the boundry conditions for the hyperbolic differential equations.

**Input:** This function takes the following inputs:\
x=the current x value from a FD method.
xlength=the final x value
  
**Output:** This function outputs a single value for the FD method to use in the Boundry conditions

**Usage/Example:**
This function was passed the following parameters:

```c++
  x=1;
  xlength=10;
```

The results of the code are shown below:

```c++
  ans=1
```

**Implementation/Code:** The following is the code for step()
```c++
double step(double x,double xlength){
    double ans;
    if (x<(xlength/2)){
        ans=1;
    }
    else{
        ans=0;
    }

    return ans;
}

```
