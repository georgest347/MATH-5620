**Function Name:**           SOLDE()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will compute the solution at time 't' for the following differential equation:

<a href="https://www.codecogs.com/eqnedit.php?latex=my''&plus;cy'&plus;ky=f(t)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?my''&plus;cy'&plus;ky=f(t)" title="my''+cy'+ky=f(t)" /></a>

**Input:** A floating point number to find the machine precision around.

**Output:** This function writes the value of the machine precision to the screen.

**Usage/Example:**

Typically inputing one will find the machine precision. The function can be called as shown below:

      compEpsilon(1);
      
Output from the lines above:

      Machine Epsilon is: 1.0842e-019


**Implementation/Code:** The following is the code for compEpsilon()

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
