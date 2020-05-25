# Withdraw Collateral

Withdraw the specified amount of collateral tokens from a given loan record. This will decrease the collateral coverage ratio of the loan record.

## Solidity Function

```solidity
function subtractCollateral(bytes32 loanId, uint256 collateralAmount)
    external
    payable
    returns (uint256 totalCollateralAmount);
```

- `totalCollateralAmount`: The total collateral amount after collateral tokens are added.

## Withdraw ERC20 or ether collateral

Suppose we have borrowed some tokens using DAI as collateral and now we want to withdraw `100` DAI as collateral tokens:

```javascript
const loanId = '...'
const collateralAmount = '100000000000000000000' // 100 DAI (18 decimals)
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .subtractCollateral(
    loanId,
    collateralAmount,
  )
  .send({
    from: myAccountAddress,
  })

console.log(receipt)
```
