
# **AquaDex - Decentralized Exchange on EDU Testnet Chain**

**AquaDex** is a cutting-edge **Automated Market Maker (AMM)** protocol built on the **EDU Testnet Chain**. It provides a seamless and decentralized platform for liquidity provision and token swaps between the **EDU** (native token) and **DEDU** (derived token) pairs. By empowering liquidity providers (LPs) with transaction fee rewards, AquaDex ensures an efficient and user-friendly DeFi ecosystem tailored to the EDU network.

---

## 🌟 **Table of Contents**
- [**AquaDex - Decentralized Exchange on EDU Testnet Chain**](#aquadex---decentralized-exchange-on-edu-testnet-chain)
  - [🌟 **Table of Contents**](#-table-of-contents)
  - [🌐 **Overview**](#-overview)
    - [**Core Features**](#core-features)
  - [💡 **Features**](#-features)
  - [🚀 **Getting Started**](#-getting-started)
    - [🛠️ **Prerequisites**](#️-prerequisites)
    - [📦 **Installation**](#-installation)
    - [🏃 **Running the Project**](#-running-the-project)
  - [📜 **Smart Contracts**](#-smart-contracts)
    - [➕ **Liquidity Add Function**](#-liquidity-add-function)
    - [➖ **Liquidity Remove Function**](#-liquidity-remove-function)
  - [📁 **Project Structure**](#-project-structure)
    - [**Key Files**](#key-files)
  - [📃 **License**](#-license)
  - [🤝 **Contributing**](#-contributing)
    - [**How to Contribute**](#how-to-contribute)
  - [**Acknowledgments**](#acknowledgments)

---

## 🌐 **Overview**

**AquaDex** is a decentralized exchange (DEX) that uses an **Automated Market Maker (AMM)** model to facilitate token swaps and liquidity provision. Designed specifically for the **EDU Testnet Chain**, AquaDex allows users to interact with **EDU** and **DEDU** tokens in a fast, secure, and trustless environment.

Liquidity providers (LPs) play a crucial role in maintaining the health of the exchange by contributing to the **EDU/DEDU** liquidity pool. In return, LPs earn rewards through transaction fees, creating a robust and dynamic decentralized finance (DeFi) platform.

### **Core Features**
- **Add Liquidity:** Users can deposit **EDU** and **DEDU** tokens in equal amounts to contribute to the liquidity pool and receive LP tokens as proof of their share.
- **Remove Liquidity:** LPs can withdraw their liquidity and receive a proportional amount of **EDU** and **DEDU** tokens.
- **Token Swap:** Perform instant token swaps between **EDU** and **DEDU**, with prices automatically set by the liquidity pool.
- **EDU Testnet Compatibility:** AquaDex is deployed on the **EDU Testnet Chain**, ensuring low fees and seamless blockchain integration for developers and users.

---

## 💡 **Features**

- **Seamless Liquidity Provision:** Add or remove liquidity easily through an intuitive interface.
- **Instant Token Swaps:** Swap **EDU** and **DEDU** tokens without intermediaries, with pricing based on the liquidity pool's algorithm.
- **Transaction Fee Rewards:** LPs earn a share of transaction fees, incentivizing long-term participation.
- **Testnet Optimization:** AquaDex is optimized for the **EDU Testnet Chain**, providing a reliable environment for development and testing without incurring real costs.

---

## 🚀 **Getting Started**

To get started with **AquaDex**, follow the steps below to set up your development environment and interact with the protocol.

### 🛠️ **Prerequisites**

1. **Node.js**: [Download and install Node.js](https://nodejs.org/) (Recommended: LTS version).  
2. **Metamask**: [Install Metamask](https://metamask.io/) for secure interaction with the EDU Testnet.  
3. **EDU Testnet Configuration**: Add the **EDU Testnet Chain** to your Metamask wallet using the appropriate RPC URL and chain ID.

### 📦 **Installation**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/GillHapp/EduSwap.git
   cd EduSwap
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   ```

### 🏃 **Running the Project**

1. Ensure your Metamask wallet is connected to the **EDU Testnet Chain**.  
2. Start the development server:  
   ```bash
   npm start
   ```
3. Open your browser and navigate to `http://localhost:3000` to interact with AquaDex.

---

## 📜 **Smart Contracts**

AquaDex is powered by smart contracts that handle liquidity management and token swaps in a secure and decentralized manner.

### ➕ **Liquidity Add Function**

The `addLiquidity` function allows users to add equal amounts of **EDU** and **DEDU** tokens to the liquidity pool. LP tokens are issued as proof of contribution.

```solidity
function addLiquidity(uint256 _eduAmount) external returns (bool) {
    require(_eduAmount > 0, "Amount must be greater than zero");

    uint256 deduAmount = calculateRequiredDEDU(_eduAmount);
    require(DEDU.balanceOf(msg.sender) >= deduAmount, "Insufficient DEDU balance");

    EDU.transferFrom(msg.sender, address(this), _eduAmount);
    DEDU.transferFrom(msg.sender, address(this), deduAmount);

    _mintLP(msg.sender, _eduAmount);
    return true;
}
```

### ➖ **Liquidity Remove Function**

The `removeLiquidity` function enables LPs to withdraw their liquidity from the pool, receiving both **EDU** and **DEDU** tokens in proportion to their share.

```solidity
function removeLiquidity(uint256 _lpTokens) external returns (uint256, uint256) {
    require(_lpTokens > 0, "Amount must be greater than zero");

    uint256 eduAmount = calculateEDUForLP(_lpTokens);
    uint256 deduAmount = calculateDEDUForLP(_lpTokens);

    _burnLP(msg.sender, _lpTokens);
    EDU.transfer(msg.sender, eduAmount);
    DEDU.transfer(msg.sender, deduAmount);

    return (eduAmount, deduAmount);
}
```

---

## 📁 **Project Structure**

AquaDex is built using **ReactJS** for the frontend and **Ethers.js** for blockchain interactions. Below is the directory structure:

```
/aquadex
|-- /src
|   |-- /components
|   |   |-- AddLiquidity.js
|   |   |-- RemoveLiquidity.js
|   |   |-- Swap.js
|   |-- /utils
|   |   |-- contract.js
|   |-- App.js
|   |-- index.js
|-- /public
|-- package.json
|-- package-lock.json
|-- .gitignore
```

### **Key Files**
- **AddLiquidity.js**: Handles UI and logic for adding liquidity.  
- **RemoveLiquidity.js**: Handles UI and logic for removing liquidity.  
- **Swap.js**: Manages token swap functionality.  
- **contract.js**: Contains smart contract interaction logic.

---

## 📃 **License**

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 🤝 **Contributing**

We welcome contributions to **AquaDex**! To contribute, fork the repository, make your changes, and submit a pull request.

### **How to Contribute**
1. **Fork the repository**.  
2. **Clone your fork**:  
   ```bash
   git clone  https://github.com/GillHapp/EduSwap.git
   ```  
3. **Create a new branch**:  
   ```bash
   git checkout -b feature-branch
   ```  
4. **Make your changes** and commit:  
   ```bash
   git commit -m "Add feature"
   ```  
5. **Push to your fork**:  
   ```bash
   git push origin feature-branch
   ```  
6. **Submit a pull request**.

---

## **Acknowledgments**
- **EDU Testnet Chain**: Providing a reliable, low-cost environment for DeFi applications.  
- **Metamask**: For secure interaction with blockchain networks.  
- **Ethers.js**: Simplifying blockchain interactions in JavaScript.

---

**Thank you for using EduSwap!** We’re excited to have you as part of the EDU ecosystem.  
