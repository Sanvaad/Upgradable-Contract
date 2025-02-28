# Box Upgradeable Contracts

## Overview
This repository contains Solidity smart contracts implementing an upgradeable storage pattern using the UUPS (Universal Upgradeable Proxy Standard) model. The contracts are built using OpenZeppelin's upgradeable library.

## Contracts

### BoxV1
- Implements an upgradeable storage contract with a single `value` variable.
- Includes a `getValue` function to retrieve the stored value.
- Implements `UUPSUpgradeable` and `OwnableUpgradeable` for secure upgrades.

### BoxV2
- Extends `BoxV1` by adding a `setValue` function to modify the stored value.
- Maintains the upgradeability structure for seamless transitions.

### Delegatecall Example (A & B)
- Demonstrates the use of `delegatecall` in Solidity.
- Contract **B** has a function `setVars` that modifies its state.
- Contract **A** calls **B** using `delegatecall`, modifying **A's** state instead.
- Highlights the importance of storage layout consistency between contracts.

### SmallProxy
- A minimalistic proxy contract implementing **EIP-1967** storage slot for upgradeability.
- Uses inline assembly to manage contract storage and upgrades.
- Provides helper functions to encode transactions and read storage.

### ImplementationA & ImplementationB
- Two implementation contracts for testing proxy upgrades.
- **ImplementationA** directly updates the `value`.
- **ImplementationB** modifies the `value` with an additional increment of `2`.

## How to Use

### Deploying Upgradeable Contracts
1. Deploy `BoxV1` using an upgradeable proxy factory (e.g., OpenZeppelin's Upgrades plugin).
2. Upgrade the proxy to `BoxV2` when needed, preserving storage and adding new functionality.

### Deploying Delegatecall Example
1. Deploy contract **B**.
2. Deploy contract **A** and call `setVars(address_of_B, value)`.
3. Observe that contract **A** modifies its storage, not **B**.

### Using the Proxy Contract
1. Deploy `SmallProxy`.
2. Deploy an implementation contract (`ImplementationA` or `ImplementationB`).
3. Use `setImplementation(address)` in `SmallProxy` to point to an implementation.
4. Interact with `SmallProxy` as if it were the implementation contract.

## References
- OpenZeppelin Upgradeable Contracts: https://docs.openzeppelin.com/contracts-upgradeable/
- Solidity Delegatecall Example: https://solidity-by-example.org/delegatecall
- EIP-1967 Proxy Standard: https://eips.ethereum.org/EIPS/eip-1967

## License
This project is licensed under the MIT License.
