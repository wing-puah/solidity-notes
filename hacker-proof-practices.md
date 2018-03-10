# Hacker proof practices

## State Changes
Contract state modifying statements
+ Setting the value in __storage variable__
+ Emitting of events from the function
+ Creating a new contract instance
+ Sending __Ethers__
+ Using low level calls OR EVM assembly
+ Using __selfdestruct__
+ Calling functions that modify the state with any of the above

## View (Hacker proof practices)
View statements e.g. function getSomethingFixed() public view returns (uint)
+ Allowed to __read__ the
+ NOT allowed to use any __state change__ statement

## Pure (Hacker proof practices)
Pure statements e.g. function returnConstantFixed() public pure returns (uint)
+ NOT allowed to __read__ the storage
+ NOT allowed to use any __state change__ statement

## Examples of good and bad coding practices

### GET function
__Bad__
function getSomething() public returns(uint) {
  someValue = 10     // Shouldn't change the state of storage in GET function
  return someValue;
}

__Good__
function getSomethingFixed() public view returns(uint) {
  someValue = 10 // With view modifier, a state change in the function will cause compilation error, forcing developer to fix the error
  return someValue;
}

### RETURN a constant
__Bad__
function returnConstant() public returns(uint) {
  return someValue + 100 // This is not a constant
}

__Good__
function returnConstantFixed() public pure returns(uint) {
  return someValue + 100 // With pure modifier, a state change in the function will cause compilation error, forcing developer to fix the error  

  return 100 // This will return constant
}
