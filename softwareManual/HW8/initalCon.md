**Function Name:**          initalCon()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function provides inital conditions to the Hyperbolic PDE

[mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D) <<-- This function creates a 2D mesh for the FD problem. one axis is space and the other is time.\

**Input:** This function takes the following inputs:\
mesh: A matrix that contains the 2D mesh. Can be produced by: [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)\
  
**Output:** This function outputs a vector 'n' that is the inital conditions of the PDE
	
**Usage/Example:**
Mesh was used to create a mesh with x values as follows:

```c++
   0 1 2 3 4 5 6 7 8 9 10
```
The function produced the following n vector

```c++
   1 1 1 1 1 0 0 0 0 0 0
```

**Implementation/Code:** The following is the code for initalCon()
```c++
vector<double> initalCon(vector<vector<double> > mesh){
        //Solves the inital conditions of the Advection Problem

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

    vector<double> n(xlength);

        for (int i=0;i<xlength/2;i++){
            n[i]=1;
        }
        for (int i=xlength/2;i<xlength;i++){
            n[i]=0;
        }

        for(int i=0;i<xlength;i++){
            cout<<n[i]<<endl;
        }

    return n;
}
```
