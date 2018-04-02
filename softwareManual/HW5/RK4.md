**Function Name:**          RK4()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function computes a numerical solution to a IVP using Runge Kutta order 4 method defined below:

<a href="https://www.codecogs.com/eqnedit.php?latex=Y_{1}=U^{n}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_{1}=U^{n}" title="Y_{1}=U^{n}" /></a>\
<a href="https://www.codecogs.com/eqnedit.php?latex=Y_{2}=U^{n}&plus;0.5\Delta&space;tf(Y_{1},t_{n})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_{2}=U^{n}&plus;0.5\Delta&space;tf(Y_{1},t_{n})" title="Y_{2}=U^{n}+0.5\Delta tf(Y_{1},t_{n})" /></a>\
<a href="https://www.codecogs.com/eqnedit.php?latex=Y_{3}=U^{n}&plus;0.5\Delta&space;tf(Y_{2},t_{n}&plus;\frac{\Delta&space;t}{2})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_{3}=U^{n}&plus;0.5\Delta&space;tf(Y_{2},t_{n}&plus;\frac{\Delta&space;t}{2})" title="Y_{3}=U^{n}+0.5\Delta tf(Y_{2},t_{n}+\frac{\Delta t}{2})" /></a>\
<a href="https://www.codecogs.com/eqnedit.php?latex=Y_{4}=U^{n}&plus;\Delta&space;tf(Y_{3},t_{n}&plus;\frac{\Delta&space;t}{2})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?Y_{4}=U^{n}&plus;\Delta&space;tf(Y_{3},t_{n}&plus;\frac{\Delta&space;t}{2})" title="Y_{4}=U^{n}+\Delta tf(Y_{3},t_{n}+\frac{\Delta t}{2})" /></a>\
<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;1}=u^{n}&plus;\frac{\Delta&space;t}{6}\left&space;[&space;f(Y_{1},t_n)&plus;2f(Y_2,t_n&plus;\frac{\Delta&space;t}{2})&plus;2f(Y_3,t_n&plus;\frac{\Delta&space;t}{2})&plus;f(Y_4,t_n&plus;\Delta&space;t)&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;1}=u^{n}&plus;\frac{\Delta&space;t}{6}\left&space;[&space;f(Y_{1},t_n)&plus;2f(Y_2,t_n&plus;\frac{\Delta&space;t}{2})&plus;2f(Y_3,t_n&plus;\frac{\Delta&space;t}{2})&plus;f(Y_4,t_n&plus;\Delta&space;t)&space;\right&space;]" title="u^{n+1}=u^{n}+\frac{\Delta t}{6}\left [ f(Y_{1},t_n)+2f(Y_2,t_n+\frac{\Delta t}{2})+2f(Y_3,t_n+\frac{\Delta t}{2})+f(Y_4,t_n+\Delta t) \right ]" /></a>

This function calls the following functions:\
functInital <<-- This function holds the f(u,t) function from the given differential equation.

**Input:** This function takes the following inputs:\
time: A vector that contains the time values to evaluate the function at. Can be produced by: [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)\
u0: The inital value of the function\
x: A constant contained in the differential equation\
B: Another constant contained in the differential equation
  
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
   RK4(mesher1D(t,n),P0,y,B);
   
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

RK4
25
25.9906
27.0194
28.0877
29.197
30.3488
31.5445
32.7858
34.0742
35.4114
36.7991
38.239
39.7329
41.2827
42.8903
44.5576
46.2866
48.0794
49.9379
51.8645
53.8611
55.9301
58.0737
60.2943
62.5942
64.9758
```

**Implementation/Code:** The following is the code for RK4()
```c++
vector<double> RK4(vector<double> time,double u0,double x, double B){
     //For 1st order IVP use x=lambda, and set B=0;
     //For Logistic Population growth, use x=y=gamma, and B=beta

    int n=time.size(); //length of the time vector
    vector<double> u(n);
    double dt=time[1]-time[0];
    u[0]=u0;

    /*
    //Use for 1st order IVP
    double Y1,Y2,Y3,Y4;
    for(int i=0;i<n-1;i++){
            Y1=u[i];
            Y2=u[i]+0.5*dt*functInital((time[i]+dt*0.5),x,Y1);
            Y3=u[i]+0.5*dt*functInital((time[i]+dt*0.5),x,Y2);
            Y4=u[i]+0.5*dt*functInital((time[i]+dt*0.5),x,Y3);

            u[i+1]=u[i]+(dt/6)*(functInital(time[i],x,Y1)+2*functInital((time[i]+dt*0.5),x,Y2)+2*functInital((time[i]+dt*0.5),x,Y3)+functInital(time[i],x,Y4));
    }*/


    //Use for Logistic Population IVP
    double Y1,Y2,Y3,Y4;
    for (int i=0;i<n-1;i++){
            Y1=u[i];
            Y2=u[i]+0.5*dt*functInitalB((time[i]+dt*0.5),x,B,Y1);
            Y3=u[i]+0.5*dt*functInitalB((time[i]+dt*0.5),x,B,Y2);
            Y4=u[i]+0.5*dt*functInitalB((time[i]+dt*0.5),x,B,Y3);

            u[i+1]=u[i]+(dt/6)*(functInitalB(time[i],x,B,Y1)+2*functInitalB((time[i]+dt*0.5),x,B,Y2)+2*functInitalB((time[i]+dt*0.5),x,B,Y3)+functInitalB(time[i],x,B,Y4));
    }


     cout<<"RK4"<<endl;
     for(int i=0;i<n;i++){
        cout<<u[i]<<endl;
     }
     cout<<endl;

    return u;
}
```
