# Mapping in Solidity
__mapping( \_KeyType => \_ValueType ) mapName__
+ Described as a hashtable (in Java) | Associative array in Javascript
+ \_KeyType can be almost any type except for a mapping
+ \_ValueType can be any type, including mapping
+ Returns 0, empty string for non existent keys
+ __keccak256__(Key data) hash is stored
+ Allowed only as a __storage__ or __state__ variable
+ __CANNOT__ be used as a __local__ variable in a function
+ __DOES NOT__ provide length function/attribute & a way to iterate

# Enums in Solidity
Enums are one way to create a user-defined type in Solidity. They are explicitly convertible to and from all integer types but implicit conversion is not allowed. The explicit conversions check the value ranges at runtime and a failure causes an exception. Enums needs at least one member.

# Struct in Solidity
Solidity provides a way to define new types in the form of __structs__. Struct types can be used inside mappings and arrays and they can itself contain mappings and arrays. Struct is kind of like an object. It has an object name and a bunch of properties inside.

+ Struct are not part of the public interface
+ External functions can not have struct type arguments
+ Struct type __cannot__ contain member of its own type

## Examples of Mapping and Struct
From https://www.youtube.com/watch?v=gfXewa4xmYE
contract Courses {

  struct Instructor {
    uint age;
    string fName;
    string lName;
  }

  mapping (address => Instructor) instructors;
  address[] public instructorAccts;

  function setInstructor(address \_address, uint \_age, string \_fName, string \_lName) public {
    var instructor = instructors[\_address];

    instructor.age = \_age;
    instructor.fName = \_fName;
    instructor.lName = \_lName;

    instructorAccts.push(\_address) -1;
  }

  function getInstructors() view public returns(address[]){
    return instructorAccts;
  }

  function getInstructor(address \_address) view public returns (uint, string, string){
    return (instructors[\_address].age, instructors[\_address].fName, instructors[\_address].lName);
  }

  function countInstructors() view public returns (uint) {
    return instructorAccts.length;
  }
}
