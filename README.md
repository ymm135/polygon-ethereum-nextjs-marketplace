- ## Full stack NFT marketplace built with Polygon, Solidity, IPFS, & Next.js
- ### [业务流程梳理](业务流程梳理.md)  
  
- [Running this project](#running-this-project)
  - [Gitpod](#gitpod)
  - [Local setup](#local-setup)
- [Configuration](#configuration)
- [问题](#问题)
- [HardHat使用](#hardhat使用)
  - [Hardhat for Visual Studio Code](#hardhat-for-visual-studio-code)
  - [next.js vscode debug](#nextjs-vscode-debug)
- [环境准备](#环境准备)
  - [更新IPFS为本地](#更新ipfs为本地)
- [Failed to start the JavaScript console: api modules: Method rpc\_modules not found](#failed-to-start-the-javascript-console-api-modules-method-rpc_modules-not-found)
- [从`Ganache`导入用户到MataMask](#从ganache导入用户到matamask)
- [fetchMarketItems() 报错](#fetchmarketitems-报错)


![Header](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pfofv47dooojerkmfgr4.png)

This is the codebase to go along with tbe blog post [Building a Full Stack NFT Marketplace on Ethereum with Polygon](https://dev.to/dabit3/building-scalable-full-stack-apps-on-ethereum-with-polygon-2cfb)

### Running this project

#### Gitpod

To deploy this project to Gitpod, follow these steps:

1. Click this link to deploy

[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#github.com/dabit3/polygon-ethereum-nextjs-marketplace)

2. Import the RPC address given to you by GitPod into your MetaMask wallet

This endpoint will look something like this:

```
https://8545-copper-swordtail-j1mvhxv3.ws-eu18.gitpod.io/
```

The chain ID should be 1337. If you have a localhost rpc set up, you may need to overwrite it.

![MetaMask RPC Import](wallet.png)

#### Local setup

Prerequisites
To be successful in this guide, you must have the following:

- Node.js version `16.14.0` or greater installed on your machine. I recommend installing Node using either nvm or fnm.
- Metamask wallet extension installed as a browser extension

To run this project locally, follow these steps.

1. Clone the project locally, change into the directory, and install the dependencies:

```sh
git clone https://github.com/dabit3/polygon-ethereum-nextjs-marketplace.git

cd polygon-ethereum-nextjs-marketplace

# install using NPM or Yarn
npm install

# or

yarn
```

2. Start the local Hardhat node

```sh
npm install -g hardhat
```

```sh
npx hardhat node
```

1. With the network running, deploy the contracts to the local network in a separate terminal window

```sh
npx hardhat run scripts/deploy.js --network localhost
```

4. Start the app

```
npm run dev
```

### Configuration

To deploy to Polygon test or main networks, update the configurations located in __hardhat.config.js__ to use a private key and, optionally, deploy to a private RPC like Infura.

```javascript
require("@nomiclabs/hardhat-waffle");
const fs = require('fs');
const privateKey = fs.readFileSync(".secret").toString().trim() || "01234567890123456789";

// infuraId is optional if you are using Infura RPC
const infuraId = fs.readFileSync(".infuraid").toString().trim() || "";

module.exports = {
  defaultNetwork: "hardhat",
  networks: {
    hardhat: { // 所有配置项
      chainId: 1337
    },
    mumbai: {
      // Infura
      // url: `https://polygon-mumbai.infura.io/v3/${infuraId}`
      url: "https://rpc-mumbai.matic.today",
      accounts: [privateKey]
    },
    matic: {
      // Infura
      // url: `https://polygon-mainnet.infura.io/v3/${infuraId}`,
      url: "https://rpc-mainnet.maticvigil.com",
      accounts: [privateKey]
    }
  },
  solidity: {
    version: "0.8.4",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      }
    }
  }
};
```

If using Infura, update __.infuraid__ with your [Infura](https://infura.io/) project ID.


### 问题
### HardHat使用

```sh
mkdir hardhat-tutorial
cd hardhat-tutorial

npm init
npx hardhat
❯ Create an empty hardhat.config.js

npm install --save-dev @nomicfoundation/hardhat-toolbox
```

> 帮助 npx hardhat help [task] , 比如 npx hardhat help compile 
> Usage: hardhat [GLOBAL OPTIONS] compile [--concurrency <INT>] [--force] [--quiet]

`hardhat.config.js`  
```js
require("@nomicfoundation/hardhat-toolbox");

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.9",
};
```

在`contracts`目录，建立`Token.sol`  
```sh
▶ npx hardhat compile
Downloading compiler 0.8.17
Compiled 1 Solidity file successfully
```

#### Hardhat for Visual Studio Code
[插件地址](https://marketplace.visualstudio.com/items?itemName=NomicFoundation.hardhat-solidity)  

#### next.js vscode debug
[官方文档](https://nextjs.org/docs/advanced-features/debugging)  

`.vscode/launch.json`
```sh
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Next.js: debug server-side",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev"
    },
    {
      "name": "Next.js: debug client-side",
      "type": "chrome",
      "request": "launch",
      "url": "http://localhost:3000"
    },
    {
      "name": "Next.js: debug full stack",
      "type": "node-terminal",
      "request": "launch",
      "command": "npm run dev",
      "serverReadyAction": {
        "pattern": "started server on .+, url: (https?://.+)",
        "uriFormat": "%s",
        "action": "debugWithChrome"
      }
    }
  ]
}
```
### IPFS环境搭建
[js 环境搭建](https://github.com/ipfs/js-ipfs/tree/master/packages/ipfs-http-client#install) 

#### demo测试
[demo地址](https://github.com/status-im/liquid-funding/blob/a0223d6adee4467470f4b3b6589b3c5784d33440/src/utils/ipfs.js#L9)  
```

```

### 环境准备

测试用例
```sh
npx hardhat test
```

输出结果
```json
  NFTMarket
items:  [
  {
    price: '1000000000000000000',
    tokenId: '1',
    seller: '0x70997970C51812dc3A010C7d01b50e0d17dc79C8',
    owner: '0x5FbDB2315678afecb367f032d93F642f64180aa3',
    tokenUri: 'https://www.mytokenlocation.com'
  },
  {
    price: '1000000000000000000',
    tokenId: '2',
    seller: '0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266',
    owner: '0x5FbDB2315678afecb367f032d93F642f64180aa3',
    tokenUri: 'https://www.mytokenlocation2.com'
  }
]
    ✔ Should create and execute market sales (2048ms)


  1 passing (2s)
```

#### 更新IPFS为本地

```sh
-const client = ipfsHttpClient('https://ipfs.infura.io:5001/api/v0')
+const client = ipfsHttpClient('http://localhost:5001/')

-      const url = `https://ipfs.infura.io/ipfs/${added.path}`
+      const url = `http://localhost:8080/ipfs/${added.path}`

-      const url = `https://ipfs.infura.io/ipfs/${added.path}`
+      const url = `http://localhost:8080/ipfs/${added.path}`
```

资源路径:
```sh
https://ipfs.io/ipfs/QmUffoK7o92C8k58xY4fMHcCN1oZ8DBEZnybkokQxvj65m?filename=%E4%BA%A4%E6%8D%A2%E6%9C%BA%E7%AE%A1%E7%90%86%E7%95%8C%E9%9D%A2-1.png
```

### Failed to start the JavaScript console: api modules: Method rpc_modules not found
```sh
▶ geth attach ipc:http://127.0.0.1:8545
Fatal: Failed to start the JavaScript console: api modules: Method rpc_modules not found
```

可以不使用`hardhat`启动,仍然使用`Ganache`,设置链ID为`1337`, 直接使用`npx hardhat run scripts/deploy.js` 部署  

```shell
▶ geth attach ipc:http://127.0.0.1:8545
Welcome to the Geth JavaScript console!

instance: EthereumJS TestRPC/v2.13.1/ethereum-js
coinbase: 0x13a5bb41d4c229b7f3c85509952080c7646a5e26
at block: 17 (Wed Aug 31 2022 19:19:46 GMT+0800 (CST))
 modules: eth:1.0 evm:1.0 net:1.0 personal:1.0 rpc:1.0 web3:1.0

To exit, press ctrl-d or type exit
```

## js问题
async表示函数里有异步操作，await表示紧跟在后面的表达式需要等待结果。需要注意的是await关键字只在async函数内有效，如果在async函数体之外使用它，会抛出语法错误。  

 async函数返回一个 `Promise`对象，可以使用then方法添加回调函数。只要使用async，不管函数内部返回的是不是Promise对象，都会被包装成Promise对象。  

```js
async function testAsync() {
    return "hello async";
}

const result = testAsync();
console.log(result);
```

返回的结果
```sh
Promise {<fulfilled>: 'hello async'}
[[Prototype]]: Promise
[[PromiseState]]: "fulfilled"
[[PromiseResult]]: "hello async"
```



### 从`Ganache`导入用户到MataMask 
在`MetaMask`通过用`Ganache`用户的私钥，导入用户

### fetchMarketItems() 报错

[Geth](https://aaronbloomfield.github.io/ccc/docs/geth_reference.html)    

```sh
Unhandled Runtime Error
Error: call revert exception [ See: https://links.ethers.org/v5-errors-CALL_EXCEPTION ] (method="fetchMarketItems()", data="0x", errorArgs=null, errorName=null, errorSignature=null, reason=null, code=CALL_EXCEPTION, version=abi/5.7.0)
```

获取现有的item报错
```js
export default function Home() {
  const [nfts, setNfts] = useState([])
  const [loadingState, setLoadingState] = useState('not-loaded')
  useEffect(() => {
    loadNFTs()
  }, [])
  async function loadNFTs() {
    /* create a generic provider and query for unsold market items */
    const provider = new ethers.providers.JsonRpcProvider()
    const contract = new ethers.Contract(marketplaceAddress, NFTMarketplace.abi, provider)
    const data = await contract.fetchMarketItems()
```

使用命令行模拟
部署之后，会在当前项目生成`ABI`文件  
`artifacts/contracts/NFTMarketplace.sol`  

```sh
var addr = '0x10b72967d0424F8E8d363Cd2ccF2AD8F3fd813D1';
var abi = [...];
var conInterface = eth.contract(abi).at(addr);

# 没有参数
conInterface.fetchMarketItems.call()
```

查看日志
```shell
[2022/12/02 14:26:49.987] - eth_call
[2022/12/02 14:26:49.988] -    > {
   >   "jsonrpc": "2.0",
   >   "id": 37,
   >   "method": "eth_call",
   >   "params": [
   >     {
   >       "data": "0x0f08efe0",
   >       "to": "0x10b72967d0424F8E8d363Cd2ccF2AD8F3fd813D1"
   >     },
   >     "latest"
   >   ]
   > }
[2022/12/02 14:26:50.031] -  <   {
 <     "id": 37,
 <     "jsonrpc": "2.0",
 <     "result": "0x00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000000"
 <   }
```

需要更新IPFS的链接
```js
import { create as ipfsHttpClient } from 'ipfs-http-client'
import { useRouter } from 'next/router'
import Web3Modal from 'web3modal'

const client = ipfsHttpClient('http://localhost:5001')
```

最后发现是依赖库的问题，因为我单独执行了`npm instal --save ipfs-http-client`, 版本已经升级到`56.0.3`, 已经不是`56.0.1`  

> 无论什么脚手架，版本号都是要匹配的，如果使用最新版本或者不是发布的版本，可能导致各种异常  








