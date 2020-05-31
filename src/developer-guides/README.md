# Developer Guides

[web3.js](https://web3js.readthedocs.io) provides a set of JavaScript APIs to interact with smart contracts on Ethereum. Please make sure you have it setup before proceeding to interact with BlueStone smart contracts.

BlueStone offers one main contract [Protocol.sol](https://github.com/bluestone-live/bluestone/blob/master/contracts/protocol/interface/IProtocol.sol) that exposes all necessary external functions for the public to interact with. We will use [web3.eth.Contract](https://github.com/bluestone-live/bluestone/blob/master/contracts/protocol/interface/IProtocol.sol) to create our contract instance:

```javascript
const protocol = new web3.eth.Contract(jsonInterface, address)
```

Notice that it requires two arguments: `jsonInterface` and `address`. Their values can be found below:

- [Protocol ABI](../contracts/abi.md)
- [Contract Address](../contracts/address.md)

In the following sections, we will guide you through a number of core contract functions that we can interact with.
