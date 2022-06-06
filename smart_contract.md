# Smart Contract: Ethereum and Solidity

Course structure (Etherum and Solidity: The Complete Developer's Guide)

![image](https://user-images.githubusercontent.com/79841341/171518640-0e4f9af1-7efd-42b8-a034-9152fa16684e.png)

## Smart Contracts: Building Blocks for Digital Markets
written by Nick Szabo

https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart_contracts_2.html

### Basic idea of smart contracts:

Many kinds of contratual clauses can be embedded in the hardware and software we deal with, in such a way as to make breach of contract expensive (if desired, sometimes prohibitively so) for the breacher => Key idea of smart contracts is to embed them in the word. The contract should be:
- Robust against naive vandalism
- Robust against sophisticated, incentive compatible breach

Some definition:
- Vandal: A person who deliberately destroys or damages property belonging to others.
- Sophisticated vandalism (where the vandals can and are willing to sacrifice substantial resources, ie. a military attack by third party)

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
