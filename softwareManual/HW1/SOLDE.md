**Function Name:**           SOLDE()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will compute the solution at time 't' for the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=my''&plus;cy'&plus;ky=f(t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?my''&plus;cy'&plus;ky=f(t)" title="my''+cy'+ky=f(t)" /></a>

This is accomplished by using the analytic solution as shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=y(t)=y_1(t)*(C_1&plus;u_1(t))&plus;y_2(t)*(C_2&plus;u_2(t))" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y(t)=y_1(t)*(C_1&plus;u_1(t))&plus;y_2(t)*(C_2&plus;u_2(t))" title="y(t)=y_1(t)*(C_1+u_1(t))+y_2(t)*(C_2+u_2(t))" /></a>

**Input:** The function takes six inputs: (a,b,c,yo,vo,t) The first three inputs are the constant
coefficients of the differential equation corresponding as follows: ay"+by'+cy. The values yo, and vo
are the inital conditions for the differential equation. They correspond as follows y(0)=yo, and y'(0)=vo.
The final value 't' is the time at which you want to see the response y(t).

**Output:** This function prints the value of y(t) to the screen. If units are used with this function,
correct unit analysis must be preformed to ensure correct answers.

**Usage/Example:**

This function requires the user to find the values of u1 and u2 for the variation of parameters
used in the analytic solution. The assumed solution for the homogeneous equation is: 

      <a href="https://www.codecogs.com/eqnedit.php?latex=y(t)=e^{rt}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?y(t)=e^{rt}" title="y(t)=e^{rt}" /></a>

The functions u1 and u2 are given below:

<a href="https://www.codecogs.com/eqnedit.php?latex=u_1(t)=-\int&space;\frac{y_2(s)f(s)}{W(s)}ds" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u_1(t)=-\int&space;\frac{y_2(s)f(s)}{W(s)}ds" title="u_1(t)=-\int \frac{y_2(s)f(s)}{W(s)}ds" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=u_2(t)=\int&space;\frac{y_1(s)f(s)}{W(s)}ds" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u_2(t)=\int&space;\frac{y_1(s)f(s)}{W(s)}ds" title="u_2(t)=\int \frac{y_1(s)f(s)}{W(s)}ds" /></a>

The function W(s) is the Wronskian and the function f(s) is the forcing function.

<a href="https://www.codecogs.com/eqnedit.php?latex=W(s)=&space;\begin{vmatrix}&space;y_1(s)&space;&&space;y_2(s)\\&space;y_1'(s)&&space;y_2'(s)&space;\end{vmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?W(s)=&space;\begin{vmatrix}&space;y_1(s)&space;&&space;y_2(s)\\&space;y_1'(s)&&space;y_2'(s)&space;\end{vmatrix}" title="W(s)= \begin{vmatrix} y_1(s) & y_2(s)\\ y_1'(s)& y_2'(s) \end{vmatrix}" /></a>


**Implementation/Code:** The following is the code for SOLDE()

      double SOLDE(double a,double b, double c,double yo, double vo, double t) {
      	/* SOLDE (Second Order Linear Differential Equation)
      	This function takes the constant coefficents of a 2nd
      	order LDE and solves using the analyitic solution
	      for the response y(t) at a given value of 't'.

	      Using varation of parameters to find the particular
	      solution, this function requires the user to know 
	      the forcing function, and the assumed solution to find
	      the homogeneous solution. The assumed solution for 
	      the yc(t)= exp(rt).

	      The full analytic solution is shown below:
	      y(t)=yc(t)+yp(t);

	      Where:
	      yc(t)=C1*y1(t)+C2*y2(t);
	      yp(t)=u1(t)*y1(t)+u2(t)*y2(t);

	      Where u1 and u2 are the integrals shown below:
	      u1(t)=-int((y2(s)*f(s))/(W(s)));
	      u1(t)=int((y1(s)*f(s))/(W(s)));

	      The function f(s) is the forcing function

	      Where W(s) is the Wronskian:
	      W(s)=y2'(s)*y1(s)-y1'(s)*y2(s);

	      The inital conditions are taken to be:
	      y(0)=yo, and y'(0)=vo;
	      Inital time value is 0. If inital time
	      changes, code needs to be updated!
	      */

	
	      //Set up Varibles
	      double r1, r2, i1, i2, C1, C2, Ytime,u1,u2,u1t,u2t,yp,dyp;
	      int tnot = 0;

	
	      //Calculate the discriminent
	      double d = (b*b) - (4 * a*c);
	      //Finds the roots of the quadradic equation
	      if (d>0)
	      {
      		//Two real and distinct roots
	      	r1 = (-b + sqrt(d)) / (2 * a);
		      r2 = (-b - sqrt(d)) / (2 * a);
	      }
	      else if (d == 0)
	      {
      		//Two real and equal roots
      		r1 = -b / (2 * a);
	      	r2 = -b / (2 * a);
	      }
	      else {
		      //Roots are complex and imaginary
		      r1 = -b / (2 * a);
		      i1 = sqrt(-d) / (2 * a);
		      r2 = r1;
		      i2 = (-1)*i1;
		      cout << "roots are imaginary" << endl;
	      }

	      /*Use this section for the particular solution.
	      Particular solution has the form of:
	      yp(t)=u1(t)*y1(t)+u2(t)*y2(t);

	      Where u1 and u2 are the integrals shown below:
      	u1(t)=-int((y2(s)*f(s))/(W(s)));
	      u1(t)=int((y1(s)*f(s))/(W(s)));
      	Calculate these integrals and place them below.
	      */

	      //Evaluate these at initial time t=0, use tnot;
	      u1 = tnot;
	      u2 = tnot;
	
	      //For the final response, evaluate the functions
	      //u1 and u2 at time=t; replace tnot with t;
	      u1t = tnot;
	      u2t = tnot;

	      // This is the particular solution evaluated at the
	      // inital condition values. t=tnot;
	      yp = u1 * exp(r1*tnot) + u2 * exp(r2*tnot);
	      dyp=r1* u1 * exp(r1*tnot) + r2*u2 * exp(r2*tnot);

	      //Finds the condstant values C1 and C2 for the
	      // homogeneous solution. 
      	//yc(t)=C1*y1+C2*y2
	
	      //
	      C1 = (1 / (r2 - r1))*(r2*(yo - yp) - (vo - dyp));
	      C2 = (1 / (r2 - r1))*((-1)*r2*(yo - yp) + (vo - dyp));

	      // Finds the response at time t=t;
	      Ytime = C1 * exp(r1*t)+ C2 * exp(r2*t)+ u1t * exp(r1*t)+ u2t * exp(r1*t);

	      return Ytime;
       }
