# helloworld-tonic

How to use Protocol Buffers (protobuf) as an interface (I/F) between Rust code (using tonic) and Python code (using grpc)

[Step By Step Rust Tonic Tutorial](https://github.com/hyperium/tonic/blob/master/examples/helloworld-tutorial.md)


## Install Rust 

```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   source "$HOME/.cargo/env"
   rustup update
```

## Rust server and client

Within the main directory, the same level as `Cargo.toml`, do the following:

To run the server, run `cargo run --bin helloworld-server`. 

To run the client, run `cargo run --bin helloworld-client` in another terminal window.

You should see the request logged out by the server in its terminal window, as well as the response logged out by the client in its window.











## Build

```bash
$ python setup.py develop
```

### Optional

```bash
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ python setup.py --help-commands # complete list of available commands for your specific package, ie python setup.py build etc. 
(venv) $ python setup.py develop # changes you make to the package's source code will immediately affect the installed package
```

## Testing

```bash
$ python python_client/client.py
```


## Directory structures

```bash
├── setup.py
├── proto
│   └── helloworld.proto
├── rust_server
│   ├── Cargo.toml
│   ├── src
│   │   ├── main.rs
│   │   └── helloworld
│   │       └── mod.rs
└── python_client
    └── client.py
```