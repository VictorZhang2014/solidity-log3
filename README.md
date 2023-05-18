# The Usage of log1,log2,log3 and log4 in Solidity
<br/>

#### Deployed Contract for testing: [0x2b1437da111b553cb1384d8d290b08820fd188eb](https://mumbai.polygonscan.com/address/0x2b1437da111b553cb1384d8d290b08820fd188eb)
<br/>

#### Test Case for `log1` for emitting an event without any parameters
```	
event Fire();

function test1(string memory n) external { 
  emit Fire();
  
  bytes32 e = keccak256(abi.encodePacked(n)); 
  assembly {   
    log1(0x0, 0x0, e)    
  }
}
```
Transaction on Polygon mumbai network: https://mumbai.polygonscan.com/tx/0x0a7da0136ddd431aad5a90a4babcec709f62963b61df3f3341b5f54037b18bb0#eventlog
<br/>

#### Test Case for for `log2` for emitting an event with one indexed parameter
```	
event Fire(int256 indexed t1);

function test2(string memory n, int256 t1) external {  
  emit Fire(t1);
  
  bytes32 e = keccak256(abi.encodePacked(n)); 
  assembly {   
    log2(0x0, 0x0, e, t1)    
  }
}
```
Transaction on Polygon mumbai network: https://mumbai.polygonscan.com/tx/0xc1480bd039b41f6b59fccd4031a7f5951061472201af78aeaafee7b74c2cda74#eventlog
<br/>

#### Test Case for `log3` for emitting an event with two indexed parameters
```	
event Fire(address indexed t1, uint256 indexed t2);

function test8(string memory n, address t1, uint256 t2) external { 
  emit Fire(t1, t2);
  
  bytes32 e = keccak256(abi.encodePacked(n));  
  assembly {   
    log3(0x0, 0x0, e, t1, t2)    
  }
}
```
Transaction on Polygon mumbai network: https://mumbai.polygonscan.com/tx/0x10bf33dcd46cc6cda1e8315a5e2e735e73567cdc05841b51758847db9421e3b0#eventlog
<br/>

#### Test Case for `log4` for emitting an event with three indexed parameters
```	
event Fire(address indexed t1, uint256 indexed t2, bool indexed t3, int128 abc);

function test10(string memory n, address t1, uint256 t2, bool t3, int128 abc) external { 
  emit Fire(t1, t2, t3, abc);
  
  bytes32 e = keccak256(abi.encodePacked(n));   
  assembly {   
    let p := add(0x0, 0x20)
      mstore(p, abc) 
      log4(p, 0x20, e, t1, t2, t3)    
    }
} 
```
Transaction on Polygon mumbai network: https://mumbai.polygonscan.com/tx/0x98813736f2e60e3559837ee33278ea86990e557a0216fe91ca6c559354a86071#eventlog
<br/>

#### Test Case for `log4` with dynamic and non-indexed parameters, plus three indexed parameters
```	
event Fire(address indexed t1, uint256 indexed t2, bool indexed t3, uint256 abc);

function test11(string memory n, address t1, uint256 t2, bool t3, bytes memory data) external { 
  emit Fire(t1, t2, t3, abi.decode(data, (uint256)));
    
  bytes32 e = keccak256(abi.encodePacked(n));   
  assembly {   
    let p := add(data, 0x20)
    let s := mload(data) 
    log4(p, s, e, t1, t2, t3)    
  }
}  
```
Transaction on Polygon mumbai network: https://mumbai.polygonscan.com/tx/0x68cd6ab903e450c8d566eb80800aeec759f31b853823c4ee2fa359e13435c5f9#eventlog
<br/>

