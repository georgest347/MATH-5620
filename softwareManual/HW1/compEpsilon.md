**Function Name:**           compEpsilon()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will compute the machine precision of a computer.

**Input:** A floating point number to find the machine precision around.

**Output:** This function writes the value of the machine precision to the screen.

**Usage/Example:**

Typically inputing one will find the machine precision. The function can be called as shown below:
```c++
      compEpsilon(1);
```      
Output from the lines above:
```c++
      Machine Epsilon is: 1.0842e-019
```

**Implementation/Code:** The following is the code for compEpsilon()
```c++
/*
Function created to find the machine
epsilon of a computer.
*/
void compEpsilon(float epsilon){

    //Define a variable to hold the old value of epsilon
    float old_epsilon;

    //A loop to find the machine epsilon. Finds the smallest value of epsilon when added to 1
    //does not equal one.
    while((1+epsilon)!=1){
        old_epsilon=epsilon;
        epsilon/=2;
    }
    //Prints the value on the screen
    cout<< "Machine Epsilon is: "<<old_epsilon<<endl;
    }
```
