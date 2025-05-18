# Experiment 7: AI-Powered Smart Contract for Decentralized Negotiation
# Aim:
# To create a smart contract that integrates AI logic for automated negotiation in decentralized commerce. The contract adjusts price and conditions dynamically based on real-time market trends using an on-chain AI model.

# Algorithm:
### Step 1: 
The seller lists an item with a minimum price and a defined negotiation range.

### Step 2: 
The buyer submits an offer price for the listed item.

### Step 3: 
AI logic evaluates the offer using market demand, historical data, and time-based pricing.

### Step 4: 
The smart contract checks if the offer meets, falls within, or is below the acceptable range.

### Step 5: 
If within range, the contract generates a counteroffer automatically.

### Step 6: 
The buyer chooses to accept, reject, or revise the counteroffer.

### Step 7: 
If accepted, the smart contract executes the transaction and transfers ownership.

### Step 8: 
The transaction data is fed into the price learning algorithm for refinement.

### Step 9: 
Future pricing decisions are dynamically optimized based on learned data.

# Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PostQuantumWallet {
    struct User {
        bytes32 publicKeyHash;
        bool registered;
    }

    mapping(address => User) private users; // Made private to hide from Remix UI
    mapping(address => uint256) public balances;

    event UserRegistered(address user, bytes32 publicKeyHash);
    event TransactionVerified(address from, address to, uint256 amount);

    // Constructor
    constructor() {}

    // Generate a quantum-safe signature (simulated using keccak256)
    function generateSignature(address _sender, address _recipient, uint256 _amount) public pure returns (bytes32) {
        return keccak256(abi.encodePacked(_sender, _recipient, _amount));
    }

    // Generate a simulated lattice-based public key hash
    function generatePublicKeyHash(string memory _publicKey) public pure returns (bytes32) {
        return keccak256(abi.encodePacked(_publicKey));
    }

    // Register a user with a public key hash
    function registerUser(bytes32 _publicKeyHash) public {
        require(!users[msg.sender].registered, "User already registered");
        users[msg.sender] = User(_publicKeyHash, true);
        emit UserRegistered(msg.sender, _publicKeyHash);
    }

    // Send funds using quantum-safe simulated signature
    function sendFunds(address _to, uint256 _amount, bytes32 _signature) public {
        require(users[msg.sender].registered, "Sender not registered");
        require(users[_to].registered, "Recipient not registered");
        require(balances[msg.sender] >= _amount, "Insufficient funds");

        bytes32 calculatedSignature = generateSignature(msg.sender, _to, _amount);
        require(calculatedSignature == _signature, "Invalid quantum-safe signature");

        balances[msg.sender] -= _amount;
        balances[_to] += _amount;
        emit TransactionVerified(msg.sender, _to, _amount);
    }

    // Deposit funds to the wallet
    function depositFunds() public payable {
        balances[msg.sender] += msg.value;}
}
```

# Output:
![image](https://github.com/user-attachments/assets/c2a9c93f-a3d5-4f47-819f-0cde1e950fd4)
![image](https://github.com/user-attachments/assets/8bb30c9b-7bc2-4d52-b6d9-0baead55636e)
![image](https://github.com/user-attachments/assets/5deb7db3-a01a-4c3e-8550-89953a99b50a)



# High-Level Overview:
First-of-its-kind AI-powered pricing contract.


Mimics real-world price negotiations using dynamic on-chain pricing.


Can be extended to AI oracles for real-time market data.


Inspired by AI-enhanced commerce and eBay-like decentralized auctions.

# RESULT:

Thus, a smart contract that integrates AI logic for automated negotiation in decentralized commerce is executed successfully.