#### General Encapsulation for the four log functions
More details and invokation example, please check the source code here: [SolidityLogTest.sol](https://github.com/VictorZhang2014/solidity-log3/blob/main/SolidityLogTest.sol)
```
function exudeLog(uint i, bytes32 eventSig, bytes32 topic1, bytes32  topic2, bytes32 topic3, bytes memory data) public {
  assembly { 
		 let p := add(data, 0x20)
		 let s := mload(data) 
		    if eq(i, 0x1) {
          log1(p, s, eventSig)  
		    } 
		    if eq(i, 0x2) {
			    log2(p, s, eventSig, topic1)  
		    } 
		    if eq(i, 0x3) {
			    log3(p, s, eventSig, topic1, topic2)  
		    }
		    if eq(i, 0x4) {
			    log4(p, s, eventSig, topic1, topic2, topic3)  
		    }
		}
} 

function getEventSig(string memory eventSigStr) public pure returns (bytes32) {
  return keccak256(abi.encodePacked(eventSigStr));
}
```

<br/>
<br/>
<br/>


# Solidity的日志内置函数log1、log2、log3 和 log4的使用
<br/>

#### 对`log1`函数的测试，无参数
```	
event Fire();

function test1(string memory n) external { 
  emit Fire();
  
  bytes32 e = keccak256(abi.encodePacked(n)); 
  assembly {   
    log1(0x0, 0x0, e)    
  }
}
```
查看交易Polygon mumbai: https://mumbai.polygonscan.com/tx/0x0a7da0136ddd431aad5a90a4babcec709f62963b61df3f3341b5f54037b18bb0#eventlog
<br/>

#### 对`log2`的测试，有一个indexed的参数 
```	
event Fire(int256 indexed t1);

function test2(string memory n, int256 t1) external {  
  emit Fire(t1);
  
  bytes32 e = keccak256(abi.encodePacked(n)); 
  assembly {   
    log2(0x0, 0x0, e, t1)    
  }
}
```
查看交易Polygon mumbai: https://mumbai.polygonscan.com/tx/0xc1480bd039b41f6b59fccd4031a7f5951061472201af78aeaafee7b74c2cda74#eventlog
<br/>

#### 对`log3`的测试，有两个indexed的参数
```	
event Fire(address indexed t1, uint256 indexed t2);

function test8(string memory n, address t1, uint256 t2) external { 
  emit Fire(t1, t2);
  
  bytes32 e = keccak256(abi.encodePacked(n));  
  assembly {   
    log3(0x0, 0x0, e, t1, t2)    
  }
}
```
查看交易Polygon mumbai: https://mumbai.polygonscan.com/tx/0x10bf33dcd46cc6cda1e8315a5e2e735e73567cdc05841b51758847db9421e3b0#eventlog
<br/>

#### 对`log4`的测试，有三个indexed的参数
```	
event Fire(address indexed t1, uint256 indexed t2, bool indexed t3, int128 abc);

function test10(string memory n, address t1, uint256 t2, bool t3, int128 abc) external { 
  emit Fire(t1, t2, t3, abc);
  
  bytes32 e = keccak256(abi.encodePacked(n));   
  assembly {   
    let p := add(0x0, 0x20)
      mstore(p, abc) 
      log4(p, 0x20, e, t1, t2, t3)    
    }
} 
```
查看交易Polygon mumbai: https://mumbai.polygonscan.com/tx/0x98813736f2e60e3559837ee33278ea86990e557a0216fe91ca6c559354a86071#eventlog
<br/>

#### 对`log4`的测试，动态data的参数，传入动态长度字节数据
```	
event Fire(address indexed t1, uint256 indexed t2, bool indexed t3, uint256 abc);

function test11(string memory n, address t1, uint256 t2, bool t3, bytes memory data) external { 
  emit Fire(t1, t2, t3, abi.decode(data, (uint256)));
    
  bytes32 e = keccak256(abi.encodePacked(n));   
  assembly {   
    let p := add(data, 0x20)
    let s := mload(data) 
    log4(p, s, e, t1, t2, t3)    
  }
}  
```
查看交易示例Polygon mumbai: https://mumbai.polygonscan.com/tx/0x68cd6ab903e450c8d566eb80800aeec759f31b853823c4ee2fa359e13435c5f9#eventlog
<br/>

