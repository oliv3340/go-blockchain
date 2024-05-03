# Go Blockchain

![GitHub Release](https://img.shields.io/github/v/release/oliv3340/go-blockchain)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/oliv3340/go-blockchain/go-ci.yml)
![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/oliv3340/go-blockchain)

This project is a technical lab to learn how works a blockchain in `Golang`.

## Features supported

- Block definition and creation
- Blockchain implementation
- Proof of work feature
- Persistence data using BoltDB

## What is a blockchain ?

> **Note** : this is a simplified explanation

A blockchain is a public database of records,
composed of blocks. Each blocks contains,
a `creation timestamp`,
the `block's data: a transaction`,
the `previous block hash` and the `current hash`.

```Go
type Block struct {
  Timestamp     int64
  Data          []byte
  PrevBlockHash []byte
  Hash          []byte
}
```

The blockchain is an array of blocks,
this could be simplified as this :

```Go
type Blockchain struct {
  blocks []*Block
}
```

Off course, in order to persiste the data,
this struct change in consequence.

## How to run it ?

### Build the project

Go to the repo path and build the project

```bash
go mod tidy && go build
```

### Run the cli

Run the CLI

```bash
$ ./go-blockchain
Usage:
  getbalance -address ADDRESS - Get balance of ADDRESS
  createblockchain -address ADDRESS - Create a blockchain and send genesis block reward to ADDRESS
  printchain - Print all the blocks of the blockchain
  send -from FROM -to TO -amount AMOUNT - Send AMOUNT of coins from FROM address to TO
```

And you should see the blockchain setup,
starting by the genesis block generation and two simulated
transaction, with proof of work process.

### Create the blockchain

```bash
./go-blockchain createblockchain -address john
```

Output :

```bash
00000055ab36d4542da2198662c2d752f689f8b4a89d4cc4b55e885da764a737

Done!
```

### Get balance

```bash
./go-blockchain getbalance -address john
```

Output :

```bash
Balance of 'john': 10
```

### Send tokens

```bash
./go-blockchain send -from john -to smith -amount 4
```

Example :

```bash
./go-blockchain getbalance -address john
Balance of 'john': 10

./go-blockchain getbalance -address smith
Balance of 'smith': 0

./go-blockchain send -from john -to smith -amount 4
000000a7a55b7854f6fecf24b7e634787b8ed4854be84f892331ecaa0e1c3e8d

Success!

./go-blockchain getbalance -address john
Balance of 'john': 6

./go-blockchain getbalance -address smith
Balance of 'smith': 4
```

### Print chain content

```bash
./go-blockchain printchain
```

Output :

```bash
Prev. hash: 000000af9662d14ae94b6afa5ca8073c869b8aa9ad69546b0163c935ace53231
Hash: 0000006e2613aa583d72f96d588267cf3d7889739ff7a8d958d9914a7890079a
PoW: true

Prev. hash: 000000ebdcde39166d2bf314807bce4305e8cd3f5f134c2be1308e441754b49b
Hash: 000000af9662d14ae94b6afa5ca8073c869b8aa9ad69546b0163c935ace53231
PoW: true

Prev. hash: 000000b8b4d4ba862ffb921e91d226b92a4db891eda85c4f8ab9be921da8af1a
Hash: 000000ebdcde39166d2bf314807bce4305e8cd3f5f134c2be1308e441754b49b
PoW: true

Prev. hash: 00000055ab36d4542da2198662c2d752f689f8b4a89d4cc4b55e885da764a737
Hash: 000000b8b4d4ba862ffb921e91d226b92a4db891eda85c4f8ab9be921da8af1a
PoW: true

Prev. hash:
Hash: 00000055ab36d4542da2198662c2d752f689f8b4a89d4cc4b55e885da764a737
PoW: true
```

## Proof of Work

Proof of work trigger when a block is closed and before a new one can be open.
It can be resume by `solving the Hash` which
mean finding the new available hash possible for a new block.

BTC use [Hashcash](https://en.wikipedia.org/wiki/Hashcash) proof of work alogrythm.

### How it's work

It can be simplified like this :

- Take some publicly known data (in case of Bitcoin, it’s block headers).
- Add a counter to it. The counter starts at 0.
- Get a hash of the data + counter combination.
- Check that the hash meets certain requirements.
  - If it does, you’re done.
  - If it doesn’t, increase the counter and repeat the steps 3 and 4.

## Data persistence

In order to persist the data, I use `BoltDB` in a single db file to keep it
simple. Like this we can reuse our blockchain.

## TODO

I still need to :

- implement addresses and wallet
- implement network
