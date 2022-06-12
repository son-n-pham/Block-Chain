# Smart Contract: Ethereum and Solidity

Course structure (Etherum and Solidity: The Complete Developer's Guide)

![image](https://user-images.githubusercontent.com/79841341/171518640-0e4f9af1-7efd-42b8-a034-9152fa16684e.png)

## Smart Contracts: Building Blocks for Digital Markets
written by Nick Szabo

https://www.fon.hum.uva.nl/rob/Courses/InformationInSpeech/CDROM/Literature/LOTwinterschool2006/szabo.best.vwh.net/smart_contracts_2.html

### Basic idea of smart contracts:

Many kinds of contractual clauses can be embedded in the hardware and software we deal with, in such a way as to make breach of contract expensive (if desired, sometimes prohibitively so) for the breacher => Key idea of smart contracts is to embed them in the word. The contract should be:
- Robust against naive vandalism
- Robust against sophisticated, incentive compatible breach

Some definition:
- Vandal: A person who deliberately destroys or damages property belonging to others.
- Sophisticated vandalism (where the vandals can and are willing to sacrifice substantial resources, ie. a military attack by third party)

Some bacic principals of contract design:
- Observation- in order to detect thte first sign of breach and minimize losses, also is a reactive form of security. A proactive form of security is a physical mechanism that makes breach expensive.
- Verifiability: The ability to prove to an arbitrator that a contract has been performed or breached, or the ability of the arbitrator to find this out by other means.
- Privity: Knowledge and control over the contents and performacne of a contract should be distributed among parties only as much as is necessary for the performance that contract.
- Enforceability: and at the same time minimizing the need for enforcement.

### Transaction

![image](https://user-images.githubusercontent.com/79841341/173215760-a752384a-c439-46c9-982c-c574e66fe780.png)

#### Web3
Web3 is the tool for developers to interact with any blockchain network

![image](https://user-images.githubusercontent.com/79841341/173216013-527e63ef-9668-4d8b-99e7-d92c3e38af0a.png)

#### What is transaction

![image](https://user-images.githubusercontent.com/79841341/173215706-07eaaeae-4a96-4543-969b-a2fd4980ef48.png)

#### Why did we wait?



## First Smart Contract

```solidity
// Specifies the version of Solidity that our code is written with
pragma solidity ^0.4.17;

// Define a new contract having some methods and variable
contract Inbox {
    // Declare all of the insance variables and their types
    string public message;

    // Constructor Inbox
    function Inbox(string initialMessage) public {
        message = initialMessage;
    }

    // Method setMessage
    function setMessage(string newMessage) public {
        message = newMessage;
    }

    // Method getMessage
    function getMessage() public view returns (string) {
       return message;
    }
}
```

getMessage is 'calling' a function while setMessage is 'sending' a Transaction to a function. Because of these, we only get the transaction hash although we add return to setMessage function.

![image](https://user-images.githubusercontent.com/79841341/172404330-2b2abed7-226b-4f9b-a3ce-2d3570cea2aa.png)


## Function:

### Function syntax:

![image](https://user-images.githubusercontent.com/79841341/172398380-20f8ccf3-9d7a-42d4-8d00-f933f6c56548.png)

### Common function types:

![image](https://user-images.githubusercontent.com/79841341/172397122-4b196a04-7256-42b5-a5c2-d166f1529a4c.png)

## Custom Node Project

![image](https://user-images.githubusercontent.com/79841341/173176818-af370dbd-2120-43e6-b050-b9d58f19bf31.png)

## Testing with Mocha

### Mocha Function

![image](https://user-images.githubusercontent.com/79841341/173213365-d3f6b8ee-d8af-44e8-8103-e70f39fdb2e1.png)

### Example of testing with Mocha
```js
// PLAYING AROUND WITH MOCHA TO PRACTIsE TESTING
class Car {
	park() {
		return 'stopped';
	}
	drive() {
		return 'vroom';
	}
}

// Declare car variable first so that the instance car is generated and passed to describe
let car;

// Pre-setup before each test
beforeEach (() => {
	car = new Car();
});

describe('Car', () => {
	it('can park', () => {
		// const car = new Car();
		assert.equal(car.park(), 'stopped');
	});

	it('can drive', () => {
		// const car = new Car();
		assert.equal(car.drive(), 'vroom')});
	});
```

### Mocha Structure
