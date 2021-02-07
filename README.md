# Setup

1. create a `.env` file like below:

   ```
   INFURA_API_KEY =
   DEPLOYMENT_ACCOUNT_KEY =
   ```

   _\*ask for values to the team and pass them_

2. navigate to your repo directory and install the dependencies:

   ```
   npm install
   ```

# Deploy to a Local Ganache Instance That Mirrors the Mainnet

1. Install the [Ganache CLI](https://github.com/trufflesuite/ganache-cli)

   ```
   npm install -g ganache-cli
   ```

2. _Fork_ and mirror mainnet into your Ganache instance.
   You can fork mainnet and use each protocol's production contracts and production ERC20 tokens.
   Replace `INFURA_API_KEY` with the value in the following and run:

   ```
   ganache-cli --fork https://mainnet.infura.io/v3/INFURA_API_KEY -i 1
   ```

3. In a new terminal window in your repo directory, run:

   ```
   truffle console
   ```

4. Migrate your FlashLoan contract to your instance of Ganache with:

   ```
   migrate --reset
   ```

   \*After a few minutes, your contract will be deployed.

# Deploy to the Mainnet

1. Run:

   ```
   truffle console --network mainnet
   ```

2. You are now connected to the mainnet. Now, use the migrate command to deploy your contract:

   ```
   migrate --reset
   ```

   You might get the error below:

   ```
   /aave-flash-loans/node_modules/@trufflesuite/web3-provider-engine/index.js:219
      number:           ethUtil.toBuffer(jsonBlock.number),
                                                   ^
   TypeError: Cannot read property 'number' of null
   ```

# Interact With the Contract

Call your contract's flashLoan function within the truffle console.

```
let instance = await FlashLoan.deployed()
const DAI = "0x6b175474e89094c44da98b954eedeac495271d0f";
const amount = 20; // specify the amount
const USDC = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48";
await instance.flashLoan(DAI, amount, USDC)
```