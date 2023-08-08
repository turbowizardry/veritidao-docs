# Rewards and penalties

As a VeritiDAO verifier, your interactions are incentivized through a system of rewards and penalties. This system is managed by the `RewardsDistributor` smart contract.

**Rewards** are accrued when you participate in the voting process and your votes align with the consensus. These rewards come from the fees collected by the VeritiDAO protocol.

**Penalties** are incurred when your votes do not align with the consensus. This mechanism serves to discourage incorrect or malicious voting. The penalty amounts are subtracted from your rewards or staked Ethereum.

The `deposit` function is called to stake Ethereum, and the `claim` function is used to claim your rewards. The `withdraw` function allows you to withdraw your stake and rewards after a certain lock period. This lock period is initially set to 7 days after your last vote but can be updated by the contract owner.

The `addBalance` function updates the rewards and penalties for a staker, while the `claim` and `withdraw` functions handle the distribution of rewards and the imposition of penalties.

In the event of a penalty, the deducted amount is sent to the protocol revenue address. This ensures that the protocol continues to generate revenue, even in cases of incorrect voting.

### Fee calculation

The rewards and penalties for VeritiDAO verifiers are calculated based on the voting results for each listing, as described in the `calculateYesFee` and `calculateNoFee` functions in the `ListingsManager` contract.

**Yes Votes Fee Calculation**: The `calculateYesFee` function is used to determine the fee to distribute for "yes" votes. If there are "yes" votes for a particular listing, the fee for each "yes" vote is calculated. This is done by dividing the verifier fee for the listing by the total number of "yes" votes. If there are no "yes" votes, the function returns zero.

**No Votes Fee Calculation**: The `calculateNoFee` function is used to calculate the fee to distribute for "no" votes. If there are "no" votes for a particular listing, the fee for each "no" vote is calculated. This is done by dividing the verifier fee for the listing by the total number of "no" votes. If there are no "no" votes, the function returns zero.

#### Example fee distribution for a verified listing

<table><thead><tr><th width="187"></th><th width="172.33333333333331">Number of voters</th><th>Fee</th></tr></thead><tbody><tr><td>Yes votes</td><td>424</td><td>Reward: 0.0057 ETH per voter</td></tr><tr><td>No votes</td><td>76</td><td>Penalty: 0.032 ETH per voter</td></tr></tbody></table>

These calculations ensure that the distribution of fees is proportional to the number of votes, which incentivizes verifiers to actively participate in the voting process.

When a listing's voting concludes, the reward and penalty distribution are determined by the outcome of the vote. If the listing is verified, meaning that the majority of votes are "yes", the "yes" votes constitute the reward and the "no" votes form the penalty. This means that those who voted correctly (in this case, "yes") receive a reward, while those who voted incorrectly ("no") incur a penalty. Conversely, if the listing is defeated, the roles are reversed. The "no" votes form the reward, and the "yes" votes incur a penalty. This system ensures that verifiers are motivated to vote accurately, as their rewards and penalties are directly tied to the outcome of their votes.

Participating as a verifier in VeritiDAO thus involves an element of risk. It's important to make well-informed decisions when voting to maximize rewards and minimize penalties.
