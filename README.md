# solidity-coding-challenges-questions
Solidity coding challenges and interview questions

## Solidity screening questions

1. Can you prove within transaction runtime that particular event with particular set of arguments has been emitted on the contract in the past? If yes, how (general concept).

2. Can you verify that the there is a contract deployed at some Ethereum address with specific bytecode within Ethereum transaction context (i.e. you want to make sure that there is the trusted contract you need at some address with some predefined source code and not some malicious code before calling it)?

3. If your contract is calling some other contract’s function can this other contract’s function return a `struct` data structure and what are your options for it?
  
## Solidity coding challenge (10 minutes)

### Task
Add code to calculate storage address for value at address:
```
contract A {
  mapping (address => uint256) values;

  function getValue(address _addr) public view returns (bytes32 storagePointer) {
    assembly {
      // add code
    }
  }
}
```

## Solidity coding challenge 2 (2-4 hours)

### Task
Given the following set of contracts the goal is to implement to-bytes and from-bytes converter for structs to be able to pass them from contract to contract in a form of bytes. Please assume that `Storage` and `Controller` contracts have different addresses on the network. `StructDefiner` is never deployed on its own and is used as a part of `Storage` or `Controller`.

```
contract StructDefiner {
  struct MyStruct {
    uint256 someField;
    address someAddress,
    uint128 someOtherField
    uint128 oneMoreField
  }
}

contract Storage {
  StructDefiner.MyStruct[] internal structs;

  function getStructByIdx(uint256 idx) external view returns (bytes) {
    assembly {
        // your code here
    }
  }
}

contract Controller {
  Storage internal storage;

  constructor(addrerss _storage) {
    storage = Storage(_storage);
  }

  getStruct(uint256 idx) public returns (StructDefiner.MyStruct myStruct) {
    bytes memory _myStruct = storage.getStructByIdx(idx);
    assembly {
        // your code here
    }
  }
}


