# Deposit

Deposit ERC20 tokens or ETH into the protocol with specified amount and term.

## Solidity Function

```solidity
function deposit(
    address tokenAddress,
    uint256 depositAmount,
    uint256 depositTerm,
    address payable distributorAddress
) external payable returns (bytes32 depositId);
```

## Deposit ERC20 tokens

As an example, we will deposit `100` [DAI](https://etherscan.io/token/0x6b175474e89094c44da98b954eedeac495271d0f) on `30-day` term:

```javascript
const tokenAddress = '0x6b175474e89094c44da98b954eedeac495271d0f'
const depositAmount = '100000000000000000000' // 100 DAI in 18 decimals
const depositTerm = 30
const myAccountAddress = '0x...'
const distributorAddress = myAccountAddress

const receipt = await protocol.methods
  .deposit(
    tokenAddress,
    depositAmount,
    depositTerm,
    distributorAddress,
  )
  .send({
    from: myAccountAddress,
  })


console.log(receipt)
```

## Deposit ETH

Because ETH is currently not ERC20-compatible, we will use `address(1)` as an identifier address for ETH, just so the contract can distinguish it from ERC20 tokens.

Similarly, we will deposit `1` ether on `30-day` term:

```javascript
const tokenAddress = '0x0000000000000000000000000000000000000001'
const depositAmount = '1000000000000000000' // 1 ether in wei
const depositTerm = 30
const myAccountAddress = '0x...'
const distributorAddress = myAccountAddress

const receipt = await protocol.methods
  .deposit(
    tokenAddress,
    depositAmount,
    depositTerm,
    distributorAddress,
  )
  .send({
    from: myAccountAddress,
    value: depositAmount // REQUIRED
  })

console.log(receipt)
```
