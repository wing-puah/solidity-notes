# Any other programming concepts

## Function overloading
Function overloading (also method overloading) is a programming concept that allows programmers to define two or more functions with the same name and in the same scope.

Solidity supports function overloading but not constructor overloading. There could only be one constructor.

### Examples of function overloading
```
function int generateNumber (int MaxValue) {
  return rand * MaxValue
}

function int generateNumber (int MinValue, int MaxValue) {
  return MinValue + rand * (MaxValue - MinValue)
}
```
When the __first__ function is called, it will generate numbers from 0 up to specified parameter MaxValue.
int Number = generateNumber(10)

When the __second__ function is called, it will return numbers above or equals MinValue and lower than MaxValue.
int Number = generateNumber(6, 10)
