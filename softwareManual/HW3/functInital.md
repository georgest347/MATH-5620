**Function Name:**          functInital()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function provides inital values for the function f(x,y)=sin(x*y)

**Input:** This function takes a mesh created by [mesher2D](https://georgest347.github.io/MATH-5620/softwareManual/HW3/mesher2D)
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
      #include <cmath> //<-- for the sin value function
  ```

**Output:** This function outputs a matrix of f(x,y) values for each point in the mesh.
	
**Usage/Example:**

Given a mesh of the form:
```c++
  MESH Xtop Ybottom
  0   0.25    0.5   0.75    1
  0   0.25    0.5   0.75    1
```

The results on the screen were as follows:

```c++
function
         0         0         0         0         0
         0 0.0624593  0.124675  0.186403  0.247404
         0  0.124675  0.247404  0.366273  0.479426
         0  0.186403  0.366273  0.533303  0.681639
         0  0.247404  0.479426  0.681639  0.841471
```
**Implementation/Code:** The following is the code for functInital()
```c++
vector<vector<double> > functInital(vector<vector<double> > mesh) {
	// Function that initalizes the f(x,y) values for the b vector
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
	vector<double> row(xlength);
	vector<vector<double> > fun(ylength,row);
	for(int i=0;i<ylength;i++){
        for(int j=0;j<xlength;j++){
            //CHANGE THIS FUNCTION to user defined f(x,y)
            fun[i][j]=sin(mesh[0][j]*mesh[1][i]);
        }
	}


	cout<<"function"<<endl;
	for(int i=0;i<ylength;i++){
        for(int j=0;j<xlength;j++){
            cout<<setw(10)<<fun[i][j];
        }
        cout<<endl;
	}


	return fun;
}
```
