# Blockchain-Practicals
## Question 1
Create a voting system with multiple candidates. Each address can vote only once.
## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract VotingSystem {
    struct Candidate {
        string name;
        uint voteCount;
    }

    mapping(address => bool) public hasVoted;
    Candidate[] public candidates;

    constructor(string[] memory candidateNames) {
        for (uint i = 0; i < candidateNames.length; i++) {
            candidates.push(Candidate(candidateNames[i], 0));
        }
    }

    function vote(uint candidateIndex) public {
        require(!hasVoted[msg.sender], "Already voted");
        require(candidateIndex < candidates.length, "Invalid candidate");

        hasVoted[msg.sender] = true;
        candidates[candidateIndex].voteCount++;
    }

    function getCandidate(uint index) public view returns (string memory, uint) {
        require(index < candidates.length, "Invalid candidate");
        Candidate storage candidate = candidates[index];
        return (candidate.name, candidate.voteCount);
    }

    function getTotalCandidates() public view returns (uint) {
        return candidates.length;
    }
}
```
## Deployment
![Screenshot 2025-05-19 135728](https://github.com/user-attachments/assets/d61eefd1-91c7-42ca-b3c7-dfe171e19c1e)
## Interaction with contract
![Screenshot 2025-05-19 142322](https://github.com/user-attachments/assets/5c1eb904-baa3-4e52-9f85-6d48ae0c53e6)


## Question 2
Write a contract that manages a list of student records (name, roll number). Allow adding and retrieving student data.
## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract StudentRecords {
    struct Student {
        string name;
        uint rollNumber;
    }

    Student[] public students;

    function addStudent(string memory name, uint rollNumber) public {
        students.push(Student(name, rollNumber));
    }

    function getStudent(uint index) public view returns (string memory, uint) {
        require(index < students.length, "Invalid index");
        Student storage student = students[index];
        return (student.name, student.rollNumber);
    }

    function getTotalStudents() public view returns (uint) {
        return students.length;
    }
}
```
## Deployment and Interaction with contract
![Screenshot 2025-05-19 142753](https://github.com/user-attachments/assets/dc25f532-6d26-43ea-8238-9c3e996ed7ad)
## Question 3
Develop a contract that only allows the deployer (owner) to call a specific function (use modifiers).
## Code
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract OwnerOnly {
    address public owner;

    constructor() {
        owner = msg.sender;
    }

    modifier onlyOwner() {
        require(msg.sender == owner, "Not the owner");
        _;
    }

    function ownerFunction() public onlyOwner {
        // Function logic for owner only
    }
}
```
## Deployment and interaction with the contract
![Screenshot 2025-05-19 143610](https://github.com/user-attachments/assets/e7075e24-31d8-49c1-8cf9-2ca06b3a3839)

## Question 4



