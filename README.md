[![Status](https://travis-ci.org/rust-verge/rust-vergecore-rpc.png?branch=master)](https://travis-ci.org/rust-verge/rust-vergecore-rpc)

# Rust RPC client for Verge Core JSON-RPC 

This is a Rust RPC client library for calling the Verge Core JSON-RPC API. It provides a layer of abstraction over 
[rust-jsonrpc](https://github.com/apoelstra/rust-jsonrpc) and makes it easier to talk to the Verge JSON-RPC interface 

This git package compiles into two crates.
1. [vergecore-rcp](https://crates.io/crates/vergecore-rpc) - contains an implementation of an rpc client that exposes 
the Verge Core JSON-RPC APIs as rust functions.

2. [vergecore-rpc-json](https://crates.io/crates/vergecore-rpc-json) -  contains rust data structures that represent 
the json responses from the Verge Core JSON-RPC APIs. vergecore-rcp depends on this.

# Usage
Given below is an example of how to connect to the Verge Core JSON-RPC for a Verge Core node running on `localhost`
and print out the hash of the latest block.

It assumes that the node has password authentication setup, the RPC interface is enabled at port `20102` and the node
is set up to accept RPC connections. 

```rust
extern crate vergecore_rpc;

use vergecore_rpc::{Auth, Client, RpcApi};

fn main() {

    let rpc = Client::new("http://localhost:20102".to_string(),
                          Auth::UserPass("<FILL RPC USERNAME>".to_string(),
                                         "<FILL RPC PASSWORD>".to_string())).unwrap();
    let best_block_hash = rpc.get_best_block_hash().unwrap();
    println!("best block hash: {}", best_block_hash);
}
```

See `client/examples/` for more usage examples. 