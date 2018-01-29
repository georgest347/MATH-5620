**Function Name:**          factorial()

**Author:** George Staples

**Language:** C++

**Description/Purpose:** This function finds the factorial of a given number. 

**Input:** The only input in this function is n, the number to find the factorial of.
  
The following headers must also be included:
  ```
      #include <iostream> <-- to show the number on screen
  ```

**Output:** This function ouputs the factorial of a value.

**Usage/Example:**

This function is used to solve the problem given below:
```
  5!=x
```
The driving code is defined below:
```
		double n = 5;
	double x;
	x=factorial(n);

	cout << x << endl;
```

The results on the screen were as follows:

```
	120

```

**Implementation/Code:** The following is the code for factorial()
```
double factorial(double n)
{
	if (n > 1)
		return n * factorial(n - 1);
	else
		return 1;
}
```
