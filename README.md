Absolutely! Here's the updated `README.md` with a new section explaining how to deploy the contract using **Remix IDE**, in addition to Hardhat.

---

```markdown
# 🧠 BrainRot Token (ROT)

A simple ERC-20 token contract deployed on the **Sepolia Testnet**, built using Solidity and OpenZeppelin.

---

## 📄 Description

This project implements a basic ERC-20 token called **BrainRot** (`ROT`). It's deployed on the Sepolia testnet and mints **1,000,000 ROT** tokens to the deployer's address upon deployment.

The contract uses OpenZeppelin's standard ERC-20 implementation for security and reliability.

---

## 🔧 Smart Contract

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
    constructor() ERC20("BrainRot", "ROT") {
        _mint(msg.sender, 1000000 * (10 ** uint256(decimals())));
    }
}
```

---

## 🚀 Deployment Options

You can deploy the token using either **Hardhat** or **Remix IDE**:

---

### 🛠 Option 1: Hardhat (Local Dev Environment)

#### ✅ Prerequisites

1. **Node.js and npm** (v14 or higher recommended)
2. **Hardhat**
3. **Metamask Wallet** with Sepolia Testnet configured
4. **Sepolia ETH** for gas fees — get from the [PoW Sepolia Faucet](https://sepolia-faucet.pk910.de/)
5. **OpenZeppelin Contracts** package installed
6. `.env` file with your private key and RPC URL (for Sepolia)

#### 📁 Project Setup

```bash
mkdir brainrot-token
cd brainrot-token
npm init -y
npm install --save-dev hardhat
npx hardhat
# Choose "Create a basic sample project"
npm install @openzeppelin/contracts dotenv
```

#### 📁 Project Structure

```
brainrot-token/
├── contracts/
│   └── MyToken.sol
├── scripts/
│   └── deploy.js
├── .env
├── hardhat.config.js
└── README.md
```

#### ✏️ `deploy.js` Script

```javascript
require("dotenv").config();
const { ethers } = require("hardhat");

async function main() {
  const Token = await ethers.getContractFactory("MyToken");
  const token = await Token.deploy();
  await token.deployed();

  console.log(`BrainRot deployed to: ${token.address}`);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

#### 🔐 .env File Example

```
PRIVATE_KEY=your_private_key_without_0x
SEPOLIA_RPC_URL=https://sepolia.infura.io/v3/YOUR_PROJECT_ID
```

#### ⚙️ `hardhat.config.js` Example

```javascript
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
  solidity: "0.8.20",
  networks: {
    sepolia: {
      url: process.env.SEPOLIA_RPC_URL,
      accounts: [`0x${process.env.PRIVATE_KEY}`],
    },
  },
};
```

#### 🚀 Deploy to Sepolia

```bash
npx hardhat run scripts/deploy.js --network sepolia
```

Make sure your wallet has **Sepolia ETH** before deploying (use the [PoW Sepolia Faucet](https://sepolia-faucet.pk910.de/)).

---

### 🧪 Option 2: Remix IDE (Quick & Easy)

#### ✅ Prerequisites

1. Visit [https://remix.ethereum.org](https://remix.ethereum.org)
2. Use a browser wallet like **MetaMask** connected to the **Sepolia Testnet**
3. Ensure your wallet has **Sepolia ETH** (get it from [PoW Faucet](https://sepolia-faucet.pk910.de/))

#### 🚀 Steps

1. Open Remix and create a new file `MyToken.sol`
2. Paste the contract code into it
3. In the **Solidity Compiler** tab, select version `0.8.20` and click **Compile**
4. In the **Deploy & Run Transactions** tab:
   - Environment: **Injected Provider - MetaMask**
   - Ensure you're connected to Sepolia
   - Click **Deploy**
5. Confirm the transaction in MetaMask

✅ That's it! You’ll receive the deployed contract address once the transaction is mined.

---

## 🔎 Verify Deployment

You can verify your deployed contract using:

- [Etherscan Sepolia Explorer](https://sepolia.etherscan.io/)
- The contract address shown in the deployment output

---

## 📬 Contact

Feel free to reach out if you have questions or want to collaborate!

---

## 🪙 License

MIT © 2025 – BrainRot Team
```

---

Let me know if you want to include a badge, a token logo, or a demo frontend where users can interact with your token (send, approve, check balance, etc.).
