# Smart Contracts with Solidity

![smart_contract](Images/smart_contracts.jpg)

*Source:https://www.forbes.com/sites/samantharadocchia/2018/09/07/why-smart-contracts-standards-are-essential-for-large-scale-adoption/?sh=1b3320c01211*

## Background

In this assignment, smart contracts were created using Solidity for the Ethereum-compatible blockchain to automate profit splitting for a new startup.

These `ProfitSplitter` contracts will do the following:

* Pay associate-level employees quickly and easily.

* Distribute profits to different tiers of employees.

* Distribute company shares for employees in a "deferred equity incentive plan" automatically.

## Associate Profit Splitter Contract

This contract will accept ether, and divide it evenly among associate-level employees. This will allow the human resources department to pay employees quickly and efficiently.

### Contract Summary

* Public payable variables were defined for three associate-level employees.

* A `balance` function is created to check current balance of the contract and make sure that with an even split between beneficiaries, this function will return a 0.

* A public payable `deposit` function is created to split the amount of profit evenly between the three employees. As Solidity does not support float/decimals the remainder wei after the split will be transferred back to the message sender/human resources.

* An external payable fallback function is created to ensure that the deposit function is executed if ether is sent directly to the contract. 

Contract Code in Solidity:

[`Associate Profit Splitter`](associateprofitsplitter.txt)

Test in Local Network:

![`Associate Profit Splitter`](Images/associate_split-test.JPG)


## Tiered Profit Splitter Contract

This contract is built to distribute different percentages of incoming ether to employees at different tiers/levels. The CEO gets paid 60%, CTO 25%, and Bob gets 15% of the profits.

### Contract Summary

* The contract calculates the percentage profit split between the CEO, CTO and Bob (three tiers of employees).

* The message value is converted to points/units by dividing by 100 and then multiplying the points with the number representing the percentage eg. `msg.value / 100` to get `points` and then `points * 60` will give the output for 60%.

* The amounts are distributed to employees based on their share of profit and also keeping a running total of the message value to keep track of how much is distributed.

Contract Code in Solidity:

[`Tiered Profit Splitter`](tieredprofitsplitter.txt)

Test in Local Network:

![`Tiered Profit Splitter`](Images/tier_split_test.JPG)

## Deferred Equity Plan Contract

This contract models traditional company stock plans. The contract will automatically manage 1000 shares, with an annual distribution of 250 shares over four years for a single employee.

### Contract Summary

* Human resources will be the message sender.

* The `total shares` to be distributed are `1000` with a `four-year` vesting period. 

* The employee will receive `250 shares` annually this value is set by manually dividing total shares by 4 because calculating this in Solidity is expensive.

* Time is set to `now` and the value will unlock after `365 days` from now.

* An `if` statement is added to ensure that if the employee does not cash out until 5+ years after the contract start, the contract does not reward more than the `total_shares` agreed upon in the contract.

Contract Code in Solidity:

[`Deferred Equity Plan`](deferredequityplan.txt)

Test in Local Network using a 'fastforward' function:

![`Deferred Equity Plan`](Images/deferred_equity_test.JPG)

## Deployment of Contracts in Kovan Testnet

1. **Associate Profit Splitter Contract**

Contract deployed in Kovan:

![`Associate Profit Splitter`](Images/associate_split_kovan.JPG)

Contract Address:

`0x2a87EB2707862B70bD0Eba4E04736eE74ba688F1`

Transaction Details in Etherscan:

![`Associate Profit Splitter`](Images/associate_split.JPG)

2. **Tiered Profit Splitter Contract**

Contract deployed in Kovan:

![`Tiered Profit Splitter`](Images/tier_split_kovan.JPG)

Contract Address:

`0xbbBE061dDfA205b1302AfE26B1d2ee0406e5cf9e`

Transaction Details in Etherscan:

![`Tiered Profit Splitter`](Images/tier_split.JPG)

3. **Deferred Equity Plan Contract**

Contract deployed in Kovan:

![`Deferred Equity Plan`](Images/deferredequity_kovan.JPG)

Contract Address:

`0x560113A92d2A78894995e4b0a8174825151CA21f`

There is no distribution of shares as the contract will come into effect `365 days` from `now`.

