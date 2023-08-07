# How to integrate with VeritiDAO

This guide will show you how to connect to the VeritiDAO smart contract using ethers.js.

### Step-by-step guide

First, set up a provider and connect to the contract. This can be a local Ethereum node, or a service like Infura.

```javascript
const ethers = require('ethers');

// Setup provider
const provider = new ethers.providers.JsonRpcProvider('https://mainnet.infura.io/v3/YOUR-PROJECT-ID');

// Contract ABI and address
const contractABI = [...]; // ABI goes here
const contractAddress = '...'; // Contract address goes here

// Create contract instance
const contract = new ethers.Contract(contractAddress, contractABI, provider);
```

Replace `'YOUR-PROJECT-ID'`, `contractABI`, and `contractAddress` with your actual Infura project ID, contract ABI, and contract address, respectively. Check the [VeritiNFT smart contract address here](../misc/smart-contracts.md).

**Example 1: Retrieve Metadata**

To retrieve metadata for a specific token, use the `tokenURI` method. This method takes a token ID as an argument and returns a JSON object containing the metadata.

Please note that the `tokenURI` function returns a data URI, which already includes the JSON object in a base64 encoded format. We need to decode this string and then parse the JSON. Here's how you can do it:

```javascript
async function retrieveMetadata(tokenId) {
    const tokenURI = await contract.tokenURI(tokenId);
    
    // Remove the prefix from the data URI
    const base64String = tokenURI.replace('data:application/json;base64,', '');

    // Decode the base64 string
    const jsonString = Buffer.from(base64String, 'base64').toString();

    // Parse the JSON
    const metadata = JSON.parse(jsonString);

    console.log(`Metadata for token ${tokenId}:`, metadata);
}
```

**Example 2: Retrieve All Current Listings**

To retrieve all current listings, iterate through each token using the `totalSupply` and `tokenByIndex` methods:

```javascript
async function retrieveAllListings() {
    const totalSupply = await contract.totalSupply();
    for(let i = 0; i < totalSupply; i++) {
        const tokenId = await contract.tokenByIndex(i);
        const tokenURI = await contract.tokenURI(tokenId);
        
        //Parse the tokenURI string into a JSON object
        //...

        console.log(`Token ID: ${tokenId}, Metadata: ${tokenURI}`);
    }
}
```

**Example 3: Listen to the Listed Event**

To maintain a live feed of all new and updated listings, you can listen to the `Listed` event using the `on` method. This allows you to update the metadata for a token in real-time whenever the `Listed` event is emitted. Here's how you can do it:

```javascript
contract.on('Listed', async (tokenId) => {
    const tokenURI = await contract.tokenURI(tokenId);
    
    //Parse the tokenURI string into a JSON object
    //...
        
    console.log(`Token ID ${tokenId} has been listed or updated. Metadata: ${tokenURI}`);
    
    //Update your database with the new metadata
    //...
});
```

Make sure to handle any errors that may occur during the execution of these methods.

### Commercial API

VeritiDAO will soon provide a commercial API for retrieving metadata. This service will eliminate the need for users to interact directly with the smart contract, offering a more streamlined and efficient data retrieval process. More information on this upcoming service will be shared in due course.
