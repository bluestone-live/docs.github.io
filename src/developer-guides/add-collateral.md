# Add Collateral

Supply additional collateral tokens to a given loan record. This will increase the collateral coverage ratio of the loan record.

## Solidity Function

```solidity
function addCollateral(bytes32 loanId, uint256 collateralAmount)
    external
    payable
    returns (uint256 totalCollateralAmount);
```

- `totalCollateralAmount`: The total collateral amount after collateral tokens are added.

## Add ERC20 collateral

Suppose we have borrowed some tokens using DAI as collateral and now we want to supply additional `100` DAI as collateral tokens:

```javascript
const loanId = '...'
const collateralAmount = '100000000000000000000' // 100 DAI (18 decimals)
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .addCollateral(
    loanId,
    collateralAmount,
  )
  .send({
    from: myAccountAddress,
  })

console.log(receipt)
```

## Add ether collateral

Suppose we have borrowed some tokens using ethers as collateral and now we want to supply additional `1` ether as collateral:

```javascript
const loanId = '...'
const collateralAmount = '1000000000000000000' // 1 ether in wei
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .addCollateral(
    loanId,
    collateralAmount,
  )
  .send({
    from: myAccountAddress,
    value: collateralAmount,
  })

console.log(receipt)
```
