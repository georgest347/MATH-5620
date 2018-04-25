**Function Name:**          heatRK4()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves the 1D heat conduction problem given in the form shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" title="\frac{\delta u}{\delta t}=k\frac{\delta^2 u}{\delta x^2}" /></a>

The RK4 FD method takes the following form:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;u}{\partial&space;t}=\frac{k}{\Delta&space;x^2}(U_{j&plus;1}^{n}-2*U_{j}^{n}&plus;U_{j-1}^{n})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;u}{\partial&space;t}=\frac{k}{\Delta&space;x^2}(U_{j&plus;1}^{n}-2*U_{j}^{n}&plus;U_{j-1}^{n})" title="\frac{\partial u}{\partial t}=\frac{k}{\Delta x^2}(U_{j+1}^{n}-2*U_{j}^{n}+U_{j-1}^{n})" /></a>

This utilizes the method of lines to turn the PDE into a system of nonlinear ODE of the form:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\partial&space;u}{\partial&space;t}=F(u,t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\partial&space;u}{\partial&space;t}=F(u,t)" title="\frac{\partial u}{\partial t}=F(u,t)" /></a>

This function calls the following functions:\
[g1](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g1) <<-- This function holds the function corresponding to the boundry condition at x=0\
[g2](https://georgest347.github.io/MATH-5620/softwareManual/HW7/g2) <<-- This function holds the function corresponding to the boundry condition at x=L\
[mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D) <<-- This function creates a 2D mesh for the FD problem. one axis is space and the other is time.\
[functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW7/functInital) <<-- This is the F(u,t) function described above.\

**Input:** This function takes the following inputs:\
mesh: A matrix that contains the 2D mesh. Can be produced by: [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)\
u0: The inital value of the function\
k: Thermal conductivity of the material (Assumed to be Constant)
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <iomanip> //<--to show the data
      #include <iostream> //<-- used for file output. (Graphing in excel)
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
    double dt=0.01;
    double dx=1.0;
    double u0=25;
    double k=10;

    heatRK4(mesher2D(dx,dt,x,t),u0,k);

}
```

The first and last lines printed are shown below:

```c++
Starting:  20        25        25        25        25        25        25        25        25        25       100
Ending:    20   26.0791   32.3443   38.9642   46.0738   53.7615   62.0599   70.9417   80.3219   90.0652       100 
```

**Implementation/Code:** The following is the code for heatRK4()
```c++
vector<vector<double> > heatRK4(vector<vector<double> > mesh,double u0,double k){

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
	double C=0.5*dt;

    vector<double> a(xlength);
    vector<vector<double> > u(tlength,a);
	vector<double> Y1(xlength);
    vector<double> Y2(xlength);
    vector<double> Y3(xlength);
    vector<double> Y4(xlength);

    //Initial value assignment
    //Change to vector if different initial temperatures along x direction
    for (int i=0;i<xlength;i++){
        u[0][i]=u0;
    }
    //Sets the boundaries for initial conditions
    u[0][0]=g1(mesh[1][0]);
    u[0][xlength-1]=g2(mesh[1][0]);

    for (int p=0;p<tlength-1;p++){
        ///Makes sure boundary conditions are kept throughout the Y vectors
        //x=0 end
        Y1[0]=u[p][0];
        Y2[0]=u[p][0];
        Y3[0]=u[p][0];
        Y4[0]=u[p][0];
        //x=L end
        Y1[xlength-1]=u[p][xlength-1];
        Y2[xlength-1]=u[p][xlength-1];
        Y3[xlength-1]=u[p][xlength-1];
        Y4[xlength-1]=u[p][xlength-1];

        //set up the Y values
        // Should be vectors same length as the spatial vector.
        for (int i=1;i<xlength-1;i++){
            Y1[i]=u[p][i];
        }
        for (int i=1;i<xlength-1;i++){
            Y2[i]=u[p][i]+C*functInital(i,dx,k,Y1);
        }
        for (int i=1;i<xlength-1;i++){
            Y3[i]=u[p][i]+C*functInital(i,dx,k,Y2);
        }
        for (int i=1;i<xlength-1;i++){
            Y4[i]=u[p][i]+C*functInital(i,dx,k,Y3);
        }
        for (int i=0;i<xlength;i++){
            u[p+1][i]=u[p][i]+(dt/6)*(functInital(i,dx,k,Y1)+2*functInital(i,dx,k,Y2)+2*functInital(i,dx,k,Y3)+functInital(i,dx,k,Y4));
        }

        //Set boundaries for time+1 values
        u[p+1][0]=g1(p);
        u[p+1][xlength-1]=g2(p);
    }

    ofstream myfile;
    myfile.open ("RK4.txt", ios::out | ios::trunc);
    cout<<"RK4"<<endl;
    for(int i=0;i<tlength;i++){
        for(int j=0;j<xlength;j++){
            //cout<<setw(10)<<u[i][j];
            myfile <<setw(10)<<u[i][j];
        }
        //cout<<endl;
        myfile<<endl;
	}
	myfile.close();

    return u;
}
```
