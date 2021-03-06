**Function Name:**          hyperLWM()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function uses Lax-Wendroff method to solve advection problems of the form:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;u}{\partial&space;t}&plus;a\frac{\partial&space;u}{\partial&space;x}=0" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;u}{\partial&space;t}&plus;a\frac{\partial&space;u}{\partial&space;x}=0" title="\frac{\partial u}{\partial t}+a\frac{\partial u}{\partial x}=0" /></a>

These problems have inital values of the form:

<a href="https://www.codecogs.com/eqnedit.php?latex=u(x,0)=\eta&space;(x)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(x,0)=\eta&space;(x)" title="u(x,0)=\eta (x)" /></a>

Where the left side of the equation is a function of x. The advection problems are useful for simulating wave propigation.

The exact solution of the Advection problem is:

<a href="https://www.codecogs.com/eqnedit.php?latex=u(x,t)=\eta&space;(x-at)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u(x,t)=\eta&space;(x-at)" title="u(x,t)=\eta (x-at)" /></a>

This function calls the following functions:\
[step](https://georgest347.github.io/MATH-5620/softwareManual/HW8/step) <<-- This function holds the function to solve the boundry conditions
[mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D) <<-- This function creates a 2D mesh for the FD problem. one axis is space and the other is time.\
[initalCon](https://georgest347.github.io/MATH-5620/softwareManual/HW8/initalCon) <<-- This function is used to create the inital conditions.\

**Input:** This function takes the following inputs:\
mesh=A 2D mesh genterate in space and time.\
u0= a vector containing the inital values.\
c=the constant a in the first equation.\

The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <iomanip> //<--to show the data
      #include <iostream> //<-- used for file out put. (Graphing)
      #include <fstream> //<-- used for file output. (Graphing)
  ```
  
**Output:** This function outputs a matrix u that contains the solution to the PDE at x and t coordinates. This matrix can be printed to the screen, or output to a file for future use.
	
**Usage/Example:**
Using the following inputs:
```c++
  c=2;
  t(0,2);
  x(0,5);
  dt=0.001;
  dx=0.1;
```
The Lax-Wendroff method added numerical dispersion to the solution.
(See HW8.docx for graph)

**Implementation/Code:** The following is the code for hyperLWM()
```c++
vector<vector<double> > hyperLWM(vector<vector<double> > mesh, vector<double> u0, double c){
    //Read mesh
	int large=mesh[0].size();
	int xlength=0;
	int tlength=0;
	for(int i=1;i<large;i++){
            if(mesh[0][i]>mesh[0][i-1]){
                xlength++;
            }
            if(mesh[1][i]>mesh[1][i-1]){
                tlength++;
            }
	}
	xlength++;
	tlength++;
	double dx=mesh[0][1]-mesh[0][0];
	double dt=mesh[1][1]-mesh[1][0];

    //cout<<xlength<<"   "<<tlength<<endl;

    vector<double> a(xlength);
    vector<vector<double> > u(tlength,a);

    double C=(c*dt)/(2*dx);
    double C2=(c*c*dt*dt)/(2*dx*dx);

    //Initial value assignment
    //Change to vector if different initial values along x direction
    for (int i=0;i<xlength;i++){
        u[0][i]=u0[i];
    }

    //Solver
    for(int i=0;i<tlength-1;i++){
        for(int j=1;j<xlength-1;j++){
                //10.18 pp209 FD by LeVeque
            u[i+1][j]=u[i][j]-C*(u[i][j+1]-u[i][j-1])+C2*(u[i][j+1]-2*u[i][j]+u[i][j-1]);
        }
        //Boundry conditions
        u[i+1][0]=step(0,mesh[0][xlength/2]);
        u[i+1][xlength-1]=step(mesh[0][xlength-1],mesh[0][xlength/2]);
    }

    ofstream myfile;
    myfile.open ("Lax-Wendroff.txt", ios::out | ios::trunc);
    cout<<"Lax-Wendroff"<<endl;
    for(int i=0;i<tlength;i++){
        for(int j=0;j<xlength;j++){
            //cout<<setw(15)<<u[i][j];
            myfile <<setw(15)<<u[i][j];
        }
        //cout<<endl;
        myfile<<endl;
	}
	myfile.close();

    return u;
}
```
