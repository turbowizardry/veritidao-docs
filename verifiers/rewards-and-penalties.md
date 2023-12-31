# Rewards and penalties

As a VeritiDAO verifier, your interactions are incentivized through a system of rewards and penalties. This system is managed by the `RewardsDistributor` smart contract.

**Rewards** are accrued when you participate in the voting process and your votes align with the consensus. These rewards come from the fees collected by the VeritiDAO protocol.

**Penalties** are incurred when your votes do not align with the consensus. This mechanism serves to discourage incorrect or malicious voting. The penalty amounts are subtracted from your rewards or staked Ethereum.

The `deposit` function is called to stake Ethereum, and the `claim` function is used to claim your rewards. The `withdraw` function allows you to withdraw your stake and rewards after a certain lock period. This lock period is initially set to 7 days after your last vote but can be updated by the contract owner.

The `addBalance` function updates the rewards and penalties for a staker, while the `claim` and `withdraw` functions handle the distribution of rewards and the imposition of penalties.

In the event of a penalty, the deducted amount is sent to the protocol revenue address. This ensures that the protocol continues to generate revenue, even in cases of incorrect voting.

### Fee calculation

The rewards and penalties for VeritiDAO verifiers are calculated based on the voting results for each listing, as described in the `calculateYesFee` and `calculateNoFee` functions in the `ListingsManager` contract.

These calculations ensure that the distribution of fees is proportional to the number of votes, which incentivizes verifiers to actively participate in the voting process.

When a listing's voting concludes, the reward and penalty distribution are determined by the outcome of the vote. If the listing is verified, meaning that the majority of votes are "yes", the amounts for the rewards and penalties are calculated from the `calculateYesFee` function. This means that those who voted correctly (in this case, "yes") receive a reward, while those who voted incorrectly ("no") incur a penalty.

Conversely, if the listing is defeated, the roles are reversed and the amount used is calculated from the `calculateNoFee` function. The "no" votes form the reward, and the "yes" votes incur a penalty. This system ensures that verifiers are motivated to vote accurately, as their rewards and penalties are directly tied to the outcome of their votes.

#### Example fee distribution for a verified listing

<table><thead><tr><th width="187"></th><th width="172.33333333333331">Number of voters</th><th>Fee</th></tr></thead><tbody><tr><td>Yes votes</td><td>424</td><td>Reward: 0.0057 ETH per voter (2.4 ETH / 424)</td></tr><tr><td>No votes</td><td>76</td><td>Penalty: 0.0057 ETH per voter</td></tr></tbody></table>

Participating as a verifier in VeritiDAO thus involves an element of risk. It's important to make well-informed decisions when voting to maximize rewards and minimize penalties.
