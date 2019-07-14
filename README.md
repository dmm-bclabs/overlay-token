# Overlay Token
Overlay Token: A cross-chain token protocol for simple, better user experiences on multi-blockchain environments.

## Overview

![Overlay Token Overview](docs/OverlayToken.svg)


![Application Example](docs/ETHLock.svg)


## Demo movies

[![OverlayTokenDemo](http://img.youtube.com/vi/P4w2f_tFXpE/0.jpg)](http://www.youtube.com/watch?v=P4w2f_tFXpE "OverlayTokenDemo")

[![OverlayTokenRopstenDemo](http://img.youtube.com/vi/P4w2f_tFXpE/0.jpg)](http://www.youtube.com/watch?v=P4w2f_tFXpE "OverlayTokenRopstenDemo")

## Repositories

- [substrate-overlay-token](https://github.com/dmm-bclabs/substrate-overlay-token)
  - Substrate version of an overlay token implementation
- [substrate-overlay-token-bridge](https://github.com/dmm-bclabs/substrate-overlay-token-bridge)
  - Bridge implementation of overlay token between substrate chains
- [substrate-overlay-token-ui](https://github.com/dmm-bclabs/substrate-overlay-token-ui)
  - Web UI implementation of overlay token for substrate chain 
- [ethereum-overlay-token](https://github.com/dmm-bclabs/ethereum-overlay-token)
  - Ethereum version of an overlay token implementation
- [ethereum-overlay-token-bridge](https://github.com/dmm-bclabs/ethereum-overlay-token-bridge)
  -  Bridge implementation of overlay token between Ethereum and substrate chains
- [ethereum-overlay-token-ui](https://github.com/dmm-bclabs/ethereum-overlay-token-ui)
  - Web UI implementation of overlay token for Ethereum

## To play

### Substrate <-> Substrate

![Demo 1 Architecture](docs/BridgeArchitecture.svg)

#### Start Parent Chain

```
$ git clone https://github.com/dmm-bclabs/substrate-overlay-token.git
$ cd substrate-overlay-token
    
$ ./scripts/build.sh
$ cargo build --release
    
$ ./target/release/substrate-overlay-token purge-chain --chain parent --base-path /tmp/parent -y
$ ./target/release/substrate-overlay-token --chain parent --charlie --validator --base-path /tmp/parent --ws-port 9944
```

#### Start Child Chain

```
$ cd substrate-overlay-token
    
$ ./target/release/substrate-overlay-token purge-chain --chain child --base-path /tmp/child -y
$ ./target/release/substrate-overlay-token --chain child --dave --validator --base-path /tmp/child --ws-port 9945
```

#### Start Bridge

```
$ git clone https://github.com/dmm-bclabs/substrate-overlay-token-bridge.git
$ cd substrate-overlay-token-bridge
    
$ yarn install
$ yarn run dev
```

### Start Parent Web UI

```
$ git clone https://github.com/dmm-bclabs/substrate-overlay-token-ui.git
$ cd substrate-overlay-token-ui
    
$ yarn install
$ PORT=8000 yarn run dev
```

### Start Child Web UI

```
$ cd substrate-overlay-token-ui
    
$ PORT=8001 yarn run dev
```

### Ethereum <-> Substrate

![Demo 2 Architecture](docs/BridgeArchitectureRopsten.svg)

#### Start Substrate Chain

```
$ git clone https://github.com/dmm-bclabs/substrate-overlay-token.git
$ cd substrate-overlay-token
    
$ ./scripts/build.sh
$ cargo build --release
    
$ ./target/release/substrate-overlay-token purge-chain --chain parent --base-path /tmp/parent -y
$ ./target/release/substrate-overlay-token --chain parent --charlie --validator --base-path /tmp/parent --ws-port 9944
```

#### Start Bridge

```
$ git clone https://github.com/dmm-bclabs/ethereum-overlay-token-bridge.git
$ cd ethereum-overlay-token-bridge
    
$ yarn install
    
$ cp config/setting-default.json config/setting.json
# edit URL, OverlayToken Address and Private Key
$ vi config/setting.json
    
$ node index.js
```

- Create setting.json file, and edit URL of Ethereum testnet, the address of the overlay token contract, and the private key of the owner of the overlay token contract.
- For URL of Etheruem testnet, create account at infura.io.

#### Start Ethereum Web UI

```
$ git clone https://github.com/dmm-bclabs/ethereum-overlay-token-ui.git
$ cd ethereum-overlay-token-ui
    
$ yarn install
$ yarn start
```

#### Start Substrate Web UI

```
$ git clone https://github.com/dmm-bclabs/substrate-overlay-token-ui.git
$ cd substrate-overlay-token-ui
    
$ yarn install
$ PORT=8000 yarn run dev
```

- Execute init and setParent on the token segment.
- At setParent, fill the amount of token supply on the Ethereum contract as totalSupply.

## License

[LICENSE](./LICENSE)