**Function Name:**          lapInital9pt()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function Initalizes the system of equations for the following laplacian equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=\Delta&space;u=f(x,y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Delta&space;u=f(x,y)" title="\Delta u=f(x,y)" /></a>

It initalizes the system of equations based on a 9pt method.
The function f(x,y) can be specified by the user with the [functInital](https://georgest347.github.io/MATH-5620/softwareManual/HW3/functInital) function.

**Input:** This function takes a 2D mesh created by [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D), and also two vectors containing the Dirichlet boundry condition values.
These specify the boundry conditions 0 index corresponds to the lower bound, 1 index corresponds to the upper bound
    uxb[0]=0;
    uxb[1]=0;
    uyb[0]=0;
    uyb[1]=0;

  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
  ```
**Output:** This function outputs a matrix of the form:

<a href="https://www.codecogs.com/eqnedit.php?latex=A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" target="_blank"><img src="https://latex.codecogs.com/gif.latex?A=\left&space;[&space;\left.\begin{matrix}&space;a_{11}&space;&a_{12}&space;&a_{13}&space;\\&space;a_{21}&space;&a_{22}&space;&a_{23}&space;\\&space;a_{31}&space;&a_{32}&space;&a_{33}&space;\end{matrix}\right|&space;\begin{matrix}&space;b_{1}\\&space;b_{2}\\&space;b_{3}&space;\end{matrix}&space;\right&space;]" title="A=\left [ \left.\begin{matrix} a_{11} &a_{12} &a_{13} \\ a_{21} &a_{22} &a_{23} \\ a_{31} &a_{32} &a_{33} \end{matrix}\right| \begin{matrix} b_{1}\\ b_{2}\\ b_{3} \end{matrix} \right ]" /></a>

Where the b vector is the last column in the matrix.
	
**Usage/Example:**

This function was initalized with the following driving code:
```c++
      double dx,dy;
    vector<double> xb(2);
    vector<double> yb(2);
    vector<double> uxb(2);
    vector<double> uyb(2);
    dx=0.2;
    dy=0.2;
    //These specify the bounds of the interval 0 index corresponds
    // to the lower bound, 1 index corresponds to the upper bound
    xb[0]=0.0;
    xb[1]=1.0;
    yb[0]=0.0;
    yb[1]=1.0;
    //These specify the boundry conditions 0 index corresponds
    // to the lower bound, 1 index corresponds to the upper bound
    uxb[0]=0;
    uxb[1]=0;
    uyb[0]=0;
    uyb[1]=0;

    //mesher2D(dx,dy,xb,yb);
    aLUb(lapInital9pt(mesher2D(dx,dy,xb,yb), uxb, uyb));
```

The results on the screen were as follows:

```c++
MESH
X     0   0.2   0.4   0.6   0.8     1
Y     0   0.2   0.4   0.6   0.8     1
function
         0         0         0         0         0         0
         0 0.0399893 0.0799147  0.119712  0.159318  0.198669
         0 0.0799147  0.159318  0.237703  0.314567  0.389418
         0  0.119712  0.237703  0.352274  0.461779  0.564642
         0  0.159318  0.314567  0.461779  0.597195  0.717356
         0  0.198669  0.389418  0.564642  0.717356  0.841471
A MATRIX
   83.3333   16.6667         0         0   16.6667   4.16667         0         0         0         0         0         0         0         0         0         0 0.0399893
   16.6667   83.3333   16.6667         0   4.16667   16.6667   4.16667         0         0         0         0         0         0         0         0         0 0.0799147
         0   16.6667   83.3333   16.6667         0   4.16667   16.6667   4.16667         0         0         0         0         0         0         0         0  0.119712
         0         0   16.6667   83.3333         0         0   4.16667   16.6667         0         0         0         0         0         0         0         0  0.159318
   16.6667   4.16667         0         0   83.3333   16.6667         0         0   16.6667   4.16667         0         0         0         0         0         0 0.0799147
   4.16667   16.6667   4.16667         0   16.6667   83.3333   16.6667         0   4.16667   16.6667   4.16667         0         0         0         0         0  0.159318
         0   4.16667   16.6667   4.16667         0   16.6667   83.3333   16.6667         0   4.16667   16.6667   4.16667         0         0         0         0  0.237703
         0         0   4.16667   16.6667         0         0   16.6667   83.3333         0         0   4.16667   16.6667         0         0         0         0  0.314567
         0         0         0         0   16.6667   4.16667         0         0   83.3333   16.6667         0         0   16.6667   4.16667         0         0  0.119712
         0         0         0         0   4.16667   16.6667   4.16667         0   16.6667   83.3333   16.6667         0   4.16667   16.6667   4.16667         0  0.237703
         0         0         0         0         0   4.16667   16.6667   4.16667         0   16.6667   83.3333   16.6667         0   4.16667   16.6667   4.16667  0.352274
         0         0         0         0         0         0   4.16667   16.6667         0         0   16.6667   83.3333         0         0   4.16667   16.6667  0.461779
         0         0         0         0         0         0         0         0   16.6667   4.16667         0         0   83.3333   16.6667         0         0  0.159318
         0         0         0         0         0         0         0         0   4.16667   16.6667   4.16667         0   16.6667   83.3333   16.6667         0  0.314567
         0         0         0         0         0         0         0         0         0   4.16667   16.6667   4.16667         0   16.6667   83.3333   16.6667  0.461779
         0         0         0         0         0         0         0         0         0         0   4.16667   16.6667         0         0   16.6667   83.3333  0.597195
```
Solving this system with the [aLUb](https://georgest347.github.io/MATH-5620/softwareManual/HW3/aLub) solver yielded the following vector of results.

```c++
These are the x values
0.000234161
0.000487942
0.000650681
0.00121849
0.000487942
0.00101068
0.00135065
0.00247828
0.000650681
0.00135065
0.00177845
0.00330617
0.00121849
0.00247828
0.00330617
0.00575495
```
**Implementation/Code:** The following is the code for lapInital9pt()
```c++
vector<vector<double> > lapInital9pt(vector<vector<double> > mesh, vector<double> uxb, vector<double> uyb){
	/*-----------------------------------------------------------------------------------
	This fuction imports a 2D mesh to initalize a system of linear
	equations for the laplacian equation del u =f(x
    It uses a 9pt method this function needs to have dx=dy
	------------------------------------------------------------------------------------*/

	//Read mesh
	int large=mesh[0].size();
	int xlength=0;
	int ylength=0;
	for(int i=1;i<large;i++){
            if(mesh[0][i]>mesh[0][i-1]){
                xlength++;
            }
            if(mesh[1][i]>mesh[1][i-1]){
                ylength++;
            }
	}
	xlength++;
	ylength++;
	double dx=mesh[0][1]-mesh[0][0];
	double dy=mesh[1][1]-mesh[1][0];
	//cout<<xlength<<"   "<<ylength<<endl;

	//Set up the matrix 'A'
	double am=(xlength-2)*(ylength-2);
	double an=am+1;
	vector<double> a(an);
	vector<vector<double> > A(am,a);
	//Checks to make sure dx=dy
    if(dx!=dy){
        cout<<"SET dx=dy"<<endl;
        return A;
	}
    double h=dx;
    double c0=(1/(6*h*h));
    double c1=c0*20;
    double c2=c0*4;
    double c3=0;

   	for(int i=0;i<am;i++){
        for(int j=0;j<am;j++){
            //Main Diagonal
            if (i == j){
				A[i][j] =c1;
			}
			//Lower diagonal
			if (i == j + 1&& (j+1)%(xlength-2)!=0) {
				A[i][j] = c2;
            }
			//Upper diagonal
			if (i == j - 1&& (i+1)%(xlength-2)!=0) {
				A[i][j] = c2;
			}
			//Upper band
            if (i==j- (xlength-2)) {
				A[i][j] = c2;
				if((j+1)%(xlength-2)!=0){
                    A[i][j+1]=c0;
				A[i+1][j]=c0;
				}
			}
			//Lower band
            if (i == j +xlength-2) {
				A[i][j] = c2;
                if((j+1)%(xlength-2)!=0){
                    A[i][j+1]=c0;
                    A[i+1][j]=c0;
				}
			}
        }
	}
	//Find the value of the function at all x and y points
	vector<double> row(xlength);
	vector<vector<double> > fun(ylength,row);
	fun=functInital(mesh);

	//Add b vector as a column vector to the end of A
	int xcount=1;
	int ycount=1;
    for(int i=0;i<am;i++){

            //inserts f(x,y)
            A[i][an-1]=fun[ycount][xcount];

            //Takes care of x lower boundry condition U(0,y)
            if(xcount==1){
                A[i][an-1]=A[i][an-1]-6*c0*uxb[0];
            }
            //Takes care of x upper boundry condition U(1,y)
            if(xcount==xlength-2){
                A[i][an-1]=A[i][an-1]-6*c0*uxb[1];
            }

            //Takes care of y lower boundry condition U(x,0)
            if(ycount==1){
                A[i][an-1]=A[i][an-1]-6*c0*uyb[0];
            }

            //Takes care of y upper boundry condition U(x,1)
            if(ycount==xlength-2){
                A[i][an-1]=A[i][an-1]-6*c0*uyb[1];
            }

            //Takes care of the corners
            if(xcount ==1 && ycount==1){
                A[i][an-1]=A[i][an-1]+(0.5)*(uxb[0]+uyb[0])*c0;
            }
            if(ycount==1&&xcount==(xlength-2)){
                A[xlength-3][an-1]=A[xlength-3][an-1]+(0.5)*(uxb[1]+uyb[0])*c0;
            }
            if(xcount==1&&ycount==(xlength-2)){
                A[am-(xlength-2)][an-1]=A[am-(xlength-2)][an-1]+(0.5)*(uyb[1]+uxb[0])*c0;
            }
            if(xcount==(xlength-2)&&ycount==(xlength-2)){
                A[am-1][an-1]=A[am-1][an-1]+(0.5)*(uxb[1]+uyb[1])*c0;
            }

            //cout<<"x"<<xcount<<"y"<<ycount<<endl;
            if(xcount<=xlength-3){
                xcount++;
            }
            else{
                xcount=1;
                ycount++;
            }
    }

    cout<<"A MATRIX"<<endl;
    for(int i=0;i<am;i++){
        for(int j=0;j<an;j++){
            cout<<setw(10)<<A[i][j];
        }
        cout<<endl;
	}


	return A;
}
```
