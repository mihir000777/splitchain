# 💸 SplitChain — Trustless Expense Sharing on Ethereum

> **"Turn 'I'll pay you back' into 'It's already done.'"**

![Solidity](https://img.shields.io/badge/Solidity-0.8.0-363636?style=for-the-badge&logo=solidity)
![Ethereum](https://img.shields.io/badge/Ethereum-Sepolia-3C3C3D?style=for-the-badge&logo=ethereum)
![ethers.js](https://img.shields.io/badge/ethers.js-5.7.2-2535a0?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-00f5b4?style=for-the-badge)

---

## 🌐 Live Demo
🔗 **[splitchain.github.io/splitchain](https://splitchain.github.io/splitchain)**

> Connect MetaMask on **Sepolia testnet** to interact with the live contract.

---

## 🚨 The Problem

Every group expense app — Splitwise, Venmo, PayPal — has the same flaw:

- ❌ Centralized servers that can go down
- ❌ Accounts that can be frozen or reversed
- ❌ You still have to **trust** your friends to pay
- ❌ No real enforcement — just awkward reminders

---

## ✅ The Solution

SplitChain moves expense sharing **on-chain**. The smart contract:

- Automatically splits ETH between participants
- Tracks balances immutably on the blockchain
- Lets anyone settle their debt by sending ETH directly
- Requires **zero trust** — the code is the agreement

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔗 **Wallet Connect** | MetaMask integration with live network detection |
| 💸 **Add Expense** | Split ETH among multiple addresses instantly |
| 📊 **Check Balance** | See exactly who owes what, on-chain |
| ⚡ **Settle Payment** | Pay your share directly to the contract |
| 🔍 **Etherscan Links** | Every transaction links to the block explorer |
| 🌐 **Multi-network** | Supports Ethereum, Sepolia, Polygon, Base |

---

## 🛠 Tech Stack

```
Smart Contract  →  Solidity ^0.8.0 (deployed on Sepolia)
Frontend        →  HTML + CSS + Vanilla JavaScript
Web3 Library    →  ethers.js v5.7.2
Wallet          →  MetaMask
Deployment      →  GitHub Pages (HTTPS)
```

---

## 📄 Smart Contract

**Deployed on Sepolia:**
`0xfd0842dee0ec43dfbf9570fddb01b193c2082b52`

🔍 [View on Sepolia Etherscan](https://sepolia.etherscan.io/address/0xfd0842dee0ec43dfbf9570fddb01b193c2082b52)

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SplitBill {

    mapping(address => int) public balances;

    function addExpense(address[] memory participants) public payable {
        require(msg.value > 0, "Send ETH");
        uint share = msg.value / participants.length;
        for (uint i = 0; i < participants.length; i++) {
            balances[participants[i]] -= int(share);
        }
        balances[msg.sender] += int(msg.value);
    }

    function settle() public payable {
        balances[msg.sender] += int(msg.value);
    }

    function getBalance(address user) public view returns (int) {
        return balances[user];
    }
}
```

---

## 🚀 How to Use

### Prerequisites
- [MetaMask](https://metamask.io) browser extension
- Sepolia test ETH from a [faucet](https://sepoliafaucet.com)

### Steps
1. Visit the **[live demo](https://splitchain.github.io/splitchain)**
2. Click **Connect** → approve MetaMask on Sepolia
3. **Add Expense** → paste participant addresses + ETH amount → confirm
4. **Check Balance** → enter any wallet address to see what they owe
5. **Settle** → enter amount → pay on-chain

---

## 🏃 Run Locally

```bash
# Clone the repo
git clone https://github.com/YOUR-USERNAME/splitchain.git
cd splitchain

# Open with Live Server (VS Code extension)
# OR just open index.html directly in your browser
```

> No npm, no webpack, no build step. Just open and use.

---

## 🗺 Roadmap

- [ ] Group creation with on-chain membership
- [ ] ERC-20 token support (USDC, DAI)
- [ ] Push notifications when balance changes
- [ ] Mobile app (React Native)
- [ ] DAO governance for protocol upgrades
- [ ] Multi-sig settlement approval

---

## 🏆 Built For

This project was built for a **Web3 Hackathon** to demonstrate how blockchain technology can solve real-world trust problems in everyday finance.

---

## 👨‍💻 Author

Built with ❤️ and a lot of Sepolia ETH.

---

## 📜 License

MIT — use it, fork it, ship it.

---

<div align="center">
  <strong>SplitChain — Because trust is overrated.</strong>
</div>
