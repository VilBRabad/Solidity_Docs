# SOLIDITY 
Reference: [Code Eater](https://www.youtube.com/watch?v=NqGe942J4Y0)

* Solidity is a High level Programming Language.
* Case Sensitive.
* Static programming language.
* We writes contract on Solidity.


## Solidity Compilation Process:


```
Contract Source File **.sol** file
               |
               |
      Solidity Compiler
         /           \
        /             \
      ABI          Byte Code
                       |
                       |
                  Ethereum Blockchain
```

**1. ABI** : (Abstract Binary Interface)
* Helps to Communicate others smart contract with this smart contrac.
* In the form of Array of JSON Obj. Format. Consisting Information of Function and more..
<br /> 

**2. Byte File** : 
* This consist JSON Object & this Obj...
* "object" key  consist byte code
* "opcode" key consist opcode (Instructions) --> to excute in EVM (Ethereum Virtual Machine).


### Some Imp Points:
1. Contract bytecode is public in readable form.
2. Contract doesn't have to be public.
3. Bytecode is immutable.
4. ABI act as a brigde between applications and smart contract.
5. ABI & Bytecode can not generate without source code.

## Mainnet VS Testnet

| Mainnet | Testnet |
|:--------|:--------|
| 1) A Network where real value of Ether has to transaction.| 1) Use for testing smart contracts & decentralized application. |
| 2) Mainnet Network ID is 1. | 2)Testnet has network IDs of 3, 4 $ 42. |
| 3) Ex. Ethereum Mainnet | 3) Ex. Georli, Sepolia Test Network. |

### Metamask: (Is a Crypto Wallet)
1. To Store Ether 
2. To Receive Ether
3. To Send Ether
4. To Run Decentralized Apps
5. To Swap tokens


## Let US Start with Solidity
*Basic Syntax:*
```solidity
   // SPDX-License-Identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0;

   contract Hello{
      function helloWorld() public pure returns(string memory){
         return "Hello World!";
      }
   }
```

### 1. State Variables
* Permanently stored in contract storage(Blockchain)
* Storage not dynamicaly allocated.
* State variables are variables that has been written in Contract.
* & Can not change without using a setter function or Contructor.
* You can initialize a variable using function or at the initialized time or using contructor. 
* Thats why Variables are expensive(Cost gas).

```solidity
   contract State{
      uint public age=5;

      //age = 10 Wronge initialization
      function setAge() public{
         age = 10;
      }
   }
```

### 2. Local Variables:
* Variables that declare in Functions
* Can be change easily.
* Dont cost gas
* Store in Stack
* There are some data types that reference the storage by default.
* To avoid conflict we write **memory** keyword along with variables.
* **string** neither store in stack nor in storage. it store in memory.
* we don't write **memory** keyword in contract level.

```solidity
   contract Local{
      string nam = "Vil"; // Static

      function store() pure public{
         string memory snam ="Rabad";
         uint age = 11; //local
      }
   }
```

### 3. Functions

