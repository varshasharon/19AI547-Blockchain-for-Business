# Experiment 1: Decentralized Certificate Verification
## Aim:
  To develop a smart contract for issuing and verifying academic certificates on Ethereum, preventing forgery and ensuring authenticity.
## Algorithm:
1. Deploy a smart contract where universities can issue certificates.
2. Store a hash of certificate data on-chain.
3. Provide a verification function that checks certificate authenticity.
4. Users can verify the certificate by comparing the stored hash.
## Program:
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract CertificateVerification {
    address public university;  // University address

    // Mapping to store issued certificate hashes
    mapping(bytes32 => bool) public certificates;

    // Event emitted when a certificate is issued
    event CertificateIssued(bytes32 certHash);

    // Constructor sets the deployer (university)
    constructor() {
        university = msg.sender;
    }

    // Function to issue certificate (only university can call)
    function issueCertificate(string memory studentName, string memory degree, uint year) public {
        require(msg.sender == university, "Only university can issue certificates");

        // Create a unique hash of the certificate details
        bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));

        certificates[certHash] = true;
        emit CertificateIssued(certHash);
    }

    // Function to verify if a certificate exists
    function verifyCertificate(string memory studentName, string memory degree, uint year) public view returns (bool) {
        bytes32 certHash = keccak256(abi.encodePacked(studentName, degree, year));
        return certificates[certHash];
    }
}
```
# Output:
![Screenshot 2025-04-16 091554](https://github.com/user-attachments/assets/7f8e3ebf-a761-4f2b-870c-cac5209e74f8)
![Screenshot 2025-04-16 091654](https://github.com/user-attachments/assets/3c806cfb-3502-48f1-9b1a-a4885f391132)
![Screenshot 2025-04-16 091804](https://github.com/user-attachments/assets/0565a7b5-3672-43a6-8a32-afda11362c99)
![Screenshot 2025-04-16 091831](https://github.com/user-attachments/assets/b6b7633f-3df2-4798-b8cc-b9a902e83d4a)


# Result:
Thus the decentralized certificate verification using remix is successfully implemented.
