NFT Minting dApp project based on the PRD:

---

# NFT Minting dApp

A simple decentralized application (dApp) that allows users to mint unique NFTs and view ownership on-chain. This project demonstrates wallet connection, NFT minting, and metadata display using Solidity, Hardhat, React, and Ethers.js.

---

## 🚀 Features

**Core Features:**

* Connect wallet (MetaMask)
* Mint NFTs (ERC-721 standard)
* View owned NFTs
* Display token metadata (name, image)

**Non-Goals (for 1-day build):**

* No marketplace (buy/sell)
* No advanced rarity logic
* No IPFS pinning UI (metadata can be hardcoded or simple upload)

---

## ✅ Success Criteria

* User can successfully mint an NFT
* Minted NFT is visible in wallet and in the UI
* Smart contract deployed to testnet (e.g., Sepolia)

---
## 📚 DEMO
<img width="766" height="334" alt="Screenshot 2026-03-27 at 7 59 06 PM" src="https://github.com/user-attachments/assets/82cf4d02-9b32-44ba-8d32-3a2dda008be6" />
<img width="1177" height="777" alt="Screenshot 2026-03-27 at 7 59 30 PM" src="https://github.com/user-attachments/assets/9b2abfe5-8a3e-4069-ad92-cd16881a99f8" />
<img width="892" height="472" alt="Screenshot 2026-03-27 at 7 59 42 PM" src="https://github.com/user-attachments/assets/51c20670-d8a9-49d1-ae69-c9d7c58e8b4a" />


---
## 🛠️ Technology Stack

* **Blockchain:** Ethereum (Sepolia testnet)
* **Smart Contract:** Solidity (ERC-721 via OpenZeppelin)
* **Deployment:** Hardhat
* **Frontend:** React + Ethers.js
* **Wallet:** MetaMask

---

## 📄 Smart Contract

**Contract: `MyNFT.sol`**

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

contract MyNFT is ERC721 {
    uint256 public tokenCounter;

    constructor() ERC721("MyNFT", "MNFT") {
        tokenCounter = 0;
    }

    function mintNFT(address to) public {
        _safeMint(to, tokenCounter);
        tokenCounter++;
    }
}
```

---

## ⚡ Deployment with Hardhat

1. Install Hardhat:

```bash
npm install --save-dev hardhat
```

2. Configure Sepolia network in `hardhat.config.js`.

3. Deploy script (`deploy.js`):

```javascript
async function main() {
  const NFT = await ethers.getContractFactory("MyNFT");
  const nft = await NFT.deploy();
  await nft.deployed();
  console.log("Deployed to:", nft.address);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

Run deployment:

```bash
npx hardhat run scripts/deploy.js --network sepolia
```

---

## 🖥️ Frontend (React + Ethers.js)

1. **Connect Wallet:**

```javascript
await window.ethereum.request({ method: "eth_requestAccounts" });
```

2. **Mint NFT:**

```javascript
const contract = new ethers.Contract(address, abi, signer);
await contract.mintNFT(userAddress);
```

3. **Display Owned NFTs:**
   Fetch token IDs from the contract and show metadata (name, image) in the UI.

---

## 🖼️ Metadata Example

```json
{
  "name": "My NFT",
  "description": "Demo NFT",
  "image": "https://example.com/image.png"
}
```

---

## 📚 References

* [OpenZeppelin ERC-721 Docs](https://docs.openzeppelin.com/contracts/4.x/erc721)
* [Hardhat Docs](https://hardhat.org/getting-started/)
* [Ethers.js Docs](https://docs.ethers.org/v5/)

---

