# Rewards and penalties

As a VeritiDAO verifier, your interactions are incentivized through a system of rewards and penalties. This system is managed by the `RewardsDistributor` smart contract.

**Rewards** are accrued when you participate in the voting process and your votes align with the consensus. These rewards come from the fees collected by the VeritiDAO protocol.

**Penalties** are incurred when your votes do not align with the consensus. This mechanism serves to discourage incorrect or malicious voting. The penalty amounts are subtracted from your rewards or staked Ethereum.

The `deposit` function is called to stake Ethereum, and the `claim` function is used to claim your rewards. The `withdraw` function allows you to withdraw your stake and rewards after a certain lock period. This lock period is initially set to 7 days after your last vote but can be updated by the contract owner.

The `addBalance` function updates the rewards and penalties for a staker, while the `claim` and `withdraw` functions handle the distribution of rewards and the imposition of penalties.

In the event of a penalty, the deducted amount is sent to the protocol revenue address. This ensures that the protocol continues to generate revenue, even in cases of incorrect voting.

Participating as a verifier in VeritiDAO thus involves an element of risk. It's important to make well-informed decisions when voting to maximize rewards and minimize penalties.
