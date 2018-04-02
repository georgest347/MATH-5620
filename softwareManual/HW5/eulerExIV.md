**Function Name:**          eulerExIV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function computes a numerical solution to a IVP using explicit euler method defined below:

<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;1}=u^{n}&plus;\Delta&space;tf(u^{n})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;1}=u^{n}&plus;\Delta&space;tf(u^{n})" title="u^{n+1}=u^{n}+\Delta tf(u^{n})" /></a>

This function calls the following functions:\
functInital <<-- This function holds the f(u,t) function from the given differential equation.

**Input:** This function takes the following inputs:\
time: A vector that contains the time values to evaluate the function at. Can be produced by: [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)\
u0: The inital value of the function
x: A constant contained in the differential equation
B: Another constant contained in the differentail equation
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
  ```

**Output:** This function outputs a vector 'u' that is the numerical solution to the equation specified above.
	
**Usage/Example:**
This program is used to solve the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=P'=\gamma&space;P-\beta&space;P^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P'=\gamma&space;P-\beta&space;P^2" title="P'=\gamma P-\beta P^2" /></a>

With the following values:

<a href="https://www.codecogs.com/eqnedit.php?latex=\gamma&space;=0.1,\beta&space;=0.0001,P_{0}=25" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma&space;=0.1,\beta&space;=0.0001,P_{0}=25" title="\gamma =0.1,\beta =0.0001,P_{0}=25" /></a>

This function was initalized with the following driving code:
```c++
int main()
{
    vector<double> t(2);
    t[0]=0;
    t[1]=10;
    int n=25;
    //For Logistic IVP
    double P0=25;
    double y=0.1;
    double B=0.0001;

   anasol2(P0,y,B,mesher1D(t,n));
   eulerExIV(mesher1D(t,n),P0,y,B);
   

    return 0;
}
```

The following was used for functInital
```c++
double functInitalB(double t, double y, double B, double P) {
	// Function that initalizes the f(t,y) values
	double f;
    f=y*P-B*P*P; //f(P,t) for logistic model of population growth

	return f;
}
```

The results on the screen were as follows:

```c++
Analytic
25
25.9937
27.0259
28.0979
29.2111
30.367
31.5672
32.8132
34.1066
35.4492
36.8426
38.2886
39.789
41.3457
42.9606
44.6356
46.3727
48.1741
50.0417
51.9778
53.9845
56.0641
58.219
60.4513
62.7635
65.158

Explicit Euler
25
25.975
26.987
28.0374
29.1274
30.2586
31.4323
32.6501
33.9134
35.224
36.5833
37.9931
39.4551
40.971
42.5427
44.172
45.8608
47.6111
49.4249
51.3042
53.2511
55.2677
57.3562
59.5189
61.7579
64.0757
```

**Implementation/Code:** The following is the code for eulerExIV()
```c++
vector<double> eulerExIV(vector<double> time,double u0,double x, double B){
     //For 1st order IVP use x=lambda, and set B=0;
     //For Logistic Population growth, use x=y=gamma, and B=beta

    int n=time.size(); //length of the time vector
    vector<double> u(n);
    double dt=time[1]-time[0];
    u[0]=u0;
    double f;

    for(int i=0;i<n-1;i++){
        //u[i+1]=u[i]+dt*functInital(time[i],u[i],x); //uncomment for simple first order equation IVP
        u[i+1]=u[i]+dt*functInitalB(time[i],x,B,u[i]); //uncomment for logistic model of population growth
    }

     cout<<"Explicit Euler"<<endl;
     for(int i=0;i<n;i++){
        cout<<u[i]<<endl;
     }
     cout<<endl;

    return u;
}
```
