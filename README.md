# ERC-20 Token Contract (Yul Implementation)

This repository contains a minimalistic implementation of an ERC-20 token contract using Yul. The contract includes basic ERC-20 functionalities such as transferring tokens, approving allowances, and querying balances. It also has a minting function restricted to the contract owner.

## Overview

The contract is written in Yul, an intermediate language for the Ethereum Virtual Machine (EVM). It leverages low-level operations to provide efficient and gas-optimized token functionality.

## Features

- **Token Transfers**: Transfer tokens to other addresses.
- **Allowance Mechanism**: Approve third-party addresses to transfer tokens on behalf of the token holder.
- **Minting**: Mint new tokens to any address, restricted to the contract owner.
- **Query Functions**: Check balances and allowances.
- **Event Emissions**: Emits standard ERC-20 events (`Transfer` and `Approval`).

## Functions

### balanceOf(address)

Returns the balance of the specified address.

- **Selector**: `0x70a08231`
- **Parameters**: `address` - the address to query the balance for.

### totalSupply()

Returns the total supply of the token.

- **Selector**: `0x18160ddd`
- **Parameters**: None

### transfer(address to, uint256 amount)

Transfers `amount` tokens to the specified `to` address.

- **Selector**: `0xa9059cbb`
- **Parameters**: 
  - `to` - the recipient address.
  - `amount` - the amount of tokens to transfer.

### transferFrom(address from, address to, uint256 amount)

Transfers `amount` tokens from the `from` address to the `to` address using the allowance mechanism.

- **Selector**: `0x23b872dd`
- **Parameters**: 
  - `from` - the address to transfer tokens from.
  - `to` - the recipient address.
  - `amount` - the amount of tokens to transfer.

### approve(address spender, uint256 amount)

Approves the `spender` address to spend `amount` tokens on behalf of the caller.

- **Selector**: `0x095ea7b3`
- **Parameters**: 
  - `spender` - the address allowed to spend tokens.
  - `amount` - the amount of tokens to be approved for spending.

### allowance(address owner, address spender)

Returns the remaining number of tokens that the `spender` will be allowed to spend on behalf of `owner`.

- **Selector**: `0xdd62ed3e`
- **Parameters**: 
  - `owner` - the address owning the tokens.
  - `spender` - the address allowed to spend tokens.

### mint(address account, uint256 amount)

Mints `amount` tokens to the `account` address. Only callable by the contract owner.

- **Selector**: `0x40c10f19`
- **Parameters**: 
  - `account` - the address to receive the minted tokens.
  - `amount` - the amount of tokens to mint.

## Deployment

To deploy the contract, use the following steps:

1. Compile the Yul code to bytecode.
2. Deploy the bytecode to the Ethereum network using a deployment tool (e.g., Remix, Hardhat, Truffle).

## Events

### Transfer

Emitted when tokens are transferred, including zero value transfers.

- **Signature**: `0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef`
- **Indexed Parameters**: 
  - `from` - address sending the tokens.
  - `to` - address receiving the tokens.
- **Non-Indexed Parameters**: 
  - `amount` - the amount of tokens transferred.

### Approval

Emitted when the allowance of a `spender` for an `owner` is set by a call to `approve`.

- **Signature**: `0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925`
- **Indexed Parameters**: 
  - `owner` - address that owns the tokens.
  - `spender` - address allowed to spend the tokens.
- **Non-Indexed Parameters**: 
  - `amount` - the amount of tokens approved.

## Storage Layout

- **Slot 0**: Contract owner address.
- **Slot 1**: Total supply of tokens.
- **Slot 0x1000 and above**: Token balances of addresses.
- **Keccak256 hash of account and spender addresses**: Allowances for each `owner`-`spender` pair.

## Security

- **Ownership**: The mint function is restricted to the contract owner.
- **Zero Address Checks**: Transfers to the zero address are disallowed.
- **Safe Arithmetic**: Uses safe addition and subtraction to prevent overflow and underflow.

## License

This project is licensed under the MIT License. See the LICENSE file for details.
