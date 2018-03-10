# Error handling practices

+ Solidity has no support for try-catch like mechanism, so error will bubble up to the caller
+ Exception thrown in the contract leads to the rolling back of all the changes that have been made in the code prior to the throwing of exception. No ethers are sent out. If ethers were received in the transaction then on exception those ethers will be sent back to the sender. Caller of the contract will still have to pay for the gas that was expended for the execution of the operations prior to the throwing of the exception. Transaction is still recorded on the chain; nonce is valid & recorded.

## Error handling function
__revert()__ : Throws an exception and refunds the unused gas
__throw()__ : Deprecated starting v0.4.14 and uses up all the gas specified in contract call


### Examples of revert()
```
contract Globals {
  enum Timeunit {Minute, Hour, Day}
  string public lastCaller = "not-set";  // Variable in storage

  function revertBehavior(string name) public returns(bool) {
    lastCaller = name;

    if( bytes(name).length == 0) {
      revert();   // If name is not found, exception is thrown and rolled back to original statement of string public lastCaller = "not-set". Hence nullifying the lastCaller = name statement.  
    }

    return true;
  }
}
```

## Additional ways of throwing an exception
__require(condition)__: revert() style exception, unused gas is return.  
__assert(condition)__: throw() style exception, all gas is consumed. Internal use for catching code bugs.

### Examples of revert()
revert() is used in production.
```
if( bytes(name).length == 0) {
  revert();   
}
```
can be written as
```
require( bytes(name).length > 0 );
```
```
function guess(uint8 num) returns (bool){
  assert(num < 10;)

  for( uint8 i = 0; i < numArray.length; i++ ){
    if( numArray[i] == num ) {
      winnerCount++;
      __require( winnerCount > 0 );
      return true;
    }
  }
  loserCount++;
  return false;
}
```

### Examples of assert()
assert() is used to catch code bugs in testing environment. Code must not lead to such runtime exceptions. Example, division by 0, negative array index
```
int someVar = 100; //Assuming you need the var to always be bigger than 0

function someProcess(int num) public {
  someVar = someVar - num;
  // some variable gets manipulated here
  assert(someVar > 0);  //Ensure that testing should not lead to an assert exception
}
