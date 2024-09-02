Here's a comprehensive and engaging README file for your project:

---

# Decentralized Stable Coin System (DSC System)

## Overview

Welcome to the Decentralized Stable Coin System (DSC System), a robust and innovative smart contract project designed to maintain a stable 1:1 peg with the US Dollar. This system is fully decentralized, algorithmically stable, and collateralized with exogenous assets like Ethereum (ETH) and Bitcoin (BTC). The project is inspired by the MakerDAO DSS system but simplified, with no governance or fees, focusing solely on maintaining stability and over-collateralization.

### Key Features

- **Exogenously Collateralized**: The system uses ETH and BTC as collateral to mint and back the stablecoin.
- **Algorithmically Stable**: Ensures that the stablecoin maintains a 1:1 peg with the US Dollar through an algorithmic approach.
- **Decentralized & Permissionless**: Anyone can interact with the system without needing permission or central authority.
- **Over-Collateralization**: The system is designed to be always over-collateralized to protect the stability and value of the stablecoin.

## Project Structure

The project is organized as follows:

### 1. Contracts

- **DecentralizedStableCoin.sol**: Implements the core ERC20 stablecoin that can be minted and burned by the `DSCEngine` contract.
- **DSCEngine.sol**: The heart of the system that manages collateral deposits, minting, and redeeming of the stablecoin, along with liquidation mechanisms to maintain system stability.
- **OracleLib.sol**: A library for interacting with Chainlink price feeds to fetch real-time collateral prices.
- **HelperConfig.sol**: Provides configuration for different network environments, including mock setups for testing.

### 2. Scripts

- **DeployDSC.s.sol**: Script for deploying the `DecentralizedStableCoin` and `DSCEngine` contracts, setting up initial configurations.
- **HelperConfig.s.sol**: Provides network-specific configurations, including mock deployments for local testing.

### 3. Tests

- **DSCEngineTest.sol**: Comprehensive tests for the `DSCEngine` contract, covering scenarios such as collateral deposits, minting, redeeming, and liquidation processes.

## How It Works

### 1. Collateral Deposit and Minting

Users can deposit collateral (ETH or BTC) into the system to mint the stablecoin (`DSC`). The amount of stablecoin minted is determined by the value of the collateral and the system's over-collateralization requirements.

### 2. Redeeming and Burning

Users can redeem their collateral by burning the stablecoin. The system ensures that the user's health factor (collateralization ratio) remains within acceptable limits.

### 3. Liquidation

If a user's health factor falls below the minimum threshold, the system allows other users (liquidators) to liquidate the under-collateralized position. Liquidators cover the debt by burning the stablecoin and receive the collateral at a discount.

## Installation and Setup

### Prerequisites

- **Node.js and npm**: Ensure you have Node.js installed.
- **Foundry**: Install Foundry for smart contract development and testing.
- **Chainlink Node**: For price feed aggregation (optional for deployment).

### Steps

1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/dsc-system.git
   cd dsc-system
   ```

2. **Install Dependencies**
   ```bash
   forge install
   ```

3. **Run Tests**
   ```bash
   forge test
   ```

4. **Deploy Contracts**
   Deploy to your preferred network using the provided deployment script.
   ```bash
   forge script script/DeployDSC.s.sol:DeployDSC --broadcast --verify -vvvv
   ```

## Usage

### Interacting with the Contracts

Once deployed, you can interact with the DSC system via the following functions:

- **Deposit Collateral**: `depositCollateral(address tokenCollateralAddress, uint256 amountCollateral)`
- **Mint DSC**: `mintDsc(uint256 amountDscToMint)`
- **Redeem Collateral**: `redeemCollateral(address tokenCollateralAddress, uint256 amountCollateral)`
- **Burn DSC**: `burnDsc(uint256 amount)`

### Liquidation Process

If a user's health factor drops below 1, the position becomes eligible for liquidation. Liquidators can use the `liquidate` function to cover the debt and receive collateral at a discount.

## Acknowledgments

- **OpenZeppelin**: For providing the secure and battle-tested libraries.
- **Chainlink**: For the reliable price feeds used in the system.
- **Forge**: For the powerful smart contract development toolkit.
