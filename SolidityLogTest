//SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

contract SolidityLogTest { 

    function exudeLog(bytes32 e, uint t0, bytes32 t1, bytes memory t2, bytes memory t3, bytes memory data) private {
        assembly { 
            let p := add(0x0, 0x20)
            mstore(p, data) 
            if eq(t0, 0x1) {
                log1(p, 0x20, e)  
            } 
            if eq(t0, 0x2) {
                log2(p, 0x20, e, t1)  
            } 
            if eq(t0, 0x3) {
                log3(p, 0x20, e, t1, t2)  
            }
            if eq(t0, 0x4) {
                log4(p, 0x20, e, t1, t2, t3)  
            }
        }
  } 

	function log(string memory n) external { 
		exudeLog(getName(n), 1, "", "", "", "");
	}

	function logInt(string memory n, int p0) external { 
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logUint(string memory n, uint p0) external {
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logString(string memory n, string memory p0) external {
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logBool(string memory n, bool p0) external {
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logAddress(string memory n, address p0) external {
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logBytes32(string memory n, bytes32 p0) external {
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logBytes(string memory n, bytes memory p0) external {
		exudeLog(getName(n), 2, keccak256(abi.encodePacked(p0)), "", "", "");
	}

	function logBytes(string memory n, uint p0, string memory p1, bool p2) external {
		exudeLog(getName(n), 4, keccak256(abi.encodePacked(p0)), abi.encodePacked(p1), abi.encodePacked(p2), "");
	}

  function getName(string memory eventName) private pure returns (bytes32) {
    return keccak256(abi.encodePacked(eventName));
  }

}
