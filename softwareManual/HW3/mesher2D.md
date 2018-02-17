**Function Name:**          mesher2D()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function creates a 2D mesh.

**Input:** 
    dx=mesh size in x direction
    dy=mesh size in y direction
    xb= vector containing lower bound at i=0, and upper bound at i=1 for the x direction
    yb= vector containing lower bound at i=0, and upper bound at i=1 for y the y direction
  
The following headers must also be included:
  ```c++
      #include <iostream> //<-- to show the number on screen
      #include <vector>  //<-- to define the aformentioned vectors and matricies
  ```

**Output:** This function outputs a matrix with the top row as the x mesh values and the bottom frow as the y mesh values.
	
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
    
    mesher2D(dx,dy,xb,yb);
    
```
The results on the screen were as follows:

```c++
MESH
X     0  0.25   0.5  0.75     1
Y     0  0.25   0.5  0.75     1
```
This mesher can also handle meshes that are not square, such as the one initalized below:

```c++
    double dx,dy;
    vector<double> xb(2);
    vector<double> yb(2);
    vector<double> uxb(2);
    vector<double> uyb(2);
    dx=0.1;
    dy=0.25;
    //These specify the bounds of the interval 0 index corresponds
    // to the lower bound, 1 index corresponds to the upper bound
    xb[0]=0.0;
    xb[1]=1.0;
    yb[0]=0.0;
    yb[1]=1.0;
    
    mesher2D(dx,dy,xb,yb);
```
The results on the screen were as follows:

```c++
MESH
X     0   0.1   0.2   0.3   0.4   0.5   0.6   0.7   0.8   0.9     1
Y     0  0.25   0.5  0.75     1     0     0     0     0     0     0
```

**Implementation/Code:** The following is the code for mesher2D()
```c++
vector<vector<double> > mesher2D(double dx, double dy, vector<double> xb, vector<double> yb){
    /*------------------------------------------------------------------------------------------------------------------------------
    This function sets up a two dimensional mesh given the boundry values, and mesh element size
    dx=mesh size in x direction
    dy=mesh size in y direction
    xb= vector containing lower bound at i=0, and upper bound at i=1 for x
    yb= vector containing lower bound at i=0, and upper bound at i=1 for y
    ------------------------------------------------------------------------------------------------------------------------------*/
    // Checks to make sure bounds are given as described above
    if(xb[0]>=xb[1]){
        cout<<"CHECK X BOUNDS"<<endl;
        vector<double> er(2);
        vector<vector<double> > error(2,er);
        return error;
    }
    if(yb[0]>=yb[1]){
        cout<<"CHECK Y BOUNDS"<<endl;
                vector<double> er(2);
        vector<vector<double> > error(2,er);
        return error;
    }

     //Divide the interval up into mesh points for x and y
    double n=(xb[1]-xb[0])/dx+1;
    double m=(yb[1]-yb[0])/dy+1;
    double large;
    if(n>=m){
         large=n;
    }
    else{
        large=m;
    }
    vector<double> leg(large);
    vector<vector<double> > mesh(2,leg);

    mesh[0][0]=xb[0];
    mesh[1][0]=yb[0];
    for(int i=1;i<n;i++){
        mesh[0][i]=mesh[0][i-1]+dx;
    }
    for(int i=1;i<m;i++){
        mesh[1][i]=mesh[1][i-1]+dy;
    }


    cout<<"MESH"<<endl;
    cout<<"X";
    for(int i=0;i<2;i++){
        for(int j=0;j<large;j++){
            cout<<setw(6)<<mesh[i][j];
        }
        cout<<endl;
        if(i==0){
            cout<<"Y";
        }
    }


    return mesh;
}
```
