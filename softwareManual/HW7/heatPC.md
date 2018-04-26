**Function Name:**          heatPC()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function solves the 1D heat conduction problem given in the form shown below:

<a href="https://www.codecogs.com/eqnedit.php?latex=\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\frac{\delta&space;u}{\delta&space;t}=k\frac{\delta^2&space;u}{\delta&space;x^2}" title="\frac{\delta u}{\delta t}=k\frac{\delta^2 u}{\delta x^2}" /></a>

The PC FD method is a 3rd order PC method with the following predictor and corrector.

A 4step Adams-Bashforth method:\
<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;-9f(u^n)&plus;37f(u^{n&plus;1})-59f(u^{n&plus;2})&plus;55f(u^{n&plus;3})&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;-9f(u^n)&plus;37f(u^{n&plus;1})-59f(u^{n&plus;2})&plus;55f(u^{n&plus;3})&space;\right&space;)" title="u^{n+4}=u^{n+3}+\frac{\Delta t}{24}\left ( -9f(u^n)+37f(u^{n+1})-59f(u^{n+2})+55f(u^{n+3}) \right )" /></a>\
A 3step Adams-Moulton Method\
<a href="https://www.codecogs.com/eqnedit.php?latex=u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;f(u^{n&plus;1})-5f(u^{n&plus;2})&plus;19f(u^{n&plus;3})&plus;9f(u^{n&plus;4})&space;\right&space;)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?u^{n&plus;4}=u^{n&plus;3}&plus;\frac{\Delta&space;t}{24}\left&space;(&space;f(u^{n&plus;1})-5f(u^{n&plus;2})&plus;19f(u^{n&plus;3})&plus;9f(u^{n&plus;4})&space;\right&space;)" title="u^{n+4}=u^{n+3}+\frac{\Delta t}{24}\left ( f(u^n+1)-5f(u^{n+2})+19f(u^{n+3})+9f(u^{n+4}) \right )" /></a>

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
      #include <iostream> //<-- used for file output. (for Graphing)
      #include <fstream> //<-- used for file output. (for Graphing)
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

    heatRK4(mesher2D(dx,dt,x,t),u0,k);

}
```

The first and last lines printed are shown below:

```c++
Starting:  20        25        25        25        25        25        25        25        25        25       100
Ending:    20	       26.0788	 32.3438	 38.9634	 46.0728	 53.7605	 62.0589	 70.9409	 80.3212	 90.0649	100
 
```

**Implementation/Code:** The following is the code for heatPC()
```c++
vector<vector<double> > heatPC(vector<vector<double> > mesh,double u0,double k){
    // This is a third order predictor corrector method. With a 4th order adams bashforth
    // method to predict, and a 3rd order corrector method.

    ///Read mesh
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

    vector<double> a(xlength);
    vector<double> b(tlength);
    vector<vector<double> > u(tlength,a);
    vector<vector<double> > rkt(2,b);
    vector<vector<double> > temp(4,a);
    vector<double> Y0(xlength);
    vector<double> Y1(xlength);
    vector<double> Y2(xlength);
    vector<double> Y3(xlength);
    vector<double> Y4(xlength);


    ///Initial value assignment
    //Change to vector if different initial temperatures along x direction
    for (int i=0;i<xlength;i++){
        u[0][i]=u0;
    }
    //Sets the boundaries conditions
    u[0][0]=g1(mesh[1][0]);
    u[0][xlength-1]=g2(mesh[1][0]);

    ///Use the RK4 method to start
    for(int i=0;i<xlength;i++){
        rkt[0][i]=mesh[0][i];
    }
    for(int i=0;i<4;i++){
        rkt[1][i]=mesh[1][i];
    }

    temp=heatRK4(rkt,u0,k);


    for (int p=0;p<4;p++){
        for (int i=0;i<xlength;i++){
            u[p][i]=temp[p][i];
        }
    }

    for(int p=4;p<tlength;p++){
        for (int z=0;z<xlength;z++){
            Y1[z]=u[p-1][z];
            Y2[z]=u[p-2][z];
            Y3[z]=u[p-3][z];
            Y4[z]=u[p-4][z];
        }

        // calculate interior values
        for (int i=1;i<xlength-1;i++){
            //4 step Adams-Bashforth Method
            u[p][i]=Y1[i]+(dt/24)*(-9*functInital(i,dx,k,Y4)+37*functInital(i,dx,k,Y3)-59*functInital(i,dx,k,Y2)+55*functInital(i,dx,k,Y1));
        }

        //Set b.c
        u[p][0]=g1(p);
        u[p][xlength-1]=g2(p);

        //For use in the Corrector
        for (int j=0;j<xlength;j++){
            Y0[j]=u[p][j];
        }

        for (int i=1;i<xlength-1;i++){
            //3 step Adams-Moulton Method
            u[p][i]=Y1[i]+(dt/24)*(functInital(i,dx,k,Y3)-5*functInital(i,dx,k,Y2)+19*functInital(i,dx,k,Y1)+9*functInital(i,dx,k,Y0));
        }
        //Set b.c
        u[p][0]=g1(p);
        u[p][xlength-1]=g2(p);

    }

    ofstream myfile;
    myfile.open ("PreCor.txt", ios::out | ios::trunc);
    cout<<"Predict Correct"<<endl;
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

int main()
{
    vector<double> t(2);
    vector<double> x(2);
    t[0]=0;
    t[1]=2;
    x[0]=0;
    x[1]=10;
    double dt=0.001;
    double dx=1;
    double u0=25;
    double k=10;

    //heatEE1D(mesher2D(dx,dt,x,t),u0,k);
    //heatIE1D(mesher2D(dx,dt,x,t),u0,k);
    //heatPC(mesher2D(dx,dt,x,t),u0,k);
    //heatRK4(mesher2D(dx,dt,x,t),u0,k);
    heatPC(mesher2D(dx,dt,x,t),u0,k);
}
```
