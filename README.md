# Payment-Splitter-Split-incoming-ETH-automatically-
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PaymentSplitter {
    address payable public recipient1;
    address payable public recipient2;
    uint256 public share1 = 60; // 60%
    uint256 public share2 = 40; // 40%

    constructor(address payable _recipient1, address payable _recipient2) {
        recipient1 = _recipient1;
        recipient2 = _recipient2;
    }

    receive() external payable {
        uint256 amount1 = (msg.value * share1) / 100;
        uint256 amount2 = msg.value - amount1;

        recipient1.transfer(amount1);
        recipient2.transfer(amount2);
    }
}
