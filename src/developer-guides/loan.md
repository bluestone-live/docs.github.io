# Loan

Borrow ERC20 tokens or ETH from the protocol with specified amount and term. We also need to supply collateral tokens into the protocol so that this borrow meets the **minimum collateral covearage ratio**, which can be calculated by:

```
(collateralAmount * collateralTokenPrice) / (loanAmount * loanTokenPrice)
```

For example, to borrow `100` DAI using `300` USDC as collateral, assuming both token prices are equal to `$1` and the minimum collateral coverage ratio requirement is `150%`:

```
(300 * 1) / (100 * 1) = 300%
```

Since `300% >= 150%`, this is a valid collateral coverage ratio.

## Solidity Function

```solidity
function loan(
    address loanTokenAddress,
    address collateralTokenAddress,
    uint256 loanAmount,
    uint256 collateralAmount,
    uint256 loanTerm,
    address payable distributorAddress
) external payable returns (bytes32 loanId);
```

## Borrow using ERC20 tokens as collateral

As an example, we will borrow `100` [DAI](https://etherscan.io/token/0x6b175474e89094c44da98b954eedeac495271d0f) on `30-day` term and supply `300` [USDC](https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48) as collateral:

```javascript
const loanTokenAddress = '0x6b175474e89094c44da98b954eedeac495271d0f'
const collateralTokenAddress = '0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48'
const loanAmount = '100000000000000000000' // 100 DAI (18 decimals)
const collateralAmount = '300000000' // 300 USDC (6 decimals)
const loanTerm = 30
const myAccountAddress = '0x...'
const distributorAddress = myAccountAddress

const receipt = await protocol.methods
  .loan(
    loanTokenAddress,
    collateralTokenAddress,
    loanAmount,
    collateralAmount,
    loanTerm,
    distributorAddress,
  )
  .send({
    from: myAccountAddress,
  })


console.log(receipt)
```

## Borrow using ETH as collateral

Because ETH is currently not ERC20-compatible, we will use `address(1)` as an identifier address for ETH, just so the contract can distinguish it from ERC20 tokens.

As an example, we will borrow `100` [DAI](https://etherscan.io/token/0x6b175474e89094c44da98b954eedeac495271d0f) on `30-day` term and supply `1` ether as collateral:

```javascript
const loanTokenAddress = '0x6b175474e89094c44da98b954eedeac495271d0f'
const collateralTokenAddress = '0x0000000000000000000000000000000000000001'
const loanAmount = '100000000000000000000' // 100 DAI (18 decimals)
const collateralAmount = '1000000000000000000' // 1 ether in wei
const loanTerm = 30
const myAccountAddress = '0x...'
const distributorAddress = myAccountAddress

const receipt = await protocol.methods
  .loan(
    loanTokenAddress,
    collateralTokenAddress,
    loanAmount,
    collateralAmount,
    loanTerm,
    distributorAddress,
  )
  .send({
    from: myAccountAddress,
    value: collateralAmount, // REQUIRED
  })


console.log(receipt)
```
