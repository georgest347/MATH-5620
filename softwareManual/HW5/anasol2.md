**Function Name:**          anasol2()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function provides the analytic solution to the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=P'=\gamma&space;P-\beta&space;P^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P'=\gamma&space;P-\beta&space;P^2" title="P'=\gamma P-\beta P^2" /></a>

This differential equation has the following inital condition:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(t_{0})=P_0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(t_{0})=P_0" title="P(t_{0})=P_0" /></a>

The exact solution used in this code is of the form:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(t)=\frac{\gamma&space;e^{\gamma&space;t}}{\beta&space;e^{\gamma&space;t}&plus;C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(t)=\frac{\gamma&space;e^{\gamma&space;t}}{\beta&space;e^{\gamma&space;t}&plus;C}" title="P(t)=\frac{\gamma e^{\gamma t}}{\beta e^{\gamma t}+C}" /></a>

Where C is defined as:

<a href="https://www.codecogs.com/eqnedit.php?latex=C=\frac{\gamma-P_{0}\beta}{P_{0}}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?C=\frac{\gamma-P_{0}\beta}{P_{0}}" title="C=\frac{\gamma-P_{0}\beta}{P_{0}}" /></a>

This function calls the following functions:
[multiplySV](https://georgest347.github.io/MATH-5620/softwareManual/HW4/multiplySV) 

**Input:** This function takes the following inputs:\
y: The gamma constant of the function
B: The beta constant of the function
t: a time vector which can be made with [mesher1D](https://georgest347.github.io/MATH-5620/softwareManual/HW4/mesher1D)\
P0: the inital value of the IVP problem.\
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <math.h> //<-- to compute the exp
  ```

**Output:** This function outputs a vector 'P' that is the exact solution to the equation specified above.
	
**Usage/Example:**
This program is used to solve the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=P'=0.1P-0.0001P^2" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P'=0.1P-0.0001P^2" title="P'=0.1P-0.0001P^2" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=P_0=25" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P_0=25" title="P_0=25" /></a>

This function was initalized with the following driving code:
```c++
int main()
{
    vector<double> t(2);
    t[0]=0;
    t[1]=10;
    int n=25;
    double P0=25;
    double y=0.1;
    double B=0.0001;

    anasol2(P0,y,B,mesher1D(t,n));

    return 0;
}
```

The results on the screen were as follows:

```c++
Analytic L.IVP
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
```

**Implementation/Code:** The following is the code for anasol2()
```c++
vector<double> anasol2(double P0,double y,double B,vector<double> t){
    // This function produces an analytic solution for the following IVP
    // P'=y*P-B*P^2 P(t.0)=P.0
    // The analytic solution takes the form:
    // P(t)=(y*exp(y*t))/(B*exp(y*t)+C);
    // where C=(y-P.0*B)/(P.0);

        int m=t.size();
        vector<double> P(m);
        vector<double> a(m);
        double C=(y-P0*B)/P0;
        a=multiplySV(y,t); // quantity y*t
        for(int i=0;i<m;i++){
            a[i]=exp(a[i]); // exp(y*t)
        }
        P=multiplySV(B,a); //B*exp(y*t)
        a=multiplySV(y,a); //y*exp(y*t)

        for(int i=0;i<m;i++){
            P[i]=(a[i])/(P[i]+C);
        }

        cout<<"Analytic L.IVP"<<endl;
        for(int i=0;i<m;i++){
            cout<<P[i]<<endl;
        }
        cout<<endl;

        return P;

}
```
