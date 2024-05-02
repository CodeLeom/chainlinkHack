# [JavaScript for Blockchain Developers](https://www.youtube.com/watch?v=8iLuNx9jYSo).

https://cll-devrel.gitbook.io/javascript-for-blockchain-master-class/decentralized-news-service-contract

> If this looks too tricky for you, check out: https://docs.chain.link/quickstarts/deploy-your-first-contract

## Day 1: Build a simple decentralized news aggregator service

Following [Richard's tutorial](https://github.com/smartcontractkit/workshop-distributed-news), the following was created:

- contracts [verified and deployed on sepolia testnet](https://sepolia.etherscan.io/tx/0x959a311db16d02c945f64c777ca7e82ebfa4605f47df7edb2e14fc6b20feafd4)

- Using Chainlink functions to get the latest news from hackernews api, store the story on the blockchain, and display the stories on a webpage.

### Todo
- [x] Create a contract that uses Chainlink functions to get the latest news from hackernews api
- [x] Store the story on the blockchain
- [x] Display the stories on a webpage

### Steps to run the project:
The contract is good to go and hooked up to Chainlink Functions Subscriber.
To deploy and set up your Functions, you need to:
- Compile and deploy the contract on a testnet (this is on Sepolia)
- Create and fund a [Chainlink Functions Subscription](https://functions.chain.link/)
- Add your deployed contract address to your subscription as a "Consumer"
- Add your subscription ID to the contract
- Run the `sendRequest` function on the contract to get the latest news from Hackernews and save it to the blockchain
- Call the `getAllArticles` function to get the latest news from the blockchain
    ```solidity
    function getAllArticles() public view returns (string[] memory) {
            string[] memory allArticles = new string[](articles.length);
            for (uint i = 0; i < articles.length; i++) {
                allArticles[i] = string(articles[i].url);
            }
            return allArticles;
        }
    ```
- in `/src/pages/index.astro` you can display the stories on a webpage

  ```astro
  async function fetchOGData(url) {
  try {
    const response = await fetch(url);
    const html = await response.text();
    const dom = new JSDOM(html);
    const doc = dom.window.document;
    let ogTitle =
      doc.querySelector('meta[property="og:title"]')?.content || url;
    const ogImage = doc.querySelector('meta[property="og:image"]')?.content;
    return { ogTitle, ogImage, url };
  } catch (error) {
    console.error("Error fetching OG data:", error);
    return { ogTitle: "No title", ogImage: "No image", url };
  }
}
```


To get started quickly with this code, clone the repo, run `npm install` and `npm run dev`

nothing might show on the screen, why?

You need to create a `.env` file and have the following:

```bash
#### RPC for sepolia
PROVIDER_URL="https://rpc.sepolia.org"
CONTRACT_ADDRESS="your-contract-address"
```

Follow this [article](https://cll-devrel.gitbook.io/javascript-for-blockchain-master-class/decentralized-news-service-contract) to get your contract ready and deployed. 

> This repo is just the frontend Dapp that interact with the smart contract using `ether-js`.

