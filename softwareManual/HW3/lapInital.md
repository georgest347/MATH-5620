**Function Name:**          lapInital()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function Initalizes the system of equations for the following laplacian equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=\Delta&space;u=f(x,y)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Delta&space;u=f(x,y)" title="\Delta u=f(x,y)" /></a>

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
    dx=0.25;
    dy=0.25;
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

    lapInital(mesher2D(dx,dy,xb,yb), uxb, uyb);
```

The results on the screen were as follows:

```c++
MESH
X     0  0.25   0.5  0.75     1
Y     0  0.25   0.5  0.75     1
function
         0         0         0         0         0
         0 0.0624593  0.124675  0.186403  0.247404
         0  0.124675  0.247404  0.366273  0.479426
         0  0.186403  0.366273  0.533303  0.681639
         0  0.247404  0.479426  0.681639  0.841471
A MATRIX
       -64        16         0        16         0         0         0         0         0 0.0624593
        16       -64        16         0        16         0         0         0         0  0.124675
         0        16       -64         0         0        16         0         0         0  0.186403
        16         0         0       -64        16         0        16         0         0  0.124675
         0        16         0        16       -64        16         0        16         0  0.247404
         0         0        16         0        16       -64         0         0        16  0.366273
         0         0         0        16         0         0       -64        16         0  0.186403
         0         0         0         0        16         0        16       -64        16  0.366273
         0         0         0         0         0        16         0        16       -64  0.533303
```
**Implementation/Code:** The following is the code for lapInital()
```c++
vector<vector<double> > lapInital(vector<vector<double> > mesh, vector<double> uxb, vector<double> uyb){
	/*-----------------------------------------------------------------------------------
	This fuction imports a 2D mesh to initalize a system of linear
	equations for the laplacian equation del u =f(x)
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

    double c1= -2*((1/(dx*dx))+(1/(dy*dy)));
    double c2=(1/(dx*dx));
    double c3=(1/(dy*dy));

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
				A[i][j] = c3;
			}
			//Lower band
            if (i == j +xlength-2) {
				A[i][j] = c3;
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
            A[i][an-1]=fun[ycount][xcount];
            //Takes care of x lower boundry condition U(0,y)
            if(xcount==1){
                A[i][an-1]=A[i][an-1]-c2*uxb[0];
            }
            //Takes care of x upper boundry condition U(1,y)
            if(xcount==xlength-2){
                A[i][an-1]=A[i][an-1]-c2*uxb[1];
            }
            //Takes care of y lower boundry condition U(x,0)
            if(ycount==1){
                A[i][an-1]=A[i][an-1]-c3*uyb[0];
            }
            //Takes care of y upper boundry condition U(x,1)
            if(ycount==ylength-2){
                A[i][an-1]=A[i][an-1]-c3*uyb[1];
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
