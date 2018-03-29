**Function Name:**          anasol1()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function provides the analytic solution to the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=u'=\lambda&space;u" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u'=\lambda&space;u" title="u'=\lambda u" /></a>

This differential equation has the following inital condition:

<a href="https://www.codecogs.com/eqnedit.php?latex=u(t_{0})=u_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(t_{0})=u_{0}" title="u(t_{0})=u_{0}" /></a>

The exact solution used in this code is of the form:

<a href="https://www.codecogs.com/eqnedit.php?latex=u(t)=u_{0}e^{\lambda&space;t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(t)=u_{0}e^{\lambda&space;t}" title="u(t)=u_{0}e^{\lambda t}" /></a>

This function calls the following functions:
[multiplySV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplySV) 

**Input:** This function takes the following inputs:
x: The constant value in the Differential Equation
t: a time vector which can be made with [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)
u0: the inital value of the IVP problem.
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <math.h> //<-- to compute the exp
  ```

**Output:** This function outputs a vector 'u' that is the exact solution to the equation specified above.
	
**Usage/Example:**
This program is used to solve the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=u'=0.85u" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u'=0.85u" title="u'=0.85u" /></a>

This function was initalized with the following driving code:
```c++
   int main()
{
    vector<double> t(2);
    t[0]=0;
    t[1]=10;
    int n=25;
    double x=0.85;
    double u0=19.0;
    double P0=25;
   
    anasol1(x,mesher1D(t,n),u0);
    
    return 0;
}
```

The results on the screen were as follows:

```c++
Analytic 1.IVP
19
26.694
37.5037
52.6907
74.0277
104.005
146.122
205.293
288.426
405.224
569.318
799.862
1123.76
1578.83
2218.17
3116.42
4378.4
6151.42
8642.43
12142.2
17059.1
23967.1
33672.6
47308.2
66465.5
93380.6
```

**Implementation/Code:** The following is the code for anasol1()
```c++
vector<double> anasol1(double x, vector<double> t, double u0){
    // This function produces the analytic solution for the following IVP
    // u'=xu , u(t.0)=u.0
    // The exact analytic solution takes the form:
    // u(t)=(u.0)*exp(x*t);

    int m= t.size();
    vector<double> u(m);
    u=multiplySV(x,t);
    for(int i=0;i<m;i++){
        u[i]=exp(u[i]);
    }
    u=multiplySV(u0,u);

    cout<<"Analytic 1.IVP"<<endl;
    for(int i=0;i<m;i++){
        cout<<u[i]<<endl;
    }
    cout<<endl;

    return u;
}
```
