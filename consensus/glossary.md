# Ethereum Consensus Glossary

This glossary covers the main concepts and terminology related to Ethereum's consensus mechanism, which operates on a Proof of Stake (PoS) system called Gasper.

## Core Consensus Concepts

### **Consensus**
The process by which all participants in the Ethereum network agree on the current state of the blockchain. Ethereum uses a Proof of Stake consensus mechanism to achieve this agreement.

### **Proof of Stake (PoS)**
A consensus mechanism where validators are selected to create and validate blocks based on the amount of cryptocurrency they have "staked" (locked up) as collateral. This replaces the energy-intensive Proof of Work system.

### **Gasper**
Ethereum's consensus protocol that combines Casper FFG (Friendly Finality Gadget) with LMD-GHOST (Latest Message Driven Greedy Heaviest Observed Subtree). It provides both liveness (blocks keep being produced) and safety (finality).

## Beacon Chain Components

### **Beacon Chain**
The central coordination layer of Ethereum's PoS system. It manages validators, coordinates consensus, and handles the overall network state. It operates alongside the execution layer but is separate from it.

### **Execution Client**
The component responsible for executing transactions and smart contracts. It processes the actual business logic of the Ethereum network and maintains the execution state.

### **Execution Payload**
The part of a beacon block that contains the execution layer data, including transactions, state changes, and other execution-related information.

## Time and Structure

### **Slot**
A 12-second time period during which one validator is selected to propose a block. Each slot can contain at most one block.

### **Epoch**
A period of 32 slots (approximately 6.4 minutes). Epochs are used for validator set updates, reward calculations, and finality decisions.

### **Checkpoint**
The first slot of each epoch. Checkpoints are special slots used for finality calculations and validator set management.

## Validators and Participation

### **Validator**
A participant in the PoS network who has staked 32 ETH and participates in block proposal and attestation. Validators are responsible for maintaining network security and consensus.

### **Proposer**
A validator selected to create a block during a specific slot. Only one proposer is selected per slot using the RANDAO algorithm.

### **Committee**
A group of validators assigned to attest to blocks during a specific slot. Committees are randomly selected and rotated to ensure security.

### **Attestation**
A vote by validators indicating their support for a specific block. Attestations are aggregated and used to determine the canonical chain and achieve finality.

## Consensus Algorithms

### **Casper FFG (Friendly Finality Gadget)**
A finality gadget that provides economic finality to blocks. It ensures that once a block is finalized, it cannot be reverted without validators losing their stake.

### **LMD-GHOST (Latest Message Driven Greedy Heaviest Observed Subtree)**
A fork choice rule that determines which chain is the canonical one. It considers the latest attestation from each validator and chooses the chain with the most attestations.

### **RANDAO**
A randomness beacon used to select block proposers and committee members. It uses a commit-reveal scheme where validators contribute randomness to create unpredictable selections.

## Finality and Security

### **Finality**
The property that once a block is finalized, it cannot be reverted without validators losing their stake. Finality provides strong guarantees about transaction permanence.

### **Justification**
A block is justified when it receives attestations from more than 2/3 of the total stake. Justified blocks are candidates for finalization.

### **Fork Choice Rule**
The algorithm that determines which chain is the canonical one when there are multiple competing chains. LMD-GHOST is Ethereum's fork choice rule.

## Rewards and Penalties

### **Stake**
The 32 ETH that each validator must deposit to participate in the consensus mechanism. Stake can be slashed for malicious behavior.

### **Rewards**
Incentives given to validators for participating in consensus, including block proposal rewards, attestation rewards, and sync committee rewards.

### **Slashing**
A severe penalty where a validator loses a portion or all of their stake for engaging in malicious behavior, such as double voting or proposing invalid blocks.

## Network Communication

### **Mempool**
A pool of pending transactions waiting to be included in a block. Proposers select transactions from the mempool when building blocks.

### **Network**
The peer-to-peer network that allows validators to communicate and share blocks, attestations, and other consensus messages.

## Block Production Process

### **Block Proposal**
The process where a selected proposer creates a new block containing transactions and other data, then broadcasts it to the network.

### **Block Validation**
The process where validators verify that a proposed block is valid according to the consensus rules before attesting to it.

### **Block Finalization**
The process where a block becomes permanently part of the canonical chain and cannot be reverted without severe economic penalties.

## State Management

### **State Root**
A cryptographic hash representing the current state of all accounts, contracts, and data on the Ethereum network.

### **Receipts Root**
A cryptographic hash of all transaction receipts in a block, providing proof of transaction execution and gas usage.

---

*This glossary covers the fundamental concepts of Ethereum's consensus mechanism. For more detailed technical specifications, refer to the Ethereum Yellow Paper and consensus specifications.*
