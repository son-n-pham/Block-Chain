# Smart Contract: Ethereum and Solidity

Course structure (Etherum and Solidity: The Complete Developer's Guide)

![image](https://user-images.githubusercontent.com/79841341/171518640-0e4f9af1-7efd-42b8-a034-9152fa16684e.png)

## First Smart Contract

```solidity
// Specifies the version of Solidity that our code is written with
pragma solidity ^0.4.17;

// Define a new contract having some methods and variable
contract Inbox {
    // Declare all of the insance variables and their types
    string public message;

    function Inbox(string initialMessage) public {
        message = initialMessage;
    }

    function setMessage(string newMessage) public {
        message = newMessage;
    }

    function getMessage() public view returns (string) {
       return message;
    }
}
```
