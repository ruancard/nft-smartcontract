Markdown
# NFT Marketplace Smart Contract

A standard ERC-721 NFT Marketplace written in Solidity (`^0.8.9`) using OpenZeppelin. It allows users to mint NFTs with metadata, list them for sale, and buy them directly.

---

## Core Features & Functions

### Write Functions
* `createNFT(string name, uint256 price, string contentURI)`: Mints a new NFT to your wallet with a custom price and metadata link.
* `toggleNFTForSale(uint256 tokenId)`: Lists or unlists your NFT on the marketplace.
* `buyNFT(uint256 tokenId) payable`: Buys a listed NFT. Transfers funds to the seller and refunds any overpayment automatically.

### Read Functions
* `getNFTsForSale()`: Returns an array of all active listings.
* `getMyNFTs()`: Returns an array of all NFTs owned by the caller.

---

## Quick Start & Interaction

### 1. Project Setup
```bash
npm install @openzeppelin/contracts hardhat dotenv
npx hardhat compile
2. Interaction Code (ethers.js example)
JavaScript
// Mint an NFT (Price in Wei: 0.05 ETH)
await nftMarketplace.createNFT("My NFT", ethers.parseEther("0.05"), "ipfs://metadata-link");

// Put it up for sale (Token ID: 0)
await nftMarketplace.toggleNFTForSale(0);

// Buy the NFT from another wallet
await nftMarketplace.buyNFT(0, { value: ethers.parseEther("0.05") });
Deployment Guide (Hardhat)
1. Environment Configuration (.env)
Snippet de código
PRIVATE_KEY="your_wallet_private_key"
RPC_URL="[https://sepolia.infura.io/v3/your_api_key](https://sepolia.infura.io/v3/your_api_key)"
2. Hardhat Config (hardhat.config.js)
JavaScript
require("@nomicfoundation/hardhat-toolbox");
require("dotenv").config();

module.exports = {
  solidity: "0.8.20",
  networks: {
    sepolia: {
      url: process.env.RPC_URL,
      accounts: [process.env.PRIVATE_KEY]
    }
  }
};
3. Deployment Script (scripts/deploy.js)
JavaScript
const hre = require("hardhat");

async function main() {
  const Marketplace = await hre.ethers.getContractFactory("NFTMarketp1ace");
  const marketplace = await Marketplace.deploy();
  await marketplace.waitForDeployment();
  console.log(`Contract deployed to: ${await marketplace.getAddress()}`);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
4. Deploy Command
Bash
npx hardhat run scripts/deploy.js --network sepolia
License
MIT
