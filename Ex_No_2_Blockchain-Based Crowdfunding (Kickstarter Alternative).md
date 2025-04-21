# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)

### Date: 16.04.2025

## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:

### Step 1:
Deploy a smart contract where the project owner sets the funding goal and deadline.

### Step 2:
Define campaign details: project owner address, funding goal, deadline, total contributions, and contributors.

### Step 3:
Contributors send ETH to the campaign, and their contribution is recorded in the contract.

### Step 4:
The smart contract tracks the total ETH raised for the campaign.

### Step 5:
After each contribution, check if the funding goal is met before the deadline.

### Step 6:
If the goal is met before the deadline, release funds to the project owner. If the goal isn’t met before the deadline, allow contributors to withdraw their funds.

### Step 7:
Contributors can withdraw their funds if the goal was not met.

### Step 8:
Once the deadline passes, the campaign ends, and either funds are released to the owner or refunded to contributors.

## Program:
```

Register number: 212222100058

// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Output:

![exp2 1](https://github.com/user-attachments/assets/1ab56bd1-9a5a-4b9f-a2c9-59c803bf871d)
![exp2 3](https://github.com/user-attachments/assets/64372a50-2eeb-4670-9290-0d595f9bbe0e)
![exp2 2](https://github.com/user-attachments/assets/bb70a52d-bfcc-43e5-9c62-764d8bca01f5)


# High-Level Overview:
Teaches decentralized fundraising.


Avoids fraud by ensuring funds are only transferred if the goal is met.

# RESULT: 
 Thus, a decentralized crowdfunding platform has been created and successfully executed.
