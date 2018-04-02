**Function Name:**          PC3O()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function computes a numerical solution to a IVP using a third order predictor corrector method defined below:

A 4step Adams-Bashforth method:\
<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;-9f(u^n)&plus;37f(u^{n&plus;1})-59f(u^{n&plus;2})&plus;55f(u^{n&plus;3})&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;-9f(u^n)&plus;37f(u^{n&plus;1})-59f(u^{n&plus;2})&plus;55f(u^{n&plus;3})&space;\right&space;)" title="u^{n+4}=u^{n+3}+\frac{\Delta t}{24}\left ( -9f(u^n)+37f(u^{n+1})-59f(u^{n+2})+55f(u^{n+3}) \right )" /></a>\
A 3step Adams-Moulton Method
<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;f(u^n&plus;1)-5f(u^{n&plus;2})&plus;19f(u^{n&plus;3})&plus;9f(u^{n&plus;4})&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;f(u^n&plus;1)-5f(u^{n&plus;2})&plus;19f(u^{n&plus;3})&plus;9f(u^{n&plus;4})&space;\right&space;)" title="u^{n+4}=u^{n+3}+\frac{\Delta t}{24}\left ( f(u^n+1)-5f(u^{n+2})+19f(u^{n+3})+9f(u^{n+4}) \right )" /></a>

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
   PC3O(mesher1D(t,n),P0,y,B);
   
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

PC3O
25
25.9906
27.0194
28.0877
29.2005
30.356
31.5558
32.8014
34.0944
35.4365
36.8294
38.2749
39.7748
41.331
42.9453
44.6197
46.3563
48.157
50.024
51.9595
53.9655
56.0445
58.1986
60.4302
62.7416
65.1354
```

**Implementation/Code:** The following is the code for PC3O()
```c++
vector<double> PC3O(vector<double> time,double u0,double x,double B){
    // This is a third order predictor corrector method. With a 4th order adams bashforth
    // method to predict, and a 3rd order corrector method.
    int n=time.size(); //length of the time vector
    vector<double> u(n);
    vector<double> f(n);
    vector<double> am(n);
    double dt=time[1]-time[0];
    u[0]=u0;

    //Use the RK4 method to start
    vector<double> rkt(4);
    for(int i=0;i<4;i++){
        rkt[i]=time[i];
    }
     rkt=RK4(rkt,u0,x,B);

    for(int i=0;i<4;i++){
        u[i]=rkt[i];
        am[i]=rkt[i];
    }


    for(int i=4;i<n;i++){

             //4 step Adams-Bashforth Method
            //u[i]=u[i-1]+(dt/24)*(-9*functInital(time[i-4] ,u[i-4], x)+37*functInital(time[i-3],u[i-3],x)-59*functInital(time[i-2],u[i-2],x)+55*functInital(time[i-1],u[i-1],x)); //Use for 1O IVP
            u[i]=u[i-1]+(dt/24)*(-9*functInitalB(time[i-4] ,x,B,u[i-4])+37*functInitalB(time[i-3],x,B,u[i-3])-59*functInitalB(time[i-2],x,B,u[i-2])+55*functInitalB(time[i-1],x,B,u[i-1])); //Use for LPM IVP

            //3 step Adams-Moulton Method
            //u[i]=u[i-1]+(dt/24)*(functInital(time[i-3] ,u[i-3], x)-5*functInital(time[i-2],u[i-2],x)+19*functInital(time[i-1],u[i-1],x)+9*functInital(time[i],u[i],x)); //Use for 1O IVP
            u[i]=u[i-1]+(dt/24)*(functInitalB(time[i-3] ,x,B,u[i-3])-5*functInitalB(time[i-2],x,B,u[i-2])+19*functInitalB(time[i-1],x,B,u[i-1])+9*functInitalB(time[i],x,B,u[i])); //Use for LPM IVP

    }

    cout<<"PC3O"<<endl;
     for(int i=0;i<n;i++){
        cout<<u[i]<<endl;
     }
     cout<<endl;

    return u;
}
```
