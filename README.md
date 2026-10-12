# Mina Token Manager

A browser app for deploying and managing fungible tokens on Mina. It is aimed at developers who want to try the Mina fungible token standard (deploy, mint, transfer, check balances) from a UI, with Auro Wallet, instead of writing scripts. The hosted demo is no longer online.

> **Status:** archived. Built in 2024. Kept for reference, not maintained.

![Mina Token Manager home page](https://github.com/user-attachments/assets/63691bef-979c-40fd-b46f-10c3bc5f3b74)

> **Warning:** for testing and development only, not for real funds. Deploying a token asks for a fee payer private key in the browser, and each new token's generated admin private key is stored in the browser's localStorage. For production use, see the official [Mina fungible token](https://github.com/MinaFoundation/mina-fungible-token) repository.

## What it does

- Deploys a new token (a `FungibleToken` contract plus its `FungibleTokenAdmin` contract) with a chosen symbol, decimals and source URL. The transaction is proved with o1js in a Web Worker and sent through Auro Wallet.
- Mints tokens to a recipient address, authorized by the token's admin key.
- Transfers tokens from the connected Auro Wallet account to another address, and checks the token balance of any public key.
- Shows token details such as circulating supply and decimals.
- Keeps a "My Tokens" list in localStorage, including tokens imported by address and admin keys.
- Switches between Mina Devnet and Mainnet from the header.

## Tech stack

- TypeScript, Next.js 14 (pages router), React 18, Tailwind CSS
- o1js 1.x, Auro Wallet
- Fungible token contracts built on `TokenContractV2`, adapted from the Mina Foundation's [mina-fungible-token](https://github.com/MinaFoundation/mina-fungible-token)
- COOP/COEP headers and `coi-serviceworker`, which o1js needs to run in the browser
- GraphQL endpoints from MinaExplorer (Devnet) and Minascan (Mainnet) for account and nonce lookups

## Running it locally

Requires Node.js 18 or later and the Auro Wallet browser extension. The UI imports the compiled contracts from `contracts/build`, so build the contracts first:

```bash
cd contracts
npm install
npm run build

cd ../ui
npm install
npm run dev
```

Then open http://localhost:3000.

## Project structure

```
.
├── contracts/   o1js FungibleToken and FungibleTokenAdmin contracts
└── ui/          Next.js app
    └── src/
        ├── pages/        index, deploy, token, my-tokens, plus the o1js Web Worker
        └── components/   Header, Footer, DeployForm, MintForm, TransferForm, BalanceForm
```

## Disclaimer

Not affiliated with or endorsed by O(1) Labs or the Mina Foundation.

## License

MIT, see [LICENSE](LICENSE). The `contracts/` folder keeps its own Apache-2.0 license ([contracts/LICENSE](contracts/LICENSE)), matching the Mina Foundation code it is adapted from.
