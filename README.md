# Go Blockchain

![GitHub Release](https://img.shields.io/github/v/release/oliv3340/go-blockchain)
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/oliv3340/go-blockchain/go-ci.yml)
![GitHub go.mod Go version](https://img.shields.io/github/go-mod/go-version/oliv3340/go-blockchain)

This project is a technical lab to learn how works a blockchain in `Golang`.

## Features supported

- Block definition and creation
- blockchain implementation
- proof of work feature

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

The the blockchain is an array of blocks

```Go
type Blockchain struct {
	blocks []*Block
}
```

## How to run it

### Step 1

Go to the repo path and build the project

```bash
$ go build
```

### Step 2

Run the binary previously created

```bash
$ go run go-blockchain
```
