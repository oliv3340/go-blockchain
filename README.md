# Go Blockchain

![GitHub Release](https://img.shields.io/github/v/release/oliv3340/go-blockchain)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/oliv3340/go-blockchain/go-ci.yml?branch=main)
![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/oliv3340/go-blockchain)

Blockchain project build in `Go`.

## How to run it

### Build the package 

```bash
$ go build
```

### Run it

```bash
$ go run go-blockchain
```

## What is a blockchain

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

The the blockchain is an array of blocks

```Go
type Blockchain struct {
	blocks []*Block
}
```
