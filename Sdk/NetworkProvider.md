# Network Provider

The CashScript SDK needs to connect to the BCH network to perform certain operations, like retrieving the contract's balance, or sending transactions. By default the network provider is an ``ElectrumNetworkProvider``.

## ElectrumNetworkProvider

The ElectrumNetworkProvider uses [electrum-cash](https://www.npmjs.com/package/electrum-cash) to connect to the BCH network. Both network and electrum parameters are optional, and they default to mainnet and a 2-of-3 ElectrumCluster with a number of reliable electrum servers.

```Typescript
new ElectrumNetworkProvider(network?: Network, electrum?: ElectrumCluster)
```

>**NOTE**
>
>In some cases it might be desirable to overwrite the 2-of-3 ElectrumCluster default to use only a 1-of-1 cluster because of network latency.

### Network

```Typescript
type Network = 'mainnet' | 'testnet3' | 'testnet4' | 'chipnet' | 'regtest';
```

The network parameter can be one of 5 different options.

#### Example

```Typescript
const provider = new ElectrumProvider('chipnet');
```

### getUtxos

```Typescript
async provider.getUtxos(address: string): Promise<Utxo[]>;
```

Returns all UTXOs on specific address. Both confirmed and unconfirmed UTXOs are included.

```Typescript
interface Utxo {
  txid: string;
  vout: number;
  satoshis: bigint;
  token?: TokenDetails;
}
```

#### Example

```Typescript
const userUtxos = await provider.getUtxos(userAddress)
```

### getBlockHeight

```Typescript
async provider.getBlockHeight(): Promise<number>;
```

Get the current blockHeight.

#### Example

```Typescript
const currentBlockHeight = await provider.getBlockHeight()
```

### getRawTransaction

```Typescript
async provider.getRawTransaction(txid: string): Promise<string>;
```

Retrieve the Hex transaction details for a given transaction ID.

#### Example

```Typescript
const rawTransaction = await provider.getRawTransaction(txid)
```

### sendRawTransaction

```Typescript
async provider.sendRawTransaction(txHex: string): Promise<string>;
```

Broadcast a raw hex transaction to the network.

#### Example

```Typescript
const txId = await provider.sendRawTransaction(txHex)
```

### performRequest

Perform an arbitrary electrum request, refer to the docs at [electrum-cash-protocol](https://electrum-cash-protocol.readthedocs.io/en/latest/).

#### Example

```Typescript
const verbose = true // get parsed transaction as json result
const txId = await provider.performRequest('blockchain.transaction.get', txid, verbose)
```

## Advanced Options

All network functionality that the CashScript SDK needs is encapsulated in a network provider. This allows different network providers to be used and makes it easy to swap out dependencies.

### MockNetworkProvider

```Typescript
new MockNetworkProvider()
```

The ``MockNetworkProvider`` is a special network provider that allows you to evaluate transactions locally without interacting with the Bitcoin Cash network. This is useful when writing automated tests for your contracts, or when debugging your contract locally. You can read more about the ``MockNetworkProvider`` and automated tests on the [testing setup](/Sdk/TestingSetup.md) page.

#### Example

```Typescript
const provider = new MockNetworkProvider();
const newUtxo = randomUtxo({satoshis: 10_000n})
provider.addUtxo(contractAddress, newUtxo);
```

### Other NetworkProviders

There are two alternative network providers implemented:

- ``FullStackNetworkProvider``: uses [FullStack.cash](https://fullstack.cash/)' infrastructure to connect to the BCH network.
- ``BitcoinRpcNetworkProvider``: uses a direct connection to a Bitcoin Cash node.

Currently neither supports CashTokens, so it is recommended to use the ``ElectrumNetworkProvider``.

### Custom NetworkProviders

A big strength of the NetworkProvider setup is that it allows you to implement custom providers. So if new BCH libraries are created in the future, it is simple to use them with CashScript. Custom NetworkProviders also potentially enables the CashScript SDK to be used with other (partially) compatible networks, such as BTC or BSV.

>**INFO**
>
>To implement a Custom NetworkProvider, refer to the [NetworkProvider interface](https://github.com/CashScript/cashscript/blob/master/packages/cashscript/src/network/NetworkProvider.ts).