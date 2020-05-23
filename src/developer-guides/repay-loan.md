# Repay Loan

Repay a loan with specified amount and get previously supplied collateral tokens back.

## Solidity Function

```solidity
function repayLoan(bytes32 loanId, uint256 repayAmount)
    external
    payable
    returns (uint256 remainingDebt);
```

## Get remaining debt

Before we repay our loan, it is a good idea to understand how many tokens plus interest we owe:

```javascript
const loanId = '...'

const { remainingDebt } = await protocol.methods
  .getLoanRecordById(loanId)
  .call()

console.log(remainingDebt)
```

## Repay with ERC20 tokens

Suppose we have borrowed `100` DAI and now we want to repay the full amount (with interest):

```javascript
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .repayLoan(
    loanId,
    remainingDebt,
  )
  .send({
    from: myAccountAddress,
  })

console.log(receipt)
```

## Repay with ethers

Suppose we have borrowed `1` ether and now we want to repay the full amount (with interest):

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

## Partial repay

To do a partial repay, simply use a repay amount smaller than `remainingDebt`.
