# Boba Profile NFT

Welcome to the Boba Profile NFT project! This project is designed to manage and interact with profile NFTs for the Toaster Finance platform on Boba Network.  
![image](https://github.com/user-attachments/assets/e02157ef-bb23-4270-81aa-c5d6df648651)


# Deployed Contracts

### Toaster Profiles

0x7272C28fEf7903704B9665530eb30d7c797Ff86d [View on Explorer](https://bobascan.com/address/0x7272C28fEf7903704B9665530eb30d7c797Ff86d/contract/288/code)

### Toaster Items

0x642C2c5BF941D5eb93C4935ee84e82A37428a27d [View on Explorer](https://blockexplorer.boba.network/address/0x642C2c5BF941D5eb93C4935ee84e82A37428a27d/contract/288/code)

## Table of Contents

- [Boba Profile NFT](#boba-profile-nft)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [System Architecture](#system-architecture)
  - [Features](#features)
  - [NFT Attributes](#nft-attributes)
  - [Item Details](#item-details)
  - [Installation](#installation)
  - [Test](#test)
  - [Deploy on local hardhat node](#deploy-on-local-hardhat-node)
  - [License](#license)

## Introduction

Toaster Items Contract is a collectible NFT system that allows users to create, manage, and customize their profile NFTs on the Toaster Finance platform. Each NFT represents a unique user profile that can be customized with various attributes based on their DeFi activities on Boba.

## System Architecture

The following diagram illustrates the interaction flow between different components of the system:

```mermaid
sequenceDiagram
    participant User
    participant Backend
    participant Contract
    participant ImageGenerator
    participant OpenSea

    Note over Backend: Action Completion
    Backend->>Backend: Action Verification
    Backend->>Backend: NFT Eligibility Check

    Note over User: NFT Minting Flow
    User->>Backend: Request Claimable Items
    Backend-->>User: Available Items List
    User->>Backend: Request Mint Signature
    Backend->>Backend: Generate Signature
    Backend-->>User: Mint Signature

    User->>Contract: mintBatch()
    Contract-->>User: NFTs Minted
    User->>Backend: Notify Mint Complete
    Backend->>Backend: Update NFT Status

    Note over User: Profile Creation
    User->>Contract: Mint Profile NFT
    Contract->>ImageGenerator: Mint Event Hook
    ImageGenerator->>ImageGenerator: Generate Profile Image
    ImageGenerator->>Backend: Profile Generation Complete
    Backend->>Backend: Update Profile Status

    Note over OpenSea: Metadata Resolution
    OpenSea->>Backend: Get Profile Metadata
    Backend-->>OpenSea: Profile Metadata
```

The system uses Alchemy Webhook for image generation, ensuring efficient and automated profile image creation upon minting.

## Features

- Create and mint unique profile NFTs
- Customize profile attributes based on DeFi activities
- Automated profile image generation
- On-chain verification of achievements

## NFT Attributes

The NFT system consists of 4 main attributes, and each profile NFT includes a randomly selected background to add uniqueness:

1. **Face (Deposit)**: Represents deposit activities

   - Includes variations like Bubbly (OolongSwap), Slick (SushiSwap), Mellow (Uniswap V3)

2. **Straw (Bridge)**: Represents bridge activities

   - Features Yellow (Boba LightBridge), Lavender (Symbiosis)

3. **Boba (Swap)**: Represents swap activities

   - Includes variations for different tokens (ETH, USDC, USDT, BOBA)

4. **Special (Optional)**: Custom attributes

**Background**: Automatically and randomly selected from:

- Common backgrounds: Lavender, Mint, Pink, Beige, etc.
- Rare backgrounds (Chain specific): Blue Starburst, Pastel Glow

Each item has a unique ID calculated by: `256 * itemId + attrId`

## Sample Profile NFT

Here's an example of a Profile NFT:  
![image](https://github.com/user-attachments/assets/f793642b-2175-4d43-914c-761fc7c21630)


## Installation

To install and run the project locally, follow these steps:

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/boba-profile-nft.git
   ```
2. Navigate to the project directory:
   ```bash
   cd boba-profile-nft
   ```
3. Install dependencies:
   ```bash
   yarn install
   ```
4. Set up environment variables:
   ```bash
   cp .env.sample .env
   # Edit .env with your configuration
   ```

## Development

### Local Testing

```bash
yarn test
```

### Local Deployment

```bash
npx hardhat node
yarn deploy:local
```

### Mainnet Deployment

1. Configure your environment variables in `.env`
2. Deploy contracts:
   ```bash
   yarn deploy:boba
   ```
3. Setup attributes:
   ```bash
   yarn setup:boba
   ```
4. Set resolvers:
   ```bash
   yarn resolver:boba
   ```

> 🔒 **Security**: Make sure to use different private keys for different purposes (deployment, resolver, etc.) and keep them secure.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
