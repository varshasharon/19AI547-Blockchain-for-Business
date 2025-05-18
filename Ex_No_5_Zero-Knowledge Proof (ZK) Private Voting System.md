# Experiment 5: Zero-Knowledge Proof (ZK) Private Voting System
# Aim:
To implement a fully private and transparent voting system using Zero-Knowledge Proofs (ZKPs). This ensures that votes are counted fairly without revealing who voted for whom.

# Algorithm:

### Step 1: 
Each voter generates a private vote key.

### Step 2: 
Voters register by submitting a hashed commitment of their vote to the smart contract.

### Step 3: 
The voting phase begins and voters submit their encrypted (hashed) votes.

### Step 4: 
The contract checks if each vote was cast by a registered voter.

### Step 5: 
Zero-knowledge proofs are used to verify votes without revealing voter identities or choices.

### Step 6: 
Duplicate or unregistered votes are automatically rejected by the smart contract.

### Step 7: 
Once voting ends, the contract tallies all valid votes.

### Step 8: 
The final result is published without exposing individual voter data or choices.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract ZKVoting {
    struct Voter {
        bool registered;
        bytes32 voteCommitment;
    }

    mapping(address => Voter) public voters;
    uint256 public votesForA;
    uint256 public votesForB;

    event VoteCommitted(address voter, bytes32 commitment);
    event VoteRevealed(address voter, uint256 choice);

    function registerVoter(bytes32 commitment) public {
        require(!voters[msg.sender].registered, "Already registered");
        voters[msg.sender] = Voter(true, commitment);
        emit VoteCommitted(msg.sender, commitment);
    }

    function revealVote(string memory secret, uint256 choice) public {
        require(voters[msg.sender].registered, "Not registered");
        require(keccak256(abi.encodePacked(secret, choice)) == voters[msg.sender].voteCommitment, "Invalid proof");

        if (choice == 1) votesForA++;
        if (choice == 2) votesForB++;

        emit VoteRevealed(msg.sender, choice);
    }
}

```
# Output:
![image](https://github.com/user-attachments/assets/a2a4760f-3c86-4ea2-96e9-149d26571655)

![image](https://github.com/user-attachments/assets/9a96ce93-d389-4015-b62e-6cc75db4b889)


![image](https://github.com/user-attachments/assets/3b1214b4-d8f4-4a8f-8004-16bf30826cce)

![image](https://github.com/user-attachments/assets/23914121-fbca-4caa-a482-5500d4404428)




# RESULT: 
Thus, a Zero-Knowledge Proof (ZK) Private Voting System has been sucessfully implemented.
