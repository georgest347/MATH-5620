**Function Name:**           logisticDE()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** The purpose of this function is to find the value of the analytic solution to the following differential
equation:

    dP/dt=a*P-B*P^2
    
With the analytic solution taken to be:

<a href="https://www.codecogs.com/eqnedit.php?latex=P(t)=\frac{\alpha&space;e^{\alpha&space;t}}{\beta&space;e^{\alpha&space;t}&plus;C}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?P(t)=\frac{\alpha&space;e^{\alpha&space;t}}{\beta&space;e^{\alpha&space;t}&plus;C}" title="P(t)=\frac{\alpha e^{\alpha t}}{\beta e^{\alpha t}+C}" /></a>

The value for C is shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=C=\frac{\alpha-P_o&space;\beta&space;}{P_o}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?C=\frac{\alpha-P_o&space;\beta&space;}{P_o}" title="C=\frac{\alpha-P_o \beta }{P_o}" /></a>
    
Where Pnot was given to be the inital condition P(0)=Pnot.

**Input:** The values are input into the function as follows: Pnot,a,B,and t. The value 't' is the time point of interest.

**Output:** This function returns the value of the analytic solution P(t). 

**Usage/Example:**
This function needs to include:

      #include "math.h"
      #include <iostream>

The function can be used as follows:

      cout<<logisticDE(1,3,2,5)<<endl;
      
Output from the lines above:

      1.5

The returned value can also be stored for later use:

     double Ptime=logisticDE(1,3,2,5);

**Implementation/Code:** The following is the code for logisticDE()

    /*
    This function given alpha beta and P_0 will
    return the value P(t)
    */
    double logisticDE(double Pnot,double alpha,double beta,double t){
        double C=(alpha-Pnot*beta)/Pnot;
        double ptime=(alpha*exp(alpha*t))/(beta*exp(alpha*t)+C);
        return ptime;
    }
