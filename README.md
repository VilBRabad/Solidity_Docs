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
   // SPDX-License-Identifier: GPL-3.0
   Pragma solidity >= 0.5.0 < 0.9.0;

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
   // SPDX-License-Identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0

   contract Local{
      string nam = "Vil"; // Static

      function store() pure public{
         string memory snam ="Rabad";
         uint age = 11; //local
      }
   }
```

## 3. Functions:

Steps for Declaring function:
* Function write with **function** keyword.
* followed by name of the function.
* Then Specified the function Type (public/private/protected).
* Then we write *view or pure* (If read or write operation done in function).
* Then we write return type in returns.
```solidity
   // SPDX-License-Identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0;

   contract Funct{
      uint age = 10;
      function getter() public view returns(uint){
         return age;
      }
      function setter() public{
         age = age + 10;
      }
   }
```

#### Some Key Points about Function:
* When you call a setter function it creates a transaction that need to be mined and costs gas because it changes the blockchain. Vice versa for getter function
* When you declare a public state variable a getter function automatically created.
* By default variable visibility is private.


### Pure VS View:
* When we do not get or set state variable in function then we can write **pure** keyword. But we need to perform get & set operation in it Then only we can use pure.
* When we try to get an state variable then we write **view** keyword. Also we can write at position pure.
* If we try to get or set without using one of above keyword then contract will give an error.

### Contructor:
A type of function which calls automatically.

```solidity
   // SPDX-License-identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0;

   contract state{
      uint public count;
      constructor(){
         count = 10;
      }
   }
```
> When we write *public* (Keyword) along with state variable **Remix IDE** creates its getter function to see value store in that variable.

* We can passed argument also.
* Executed only once.
* You can create only one constuctor and that is optional.
* A default constructor is created by the compiler if there is no explicitly defined constructor.



## 4. Interger Data Type:
* There are two type of Integers i.e int, uint
* uint can not Initialize with (or store) a Negative value.

```
        int                  uint
         |                    |
signed and unsigned Integers can be of various sizes
         |                    |
   nt8 to int256       uint8 to uint256
         |                    |
int alias to int256    uint alias to uint256
         |                    |
   By default an int is initialized to 0
```

#### Range:

| int | uint |
|:-----|:-------|
| int8: -128 to +127 | uint8: 0 to 255 |
| int16: -32768 to +32767 | uint16: 0 to 65535 |
| -2^(n-1) **to** (2^(n-1)) -1 | 0 **to** 2^(n) -1 |


> [Integer Overflow(i.e. proxyOverflow Bug) Found in Multiple ERC20 Smart Contracts (CSV-2018-10376)](https://peckshield.medium.com/integer-overflow-i-e-proxyoverflow-bug-found-in-multiple-erc20-smart-contracts-14fecfba2759)

> [New batchOverflow Bug in Multiple ERC20 Smart Contracts (CVE-2018–10299)](https://peckshield.medium.com/alert-new-batchoverflow-bug-in-multiple-erc20-smart-contracts-cve-2018-10299-511067db6536)


## 5. Array:
There are two type of array:
1. Fixed Size Array
2. Dynamic Size Array

### 1. Fixed Size Array:
Need to give length of Array at compile time.</br>
Declaration:
```solidity
   // SPDX-License-Identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0;

   contract Array{
      uint[4] public arr = [10, 20, 30, 40];
   }
```
* We can access element from array with the help of Index (0, 1.....).

Changing value at Index:
```solidity
   // SPDX-License-Identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0;

   contract Array{
      uint[4] public arr = [10, 20, 30, 40];

      function setter(uint index, uint value) public{
         arr[index] = value;
      }
   }
```

### 2. Dynamic Size Array:
Do not need to set length of array at compile time.
Declaration:
```solidity
   // SPDX-License-Identifier: GPL-3.0
   pragma solidity >= 0.5.0 < 0.9.0;

   contract Array{
      uint[] public arr;
   }
```
* There are push & pop member function dynamic array to insert and delete the data.