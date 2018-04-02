**Function Name:**          eulerIMIV()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function computes a numerical solution to a IVP using implicitcod euler method defined below:

<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;1}=u^{n}&plus;\Delta&space;tf(u^{n&plus;1},t_{n&plus;1})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;1}=u^{n}&plus;\Delta&space;tf(u^{n&plus;1},t_{n&plus;1})" title="u^{n+1}=u^{n}+\Delta tf(u^{n+1},t_{n+1})" /></a>

This function calls the following functions:\
[absoluteErrorNormal](https://georgest347.github.io/MATH-5620/softwareManual/HW2/absoluteErrorNormal)

**Input:** This function takes the following inputs:\
time: A vector that contains the time values to evaluate the function at. Can be produced by: [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)\
u0: The inital value of the function\
x: A constant contained in the differential equation\
B: Another constant contained in the differentail equation\
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      also any math headers for math functions included with the differential equation
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
    double P0=25;
    double y=0.1;
    double B=0.0001;

    ///Problem B
   anasol2(P0,y,B,mesher1D(t,n));
   eulerIMIV(mesher1D(t,n),P0,y,B);
   
    return 0;
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

Implicit Euler
25
26.0135
27.0669
28.1617
29.2994
30.4816
31.7098
32.9858
34.3112
35.6878
37.1175
38.6021
40.1435
41.7436
43.4045
45.1283
46.9171
48.773
50.6983
52.6952
54.766
56.9131
59.139
61.446
63.8367
66.3136
```

**Implementation/Code:** The following is the code for eulerIMIV()
```c++
vector<double> eulerIMIV(vector<double> time,double u0,double x, double B){
     //For 1st order IVP use x=lambda, and set B=0;
     //For Logistic Population growth, use x=y=gamma, and B=beta

    int n=time.size(); //length of the time vector
    vector<double> u(n);
    double dt=time[1]-time[0];
    u[0]=u0;

    //Initial values for loop
    int maxiter=1000;
    double uold=u0;
    double fun,dfun;
    //Main loop use 1 because loop is set up for i-1
    for (int i=1;i<n;i++){
        //Reset the newton method
        double tol=0.0001;
        double nerror=1000000000000;
        int iter=0;
        double uold=u[i]-1;
        //Solve the x1 value or u_n+1 using newton method
        while(nerror>tol&&iter<maxiter){
            //fun=u[i-1]-u[i-1]+dt*x*u[i-1];  //Use for 1st order IVP
            //dfun=dt*x-1;  //Use for 1st order IVP
            fun=u[i-1]-u[i-1]+dt*(x*u[i-1]-B*u[i-1]*u[i-1]);  //Use for Logistic Population Growth
            dfun=dt*(x-2*B*u[i-1])-1;  //Use for Logistic Population Growth

            u[i]=u[i-1]-(fun)/(dfun);
            nerror=absoluteErrorNormal(u[i],uold);
            uold=u[i];
            iter++;
        }
    }


     cout<<"Implicit Euler"<<endl;
     for(int i=0;i<n;i++){
        cout<<u[i]<<endl;
     }
     cout<<endl;

    return u;
}
```
