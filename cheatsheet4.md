Recap 
 - We have visibility modifiers that control when and where the function can be called from: private means it's only callable from other functions inside the contract; internal is like private but can also be called by contracts that inherit from this one; external can only be called outside the contract; and finally public can be called anywhere, both internally and externally.
 - We also have state modifiers, which tell us how the function interacts with the BlockChain: view tells us that by running the function, no data will be saved/changed. pure tells us that not only does the function not save any data to the blockchain, but it also doesn't read any data from the blockchain. Both of these don't cost any gas to call if they're called externally from outside the contract (but they do cost gas if called internally by another function).
 
Payable modifier
```
contract OnlineStore {
  function buySomething() external payable {
    // Check to make sure 0.001 ether was sent to the function call:
    require(msg.value == 0.001 ether);
    // If so, some logic to transfer the digital item to the caller of the function:
    transferThing(msg.sender);
  }
}
```