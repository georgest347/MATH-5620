**Function Name:**          eulerExIV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves an initalvalue problem using the explicit euler method. The form of the problem is shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=y'=f(t,y),&space;y(t_{0})=y_{0}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y'=f(t,y),&space;y(t_{0})=y_{0}" title="y'=f(t,y), y(t_{0})=y_{0}" /></a>

The explicit euler method uses the following general formula to solve the next u values. This is a one step one left end point rule formula.

<a href="https://www.codecogs.com/eqnedit.php?latex=Y^{n&plus;1}=Y^{n}&plus;\Delta&space;tf(Y^{n}(t^{n}),t^{n})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y^{n&plus;1}=Y^{n}&plus;\Delta&space;tf(Y^{n}(t^{n}),t^{n})" title="Y^{n+1}=Y^{n}+\Delta tf(Y^{n}(t^{n}),t^{n})" /></a>

This function calls the following function:
[mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)
[functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW4/functInital)

**Input:** This function takes a mesh created by the 1D mesher, and the inital Y_0 value.
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <iomanip> //<-- to view the output data
      #include <cmath> //<-- to compute the exact solution
  ```

**Output:** This function outputs a vector of the Y values at the specified time step points.
	
**Usage/Example:**
This program is used to solve the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=y'=0.85y,&space;y(0)=19" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y'=0.85y,&space;y(0)=19" title="y'=0.85y, y(0)=19" /></a>

The exact solution was found to be:

<a href="https://www.codecogs.com/eqnedit.php?latex=y(t)=19e^{0.85t}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y(t)=19e^{0.85t}" title="y(t)=19e^{0.85t}" /></a>

This function was initalized with the following driving code:
```c++
       // y'=f(t,y), y(t0)=y0;
    // use the example of y'=0.85y;
    vector<double> t(2);
    t[0]=0; //value of the inital time t0
    t[1]=10; //value of the final time t.f
    double y0=19;
    int n=25; //number of intervals
    vector<double> u(n+1);
    eulerExIV(mesher1D(t,n),y0);

    return 0;
```

The results on the screen were as follows:

```c++
euler
19
25.46
34.1164
45.716
61.2594
82.0876
109.997
147.397
197.511
264.665
354.651
475.233
636.812
853.328
1143.46
1532.24
2053.2
2751.28
3686.72
4940.2
6619.87
8870.63
11886.6
15928.1
21343.7
28600.5

exact
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
For this function, the explicit euler method approximates the first values well, but starts to diverge from the solution.


**Implementation/Code:** The following is the code for eulerExIV()
```c++
  vector<double> eulerExIV(vector<double> time,double y0){

    int n=time.size(); //number of rows
    vector<double> u(n);
    double dt=time[1]-time[0];
    u[0]=y0;
    double f;
    for(int i=0;i<n-1;i++){
        f=functInital(time[i],u[i]);
        u[i+1]=u[i]+dt*f;
    }


    //Compute exact solution to compare
    vector<double> exact(n);
    for(int i=0;i<n;i++){
        exact[i]=19*exp(0.85*time[i]);
    }

     cout<<"euler"<<endl;
     for(int i=0;i<n;i++){
        cout<<u[i]<<endl;
     }
     cout<<endl;

    cout<<"exact"<<endl;
    for(int i=0;i<n;i++){
        cout<<exact[i]<<endl;
     }
     cout<<endl;

    return u;
}
```
