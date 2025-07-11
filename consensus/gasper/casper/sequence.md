# Understanding Casper FFG in Ethereum Consensus

This diagram illustrates the simplified flow of how Casper the Friendly Finality Gadget (FFG) contributes to Ethereum's Proof of Stake (PoS) consensus, focusing on the justification and finalization of blocks and epochs.

## Sequence Diagram

```mermaid
sequenceDiagram
    participant V as Validator
    participant BC as Beacon Chain (Consensus Layer)
    participant EL as Execution Layer

    Note over V,EL: Ethereum's Proof of Stake (PoS)
    Note over V,EL: Casper FFG provides finality on top

    V->>BC: 1. Stake 32 ETH (become active)
    BC-->>V: Validator assigned duties (proposer/attester)

    loop Every 12 seconds (Slot)
        BC->>V: Selects a Block Proposer
        V->>EL: Request pending transactions
        EL-->>V: Provides Execution Payload (transactions)
        V->>BC: 2. Propose new Block (includes attestations)
        BC->>V: Assigns Attesters (committee)
        V->>BC: 3. Attest to proposed Block (vote for head of chain)
    end

    Note over BC: Epochs (32 Slots) drive FFG
    Note over BC: Justification & Finalization happen on epoch boundaries

    loop Every Epoch (32 Slots)
        V->>BC: 4. Cast FFG Vote (source & target epoch boundary blocks)
        Note over BC: Votes aggregated by Beacon Chain
        alt If 2/3+ of staked ETH vote for target block
            BC->>BC: 5. Target Block becomes JUSTIFIED
            Note over BC: (First block of Epoch N+1 is justified)
            alt If previous Epoch N's first block was already JUSTIFIED
                BC->>BC: 6. Epoch N (and its first block) becomes FINALIZED
                Note over BC: Irreversible state achieved
            end
        else Else (no 2/3 supermajority)
            BC->>BC: Block remains un-justified
        end
    end

    Note over V,BC: Incentives: Rewards for honest participation
    Note over V,BC: Penalties: Slashing for malicious behavior (e.g., double finality vote)
```

## Explanation of Steps

### 1. Stake 32 ETH
To become a validator, an entity must stake 32 ETH on the Beacon Chain.

### 2. Propose new Block
A randomly selected validator proposes a new block, which includes transactions from the Execution Layer and attestations from other validators.

### 3. Attest to proposed Block
Other validators in assigned committees attest to the validity of the proposed block, effectively voting for it as the head of the chain.

### 4. Cast FFG Vote
At the end of each epoch, validators cast specific Casper FFG votes, targeting the first block of the current epoch (as the "target") and the last justified block they know (as the "source").

### 5. Target Block becomes JUSTIFIED
If a block receives votes from over 2/3 of the total staked ETH, it becomes "justified." This is a strong indication of agreement.

### 6. Epoch becomes FINALIZED
If a block (representing the start of an epoch) is justified, and the next epoch's starting block is also justified, then the first epoch (and all its blocks) becomes "finalized." This state is considered irreversible.

## Summary

Casper FFG, through this voting and justification mechanism, provides the strong "finality" guarantee that is crucial for the security and usability of the Ethereum network.