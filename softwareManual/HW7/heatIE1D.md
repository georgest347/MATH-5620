**Function Name:**          heatIE1D()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves the 1D heat conduction problem given in the form shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" title="\frac{\delta u}{\delta t}=k\frac{\delta^2 u}{\delta x^2}" /></a>

The Implicit Euler FD method takes the following form:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{U_{j}^{n&plus;1}-U_{j}^{n}}{\Delta&space;t}=\frac{k}{\Delta&space;x^2}\left&space;(&space;U_{j&plus;1}^{n&plus;1}&space;-2U_{j}^{n&plus;1}&plus;U_{j&plus;1}^{n&plus;1}\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{U_{j}^{n&plus;1}-U_{j}^{n}}{\Delta&space;t}=\frac{k}{\Delta&space;x^2}\left&space;(&space;U_{j&plus;1}^{n&plus;1}&space;-2U_{j}^{n&plus;1}&plus;U_{j&plus;1}^{n&plus;1}\right&space;)" title="\frac{U_{j}^{n+1}-U_{j}^{n}}{\Delta t}=\frac{k}{\Delta x^2}\left ( U_{j+1}^{n+1} -2U_{j}^{n+1}+U_{j+1}^{n+1}\right )" /></a>

This equation is used in the creation of a Ay=b linear algebra problem to solve the differential equation. The [aLUb](https://georgest347.github.io/MATH-5620/softwareManual/HW3/aLUb) solver is imbedded in this function, but can be changed to any solver that accepts the matrix of form:

<a href="https://www.codecogs.com/eqnedit.php?latex=\begin{bmatrix}&space;a&space;&&space;a&&space;a&&space;|&space;b\\&space;a&&space;a&&space;a&&space;|&space;b\\&space;a&&space;a&space;&&space;a&&space;|&space;b&space;\end{bmatrix}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\begin{bmatrix}&space;a&space;&&space;a&&space;a&&space;|&space;b\\&space;a&&space;a&&space;a&&space;|&space;b\\&space;a&&space;a&space;&&space;a&&space;|&space;b&space;\end{bmatrix}" title="\begin{bmatrix} a & a& a& | b\\ a& a& a& | b\\ a& a & a& | b \end{bmatrix}" /></a>

This function calls the following functions:\
[g1](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g1) <<-- This function holds the function corresponding to the boundry condition at x=0\
[g2](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g2) <<-- This function holds the function corresponding to the boundry condition at x=L\
[mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D) <<-- This function creates a 2D mesh for the FD problem. one axis is space and the other is time.\
[aLUb](https://georgest347.github.io/MATH-5620/softwareManual/HW3/aLUb) <<-- This function solves the Ay=b equation.\

**Input:** This function takes the following inputs:\
mesh: A matrix that contains the 2D mesh. Can be produced by: [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)\
u0: The inital value of the function\
k: Thermal conductivity of the material (Assumed to be Constant)
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <iomanip> //<--to show the data
      #include <iostream> //<-- used for file out put. (Graphing in excel)
      #include <fstream> //<-- used for file output. (Graphing in excel)
  ```

**Output:** This function outputs a matrix 'u' that is the numerical solution to the equation specified above. The first index number corresponds to time, and the second index number corresponds to space.
	
**Usage/Example:**
This program was used to solve the temperature distribution on a rod with fixed temperatures at the ends. The following values were used:

```c++
  x(t,0)=20;
  x(t,L)=100;
  x(0,x)=25;
  L=10;
  time final=2;
```

This function was initalized with the following driving code:
```c++
int main()
{
    vector<double> t(2);
    vector<double> x(2);
    t[0]=0;
    t[1]=2;
    x[0]=0;
    x[1]=10;
    double dt=0.001;
    double dx=1.0;
    double u0=25;
    double k=10;

    heatIE1D(mesher2D(dx,dt,x,t),u0,k);

}
```

The first and last lines printed are shown below:

```c++
Starting:  20        25        25        25        25        25        25        25        25        25       100
Ending:    20   26.0771   32.3404   38.9587   46.0673   53.7545   62.0531   70.9359   80.3176    90.063       100 
```

**Implementation/Code:** The following is the code for heatIE1D()
```c++
vector<vector<double> > heatIE1D(vector<vector<double> > mesh,double u0,double k){
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
    double am=xlength-1;
    double an=xlength-2;

    vector<double> v(xlength);
    vector<vector<double> > u(tlength,v);
    vector<double> a(am);
    vector<vector<double> > A(an,a);

    double C=((k*dt)/dx*dx);
    double D=1+2*C;

    //Initial value assignment
    //Change to vector if different initial temperatures along x direction
    for (int i=0;i<xlength;i++){
        u[0][i]=u0;
    }
    //Update boundries
    u[0][0]=g1(0);
    u[0][xlength-1]=g2(0);

    ///Time loop
    //tlength-1 b/c solving for p+1
    for (int p=0;p<tlength-1;p++){
        //set up A matrix for solver
        for(int i=0;i<an;i++){
            for(int j=0;j<am;j++){
                if (i==j){
                    A[i][j]=D;
                }
                if (i==j+1|| i==j-1){
                    A[i][j]=-1*C;
                }
            }
        }
        //For b vector
        for(int i=1;i<am;i++){
            A[i-1][am-1]=u[p][i];
        }
        //Update boundries
        u[p+1][0]=g1(p);
        u[p+1][xlength-1]=g2(p);
        //Set up b.c in matrix
        A[0][am-1]=A[0][am-1]+C*u[p+1][0];
        A[an-1][am-1]=A[an-1][am-1]+C*u[p+1][xlength-1];

        /*
        cout<<"A MATRIX"<<endl;
        for(int i=0;i<an;i++){
            for(int j=0;j<am;j++){
                cout<<setw(10)<<A[i][j];
            }
            cout<<endl;
        }*/

        a=aLUb(A);

        for(int j=0;j<an;j++){
            u[p+1][j+1]=a[j];
        }
    }

    ofstream myfile;
    myfile.open ("ImplicitEuler.txt");
    cout<<"Implicit Euler"<<endl;
    for(int i=0;i<tlength;i++){
        for(int j=0;j<xlength;j++){
            cout<<setw(10)<<u[i][j];
            myfile <<setw(10)<<u[i][j];
        }
        cout<<endl;
        myfile<<endl;
	}
	myfile.close();

    return u;
}
```
