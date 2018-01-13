**Function Name:**           absoluteError()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will compute the absolute error between a actual value and an approximation.

**Input:** Two double numbers. The first is the real value and the second is the approximated value.

**Output:** This function returns the absolute error as a double.

**Usage/Example:**

The function is used when the absolute error is desired between two numbers. It can be called by:

       cout<<compEpsilon(6,6.5)<<endl;
      
Output from the lines above:

      0.5
      
The value can also be stored for later use by:

    double error=compEpsilon(6,6.5);

**Implementation/Code:** The following is the code for absoluteError()

    double absoluteError(double realValue, double approxValue){
        double absError=abs(realValue-approxValue);
        return absError;
    }
