**Function Name:**          mesher1D()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function creates a 1D mesh.

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
vector<double>  mesher1D(vector<double> t, double n){
    /*-------------------------------------------------------------
    This function sets up a one dimensional mesh
    -------------------------------------------------------------*/
    int m=n+1; //number of numbers
    vector<double> time(m);
    double dt=(t[1]-t[0])/n;

    time[0]=t[0];
    time[m-1]=t[1];
    for(int i=1;i<m;i++){
        time[i]=time[i-1]+dt;
    }
    /*
    cout<<"MESH 1D"<<endl;
    cout<<"T";
    for(int i=0;i<m;i++){
        cout<<time[i]<<endl;
    }
    cout<<endl;
    */
    return time;
}
```
