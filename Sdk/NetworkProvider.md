# Network Provider

The CashScript SDK needs to connect to the BCH network to perform certain operations, like retrieving the contract's balance, or sending transactions. By default the network provider is an ``ElectrumNetworkProvider``, however for local development it is recommended to use a ``MockNetworkProvider``.

>**TIP**
>
>CashScript NetworkProviders have a standardized interface, this allows different network providers to be used by the SDK and makes it easy to swap out dependencies.

## Interface NetworkProvider

### Network

```javascript
type Network = 'mainnet' | 'chipnet' | 'mocknet' | 'testnet3' | 'testnet4' | 'regtest';
```

The network parameter can be one of 6 different options.

#### Example

```javascript
const connectedNetwork = provider.network;
```

### getUtxos()

```javascript
async provider.getUtxos(address: string): Promise<Utxo[]>;
```

Returns all UTXOs on specific address. Both confirmed and unconfirmed UTXOs are included.

```javascript
interface Utxo {
  txid: string;
  vout: number;
  satoshis: bigint;
  token?: TokenDetails;
}

interface TokenDetails {
  amount: bigint;
  category: string;
  nft?: {
    capability: 'none' | 'mutable' | 'minting';
    commitment: string;
  };
}
```

#### Example

```javascript
const userUtxos = await provider.getUtxos(userAddress)
```

### getBlockHeight()

```javascript
async provider.getBlockHeight(): Promise<number>;
```

Get the current blockHeight.

#### Example

```javascript
const currentBlockHeight = await provider.getBlockHeight()
```

### getRawTransaction()

```javascript
async provider.getRawTransaction(txid: string): Promise<string>;
```

Retrieve the Hex transaction details for a given transaction ID.

#### Example

```javascript
const rawTransaction = await provider.getRawTransaction(txid)
```

### sendRawTransaction()

```javascript
async provider.sendRawTransaction(txHex: string): Promise<string>;
```

Broadcast a raw hex transaction to the network.

#### Example

```javascript
const txId = await provider.sendRawTransaction(txHex)
```

## Custom NetworkProviders

A big strength of the NetworkProvider setup is that it allows you to implement custom providers. So if you want to use a new or different BCH indexer for network information, it is simple to add support for it by creating your own ``NetworkProvider`` adapter by implementing the [NetworkProvider interface](https://github.com/CashScript/cashscript/blob/master/packages/cashscript/src/network/NetworkProvider.ts).

You can create a PR to add your custom ``NetworkProvider`` to the CashScript codebase to share this functionality with others. It is required to have basic automated tests for any new ``NetworkProvider``.