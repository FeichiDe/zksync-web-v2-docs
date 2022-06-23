# Understanding system contracts

In order to keep the zero-knowledge circuits as simple as possible and enable simple extensions, a large chunk of the logic of zkSync was moved to the so called "system contracts" -- a set of contracts that have special priviliges and serve special purposes, e.g. deployment of contracts, making sure that the user pays only once for publishing contracts' calldata, etc.

Until the code for the system contracts has gone thorough testing, the code for all the system contracts will not be public. This section will only provide you with the knowledge needed to build on zkSync.

## Interfaces

The addresses and the interfaces of the system contracts can be found [here](https://github.com/matter-labs/v2-testnet-contracts/blob/main/l2/system-contracts/Constants.sol).

This section will describe semantic meaning of some of the most popular system contracts.

## ContractDeployer

[Interface](https://github.com/matter-labs/v2-testnet-contracts/blob/6a93ff85d33dfff0008624eb9777d5a07a26c55d/l2/system-contracts/interfaces/IContractDeployer.sol#L5)

This contract is used to deploy new smart contracts. Its job is to make sure that the bytecode for each deployed contract is known. This contract also defined the derivation address. Whenever a contract is deployed it emits the `ContractDeployed` event.

In the future, we will add the description on how to interact directly with this contract.

## IL1Messenger

[Interface](https://github.com/matter-labs/v2-testnet-contracts/blob/6a93ff85d33dfff0008624eb9777d5a07a26c55d/l2/system-contracts/interfaces/IL1Messenger.sol#L5)

This contract is used to send messages from zkSync to Ethereum L1. For each message sent the `L1MessageSent` event is emitted.

## INonceHolder

[Interface](https://github.com/matter-labs/v2-testnet-contracts/blob/6a93ff85d33dfff0008624eb9777d5a07a26c55d/l2/system-contracts/interfaces/INonceHolder.sol#L5).

This contract stores nonces for the accounts. The nonces for the accounts are stored in a centralized place for efficiency ([the tx nonce and the deployment nonce](./contracts.md#differences-in-create-behaviour) are stored in a single place) and also for the ease of the operator.