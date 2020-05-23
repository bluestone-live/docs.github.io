# Liquidate Loan

When a loan record is defaulted, i.e., loaner did not repay on time, or is under minimum collateral coverage ratio, this loan record can be liquidated by anyone who wishes to repay on loaner's behalf and, as a reward, the liquidator will get equal value of loaner's collateral tokens in discount.

## Solidity Function

```solidity
function liquidateLoan(bytes32 loanId, uint256 liquidateAmount)
    external
    payable
    returns (uint256 remainingCollateral, uint256 liquidatedAmount);
```

## Get liquidatable loan records

Obviously, the first step is to get loan records that are liquidatable. Currently, there is no straightforward way to get a list of liqudiatable records on chain, but it is certainly possible. Here is a high-level overview of how to achieve this:

- Get and/or listen to `LoanSucceed` events with the help of [web3 events](https://web3js.readthedocs.io/en/v1.2.8/web3-eth-contract.html#events).
- Collect a list of `loanId`s from those events.
- Check if a specific loan record is liquidatable using `protocol.methods.getLoanRecordById(loanId).call()`. The response will include necessary information so you can do some math to figure out whether it's liquidatable.

This indeed sounds troublesome, but we will open source our liquidation bot service, which is much easier to work with, once it gets stabilized. So stay in tuned.

## Get remaining debt

Before we liquidate a loan, it is a good idea to understand how many tokens plus interest loaner owes:

```javascript
const loanId = '...'

const { remainingDebt } = await protocol.methods
  .getLoanRecordById(loanId)
  .call()

console.log(remainingDebt)
```

## Liquidate ERC20 tokens

Suppose Bob have borrowed `100` DAI but he defaulted, so now we want to liquidate his loan record:

```javascript
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .liquidateLoan(
    loanId,
    remainingDebt,
  )
  .send({
    from: myAccountAddress,
  })

console.log(receipt)
```

## Liquidate with ethers

Suppose Bob have borrowed `1` ether but he defaulted, so now we want to liquidate his loan record:

```javascript
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .repayLoan(
    loanId,
    remainingDebt,
  )
  .send({
    from: myAccountAddress,
    value: remainingDebt,
  })

console.log(receipt)
```

## Partial liquidation

To do a partial liquidation, simply use a liquidate amount smaller than `remainingDebt`.
