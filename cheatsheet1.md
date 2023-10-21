Solidity cheatsheet1

keyword `contract` and `pragma solidity`
```
pragma solidity >=0.5.0 <0.6.0;

contract HelloWorld {

}
```
State variables are permanently stored in contract storage.
```
contract Example {
  // This will be stored permanently in the blockchain
  uint myUnsignedInteger = 100;
}
```
struct
```
struct Person {
  uint age;
  string name;
}
```
array 
```
// Array with a fixed length of 2 elements:
uint[2] fixedArray;
// another fixed Array, can contain 5 strings:
string[5] stringArray;
// a dynamic Array - has no fixed size, can keep growing:
uint[] dynamicArray;
// you can declare an array as public, and Solidity will automatically create a getter method for it
Person[] public people;
```
function declarition
```
function eatHamburgers(string memory _name, uint _amount) public {

}
```
working with struct and array
```
struct Person {
  uint age;
  string name;
}
Person[] public people;

people.push(Person(16, "Vitalik"));
```
Private / Public / external /internal
 - it's convention to start private function names with an underscore (_).

more on functions 
```
function sayHello() public returns (string memory) {
  return greeting;
}

//So in this case we could declare it as a view function, meaning it's only viewing the data but not modifying it
function sayHello() public view returns (string memory) 

// Solidity also contains pure functions, which means you're not even accessing any data in the app
function _multiply(uint a, uint b) private pure returns (uint) {
  return a * b;
}
```
Keccak256 and Typecasting
```
//b1f078126895a1424524de5321b339ab00408010b7cf0e6ed451514981e58aa9
keccak256(abi.encodePacked("aaaac"));

uint8 a = 5;
uint b = 6;
// throws an error because a * b returns a uint, not uint8:
uint8 c = a * b;
// we have to typecast b as a uint8 to make it work:
uint8 c = a * uint8(b);
```

events
```
// declare the event
event IntegersAdded(uint x, uint y, uint result);

function add(uint _x, uint _y) public returns (uint) {
  uint result = _x + _y;
  // fire an event to let the app know the function was called:
  emit IntegersAdded(_x, _y, result);
  return result;
}
```
Your app front-end could then listen for the event. A JavaScript implementation would look something like:
```
YourContract.IntegersAdded(function(error, result) {
  // do something with result
})
```