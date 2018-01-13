**Function Name:**           relativeError()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function will compute the relative error of two values.

**Input:** The real value, and the approximated value. Both numbers are double.

**Output:** The function will return the decimal value of the relative error.

**Usage/Example:**

Use the function as shown below to find the relative error between 1 and 0.75. 

      cout<<relativeError(1,0.75)<<endl;
      
Output from the lines above:

      0.25
The value returned from relativeError() can also be stored in a variable as shown below:

    double relError=relativeError(1,0.75);

**Implementation/Code:** The following is the code for relativeError()

    double relativeError(double realValue, double approxValue){

        if  (realValue == 0)
        {
            cout<<"Can not divide by 0"<<endl;
            return 0;
        }
        else{
            double relError=abs((realValue-approxValue)/realValue);
            return relError;
        }

    }
