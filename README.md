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

A blockchain is a public database of records, composed of blocks. Each blocks contains, a `creation timestamp`, the `block's data`, the `previous block hash` and the `current hash`.

```Go
type Block struct {
	Timestamp     int64
	Data          []byte
	PrevBlockHash []byte
	Hash          []byte
}
```

The blockchain is an array of blocks, this could be simplified as this :

```Go
type Blockchain struct {
	blocks []*Block
}
```

Off course, in order to persiste the data, this struct change in consequence.

## How to run it ?

### Build the project

Go to the repo path and build the project

```bash
$ go mod tidy && go build
```

### Run the cli

Run the CLI

```bash
$ ./go-blockchain
Usage:
  addblock -data BLOCK_DATA - add a block to the blockchain
  printchain - print all the blocks of the blockchain
```

And you should see the blockchain setup, starting by the genesis block generation and two simulated transaction, with proof of work process.

### Print chain content

```bash
$ ./go-blockchain printchain
No existing blockchain found. Creating a new one...
Mining the block containing "Genesis Block"
000000bdcd052450c2c0b9d71b4c25d2eb543d74f1b38f4c17b812d5f8512702

Prev. hash: 
Data: Genesis Block
Hash: 000000bdcd052450c2c0b9d71b4c25d2eb543d74f1b38f4c17b812d5f8512702
PoW: true
```

### Add new block to the blockchain

```bash
$ ./go-blockchain addblock -data "Send 1 BTC to John Smith"
Mining the block containing "Send 1 BTC to John Smith"
0000006f21aba63ef2de138ef697fb5344e10d42442aa2bf3ed9dcdf78b5831a

Success!
```

And print the chain once again

```bash
$ ./go-blockchain printchain
Prev. hash: 000000bdcd052450c2c0b9d71b4c25d2eb543d74f1b38f4c17b812d5f8512702
Data: Send 1 BTC to John Smith
Hash: 0000006f21aba63ef2de138ef697fb5344e10d42442aa2bf3ed9dcdf78b5831a
PoW: true

Prev. hash: 
Data: Genesis Block
Hash: 000000bdcd052450c2c0b9d71b4c25d2eb543d74f1b38f4c17b812d5f8512702
PoW: true
```

## Data persistence

In order to persist the data, I use `BoltDB` in a single db file to keep it simple. Like this we can reuse our blockchain.
