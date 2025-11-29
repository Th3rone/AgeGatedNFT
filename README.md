# 🎟️ AgeGatedNFT — Encrypted Age Verification for NFT Access (FHEVM)

**AgeGatedNFT** introduces a new approach to gated digital collectibles using **Fully Homomorphic Encryption (FHE)**.
Instead of revealing a user’s birth year or age, the contract performs an encrypted comparison to determine whether the user meets a required minimum age — without ever exposing sensitive information on-chain.

Powered by **Zama’s FHEVM**, this system enables **private age verification**, secure NFT minting, and optional public reveal of verification status.

---

## 🔍 What This Project Demonstrates

* 🔐 **Confidential Age Proofing**: Users submit encrypted birth year values.
* 🧮 **Encrypted On-Chain Computation**: Age is calculated using FHE subtraction and compared to the minimum allowed age homomorphically.
* 🎯 **NFT Minting Based on Private Conditions**: Only users who satisfy the encrypted age check may mint.
* 🕵️ **Zero Exposure of Personal Data**: No plaintext age or birth year is ever revealed unless the user chooses to.
* 🌐 **Seamless User Flow**: The contract returns encrypted handles compatible with the Relayer SDK for client-side decryption.

This contract is ideal for **age-restricted content**, **event passes**, **membership NFTs**, and any scenario where verifying identity attributes must remain private.

---

## 🧱 Core Components

### 🔹 Encrypted Verification Storage

Each user receives a private `ebool` representing whether they meet the age requirement.

### 🔹 Homomorphic Age Calculation

Steps performed entirely under encryption:

```
1. Retrieve encrypted birth year.
2. Convert current year → encrypted constant.
3. Compute encryptedAge = currentYear - birthYear.
4. Compare encryptedAge >= minAgeEncrypted.
```

### 🔹 NFT Minting Logic

Minting is only permitted if the **publicly decrypted result** returns `true`.
This avoids plaintext exposure inside the smart contract while keeping the logic verifiable for users.

---

## 📦 Repository Structure

```
AgeGatedNFT/
├── contracts/
│   └── AgeGatedNFT.sol
├── deploy/
├── frontend/
│   └── index.html (optional UI integration)
├── hardhat.config.js
└── package.json
```

---

## 🚀 Setup

### Install Packages

```bash
git clone https://github.com/Th3rone/AgeGatedNFT
cd AgeGatedNFT
npm install
```

### Configure Environment

```bash
npx hardhat vars set MNEMONIC
npx hardhat vars set INFURA_API_KEY
npx hardhat vars set ETHERSCAN_API_KEY
```

### Compile / Test

```bash
npm run compile
npm run test
```

---

## 🌐 Deployment

### Local Development Chain

```bash
npx hardhat node
npx hardhat deploy --network localhost
```

### Deploy to Sepolia FHEVM

```bash
npx hardhat deploy --network sepolia
npx hardhat verify --network sepolia
```

Add your deployed contract address here after deployment.

---

# 🖥 Frontend Workflow (Relayer SDK)

The encrypted birth year is submitted via:

* `createEncryptedInput(...)`
* `userDecrypt(...)` for private decryption
* `publicDecrypt(...)` if the user chooses to reveal their result

Workflow:

1. User encrypts their birth year in the browser.
2. Contract computes age eligibility homomorphically.
3. User decrypts the result locally.
4. If desired, user can publish the verification.
5. Eligible users mint their NFT.

No sensitive information ever touches the chain.

---

## 📚 Reference Links

* FHEVM Overview — [https://docs.zama.ai/protocol](https://docs.zama.ai/protocol)
* Relayer SDK Docs — [https://docs.zama.ai/protocol/relayer-sdk-guides/](https://docs.zama.ai/protocol/relayer-sdk-guides/)
* Solidity FHE Library — [https://github.com/zama-ai/fhevm-solidity](https://github.com/zama-ai/fhevm-solidity)
* OpenZeppelin ERC721 — [https://docs.openzeppelin.com/contracts/](https://docs.openzeppelin.com/contracts/)

---

## 🆘 Support

* Create an issue on GitHub
* Zama Discord — [https://discord.gg/zama-ai](https://discord.gg/zama-ai)

---

## 📄 License

**MIT License**
