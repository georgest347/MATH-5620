**Function Name:**          RK2()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function computes a numerical solution to a IVP using Runge Kutta order 2 method defined below:

<a href="https://www.codecogs.com/eqnedit.php?latex=u^{*}=u^{n}&plus;0.5\Delta&space;tf(u^{n})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{*}=u^{n}&plus;0.5\Delta&space;tf(u^{n})" title="u^{*}=u^{n}+0.5\Delta tf(u^{n})" /></a>
<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;1}=u^{n}&plus;\Delta&space;tf(u^{*})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;1}=u^{n}&plus;\Delta&space;tf(u^{*})" title="u^{n+1}=u^{n}+\Delta tf(u^{*})" /></a>

This function calls the following functions:\
functInital <<-- This function holds the f(u,t) function from the given differential equation.

**Input:** This function takes the following inputs:\
time: A vector that contains the time values to evaluate the function at. Can be produced by: [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)\
u0: The inital value of the function\
x: A constant contained in the differential equation\
B: Another constant contained in the differentail equation\
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      Any headers needed for math included in the differential equation
  ```

**Output:** This function outputs a vector 'u' that is the numerical solution to the equation specified above.
	
**Usage/Example:**
This program is used to solve the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=P'=\gamma&space;P-\beta&space;P^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P'=\gamma&space;P-\beta&space;P^2" title="P'=\gamma P-\beta P^2" /></a>

With the following values:

<a href="https://www.codecogs.com/eqnedit.php?latex=\gamma&space;=0.1,\beta&space;=0.0001,P_{0}=25" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\gamma&space;=0.1,\beta&space;=0.0001,P_{0}=25" title="\gamma =0.1,\beta =0.0001,P_{0}=25" /></a>

This function was initalized with the following driving code:
```c++
int main(){
    vector<double> t(2);
    t[0]=0;
    t[1]=10;
    int n=25;
    //For Logistic IVP
    double P0=40000;
    double y=0.1;
    double B=0.0001;

   ///Problem B
   anasol2(P0,y,B,mesher1D(t,n));
   RK2(mesher1D(t,n),P0,y,B);
   
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

RK2
25
25.9935
27.0254
28.0971
29.21
30.3656
31.5655
32.8112
34.1042
35.4464
36.8394
38.285
39.7849
41.3411
42.9555
44.6299
46.3665
48.1672
50.0342
51.9696
53.9756
56.0545
58.2086
60.4401
62.7515
65.1451
```

**Implementation/Code:** The following is the code for RK2()
```c++
vector<double> RK2(vector<double> time,double u0,double x, double B){
     //For 1st order IVP use x=lambda, and set B=0;
     //For Logistic Population growth, use x=y=gamma, and B=beta

    int n=time.size(); //length of the time vector
    vector<double> u(n);
    double dt=time[1]-time[0];
    u[0]=u0;

    /*
    //Use for 1st order IVP
    double ustar;
    for(int i=0;i<n-1;i++){
        ustar=u[i]+0.5*dt*functInital(time[i],x,u[i]);
        u[i+1]=u[i]+dt*functInital(time[i],x,ustar);
    }*/


    //Use for Population Growth IVP
    double ustar;
    for(int i=0;i<n-1;i++){
        ustar=u[i]+0.5*dt*functInitalB(time[i],x,B,u[i]);
        u[i+1]=u[i]+dt*functInitalB(time[i],x,B,ustar);
    }


     cout<<"RK2"<<endl;
     for(int i=0;i<n;i++){
        cout<<u[i]<<endl;
     }
     cout<<endl;

    return u;
}
```
