# The Usage of log1,log2,log3 and log4 in Solidity

### Test Case for `log1` for emitting an event without any parameters
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

### Test Case for for `log2` for emitting an event with one indexed parameter
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

### Test Case for `log3` for emitting an event with two indexed parameter
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


### Test Case for `log4` for emitting an event with three indexed parameter
```	
event Fire(address indexed t1, uint256 indexed t2, bool indexed t3);
function test9(string memory n, address t1, uint256 t2, bool t3) external { 
  emit Fire(t1, t2, t3);
  bytes32 e = keccak256(abi.encodePacked(n));  
  assembly {   
    log4(0x0, 0x0, e, t1, t2, t3)    
  }
} 
```

