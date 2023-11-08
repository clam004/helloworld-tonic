

[Step By Step Rust Tonic Tutorial](https://github.com/hyperium/tonic/blob/master/examples/helloworld-tutorial.md)

How to use Protocol Buffers (protobuf) as an interface (I/F) between Rust code (using tonic) and Python code (using grpc)

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

## Install Rust 

1. You can install the nightly version of Rust using Rustup, which is a tool for managing Rust installations. 
   If you don't have Rustup installed, you can get it from the official website: https://rustup.rs/. 
   
   ```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   ```
   
2. Once you have Rustup, you can install the nightly version with the following command:

   ```bash
   rustup install nightly
   ```

3. Switch to the nightly version of Rust for your project:
   To use the nightly version of Rust for your project, navigate to your project directory and run the following command:

   ```bash
   rustup override set nightly
   ```

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