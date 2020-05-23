# Withdraw Deposit

Withdraw previously deposited tokens from the protocol.

## Solidity Function

```solidity
function withdraw(bytes32 depositId)
  external
  returns (uint256 withdrewAmount);
```


```solidity
function earlyWithdraw(bytes32 depositId)
  external
  returns (uint256 withdrewAmount);
```

## Withdraw

Withdraw matured deposit will return original deposit plus accrued interest:

```javascript
const depositId = '...'
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .withdraw(
    depositId,
  )
  .send({
    from: myAccountAddress,
  })

console.log(receipt)
```

## Early Withdraw

Withdraw inmature deposit will only return original deposit without interest:

```javascript
const depositId = '...'
const myAccountAddress = '0x...'

const receipt = await protocol.methods
  .earlyWithdraw(
    depositId,
  )
  .send({
    from: myAccountAddress,
  })

console.log(receipt)
```
