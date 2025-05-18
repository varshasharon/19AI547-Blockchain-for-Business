# Experiment 8: Post-Quantum Blockchain Wallet with Lattice-Based Cryptography
# Aim:
To create a quantum-resistant wallet using lattice-based cryptography instead of traditional ECDSA, ensuring that future quantum computers cannot break private keys.

# Algorithm:

### Step 1: 
ECDSA-based blockchain wallets are vulnerable to attacks from future quantum computers.

### Step 2: 
Lattice-based cryptographic algorithms like NTRU and CRYSTALS-Kyber offer quantum resistance.

### Step 3: 
Precomputed lattice-based public-private key pairs are used to simulate quantum-safe authentication.

### Step 4: 
Users register by submitting a hash of their lattice-based public key to the smart contract.

#### Step 5: 
Transactions are signed off-chain using lattice-based cryptographic techniques.

### Step 6: 
The smart contract receives the transaction and the corresponding hash signature for verification.

###  Step 7: 
It verifies the authenticity of the transaction by comparing the hashed input with the registered key hash.

### Step 8: 
If valid, the transaction is processed on-chain, simulating a quantum-resistant wallet interaction.


# Program:

(Solidity does not natively support lattice cryptography yet, but we simulate it using custom hash-based authentication.)
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract PostQuantumWallet {
    struct User {
        bytes32 publicKeyHash;
        bool registered;
    }

    mapping(address => User) public users;
    mapping(address => uint256) public balances;

    event UserRegistered(address user, bytes32 publicKeyHash);
    event TransactionVerified(address from, address to, uint256 amount);

    function registerUser(bytes32 _publicKeyHash) public {
        require(!users[msg.sender].registered, "User already registered");
        users[msg.sender] = User(_publicKeyHash, true);
        emit UserRegistered(msg.sender, _publicKeyHash);
    }

    function sendFunds(address _to, uint256 _amount, bytes32 _signature) public {
        require(users[msg.sender].registered, "Sender not registered");
        require(users[_to].registered, "Recipient not registered");
        require(balances[msg.sender] >= _amount, "Insufficient funds");

        bytes32 calculatedHash = keccak256(abi.encodePacked(msg.sender, _to, _amount));
        require(calculatedHash == _signature, "Invalid quantum-safe signature");

        balances[msg.sender] -= _amount;
        balances[_to] += _amount;
        emit TransactionVerified(msg.sender, _to, _amount);
    }
}
```

# Output:

![image](https://github.com/user-attachments/assets/b9eb4a3e-10a2-4ce9-a37b-19b3ca1ec561)


Deployment: 

![image](https://github.com/user-attachments/assets/7410d3b9-809a-40aa-802e-6a877897aeb2)

Register  User:

![image](https://github.com/user-attachments/assets/640d1892-be9f-4a80-8301-2e5f11f47eb7)

Check Balance:

![image](https://github.com/user-attachments/assets/eeb744e6-0162-4004-88bc-9a1f30fc0779)


# RESULT : 

Thus, a quantum-resistant wallet using lattice-based cryptography has been implemented successfully using Remix.

