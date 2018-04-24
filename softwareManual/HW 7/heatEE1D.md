**Function Name:**          heatEE1D()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves the 1D heat conduction problem given in the form shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" title="\frac{\delta u}{\delta t}=k\frac{\delta^2 u}{\delta x^2}" /></a>

The Explicit Euler FD method takes the following form:

<a href="https://www.codecogs.com/eqnedit.php?latex=U_{j}^{n&plus;1}=U_{j}^{n}&plus;\frac{k\Delta&space;t}{\Delta&space;x^2}(U_{j&plus;1}^{n}-2U_{j}^{n}&plus;U_{j-1}^{n})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?U_{j}^{n&plus;1}=U_{j}^{n}&plus;\frac{k\Delta&space;t}{\Delta&space;x^2}(U_{j&plus;1}^{n}-2U_{j}^{n}&plus;U_{j-1}^{n})" title="U_{j}^{n+1}=U_{j}^{n}+\frac{k\Delta t}{\Delta x^2}(U_{j+1}^{n}-2U_{j}^{n}+U_{j-1}^{n})" /></a>

This function calls the following functions:\
g1 <<-- This function holds the function corresponding to the boundry condition at x=0\
g2 <<-- This function holds the function corresponding to the boundry condition at x=L\
mesher2D <<-- This function creates a 2D mesh for the FD problem. one axis is space and the other is time.\

**Input:** This function takes the following inputs:\
mesh: A matrix that contains the 2D mesh. Can be produced by: [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)\
u0: The inital value of the function\
k: Thermal conductivity of the material (Assumed to be Constant)
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <iomanip> //<--to show the data
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
    double dt=0.01;
    double dx=1.0;
    double u0=25;
    double k=10;

    heatEE1D(mesher2D(dx,dt,x,t),u0,k);

}
```

The first and last lines printed are shown below:

```c++
Starting:  20        25        25        25        25        25        25        25        25        25       100
Ending:    20   26.0964   32.3774   39.0103   46.1288   53.8204   62.1168   70.9909    80.358   90.0844       100
```

**Implementation/Code:** The following is the code for heatEE1D()
```c++
vector<vector<double> > heatEE1D(vector<vector<double> > mesh,double u0,double k){
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

    //cout<<xlength<<"   "<<tlength<<endl;h

    vector<double> a(xlength);
    vector<vector<double> > u(tlength,a);

    double C=((k*dt)/dx*dx);

    ///CHECK stability
    if(C>=0.5){
        cout<<"CHECK STABILITY (dt and dx values)"<<endl;
        return u;
    }

    //Initial value assignment
    //Change to vector if different initial temperatures along x direction
    for (int i=0;i<xlength;i++){
        u[0][i]=u0;
    }
    //Sets the boundaries for initial conditions
    u[0][0]=g1(mesh[1][0]);
    u[0][xlength-1]=g2(mesh[1][0]);

    for(int i=0;i<xlength;i++){
        cout<<u[0][i]<<endl;
    }

    //Solver
    for(int i=0;i<tlength-1;i++){
        for(int j=1;j<xlength-1;j++){
            u[i+1][j]=u[i][j]+C*(u[i][j+1]-2*u[i][j]+u[i][j-1]);
        }
        //Update boundries
        u[i+1][0]=g1(i);
        u[i+1][xlength-1]=g2(i);
    }


    ofstream myfile;
    myfile.open ("ExplicitEuler.dat");
    cout<<"Explicit Euler"<<endl;
    for(int i=0;i<tlength;i++){
        for(int j=0;j<xlength;j++){
            cout<<setw(10)<<u[i][j];
            myfile <<u[i][j]<<" ";
        }
        cout<<endl;
        myfile<<endl;
	}
	myfile.close();





    return u;
}
```
