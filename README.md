This repo shows how to use the Transparent Proxy pattern for upgrading smart contracts. It uses most of the code from openzeppelin's repo, and adds brownie scripts on top. Freecodecamp lesson.

## Prerequisites

Please install or have installed the following:

- [nodejs and npm](https://nodejs.org/en/download/)
- [python](https://www.python.org/downloads/)
## Installation

1. [Install Brownie](https://eth-brownie.readthedocs.io/en/stable/install.html), if you haven't already. Here is a simple way to install brownie.

```bash
pip install eth-brownie
```
Or, if that doesn't work, via pipx
```bash
pip install --user pipx
pipx ensurepath
# restart your terminal
pipx install eth-brownie
```

2. For local testing [install ganache-cli](https://www.npmjs.com/package/ganache-cli)
*Skip if you only want to use testnets*

```bash
npm install -g ganache-cli
```
or
```bash
yarn add global ganache-cli
```

3. Download the mix and install dependancies. 

```bash
brownie bake upgrades-mix
cd upgrades
```

Or, you can clone from source:

```bash
git clone https://github.com/PatrickAlphaC/upgrades-mix
cd upgrades-mix
```

## Environment Variables
If you want to be able to deploy to testnets or work with mainnet-fork, do the following. 

1. Set your `WEB3_INFURA_PROJECT_ID`, and `PRIVATE_KEY` [environment variables](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html). 

You can get a `WEB3_INFURA_PROJECT_ID` by getting a free trial of [Infura](https://infura.io/). At the moment, it does need to be infura with brownie. If you get lost, you can [follow this guide](https://ethereumico.io/knowledge-base/infura-api-key-guide/) to getting a project key. You can find your `PRIVATE_KEY` from your ethereum wallet like [metamask](https://metamask.io/). 

You'll also need testnet rinkeby ETH and LINK. You can get LINK and ETH into your wallet by using the [rinkeby faucets located here](https://docs.chain.link/docs/link-token-contracts#rinkeby). If you're new to this, [watch this video.](https://www.youtube.com/watch?v=P7FX_1PePX0)

You can add your environment variables to the `.env` file:

```
export WEB3_INFURA_PROJECT_ID=<PROJECT_ID>
export PRIVATE_KEY=<PRIVATE_KEY>
```

AND THEN RUN `source .env` TO ACTIVATE THE ENV VARIABLES
(You'll need to do this everytime you open a new terminal, or [learn how to set them easier](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html)). 

> DO NOT SEND YOUR PRIVATE KEY WITH FUNDS IN IT ONTO GITHUB

Otherwise, you can build, test, and deploy on your local environment. 

# Useage
## Scripts

```
brownie run scripts/01_deploy_box.py
brownie run scripts/02_upgrade_box.py
```
This will:
1. Deploy a `Box` implementation contract
2. Deploy a `ProxyAdmin` contract to be the admin of the proxy
3. Deploy a `TransparentUpgradeableProxy` to be the proxy for the implementations
   
Then, the upgrade script will:

4. Deploy a new Box implementation `BoxV2`
5. Upgrade the proxy to point to the new implementation contract, essentially upgrading your infrastructure. 
6. Then it will call a function only `BoxV2` can call

## Test

```
brownie test
```
