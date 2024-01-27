# rust-grpc-python-tonic

How to use a gRPC service defined using protocol buffers (protobuf) as an interface (I/F) between a server and a client, where the server - client can be written in: Python - Python, Python - Rust, Rust - Python or Rust code and Python code (using tonic).

In the example below we first have a Rust server and client exchange a message via gRPC, then we have python exchange a message via gRPC, then
you can have a python-client exchange a message via gRPC with a rust-server, or have a rust-client exchange a message via gRPC with a python-server.

## Rust server and client

[Step By Step Rust Tonic Tutorial](https://github.com/hyperium/tonic/blob/master/examples/helloworld-tutorial.md)

### Install Rust 

```bash
   curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
   source "$HOME/.cargo/env"
   rustup update
```

Within the main directory, the same level as `Cargo.toml`, do the following:

To run the server, run `cargo run --bin helloworld-server`. 

To run the client, run `cargo run --bin helloworld-client` in another terminal window.

You should see the request logged out by the server in its terminal window, as well as the response logged out by the client in its window.

```bash
(venv) helloworld-tonic % cargo run --bin helloworld-server
    Updating crates.io index
  Downloaded percent-encoding v2.3.0
  Downloaded fastrand v2.0.1
  Downloaded futures-core v0.3.29
  Downloaded futures-task v0.3.29
  .
  .
  .
   Compiling tonic v0.10.2
    Finished dev [unoptimized + debuginfo] target(s) in 36.61s
     Running `target/debug/helloworld-server`
Got a request: Request { metadata: MetadataMap { headers: {"te": "trailers", "content-type": "application/grpc", "user-agent": "tonic/0.10.2"} }, message: HelloRequest { name: "Tonic" }, extensions: Extensions }
Got a request: Request { metadata: MetadataMap { headers: {"content-type": "application/grpc", "te": "trailers", "grpc-accept-encoding": "identity, deflate, gzip", "user-agent": "grpc-python/1.59.2 grpc-c/36.0.0 (osx; chttp2)"} }, message: HelloRequest { name: "you" }, extensions: Extensions }
```

## Python server and client

[Step by Step Python gRPC tutorial](https://grpc.io/docs/languages/python/quickstart/)

```bash
$ python3 -m pip install --upgrade pip 
$ python3 -m pip install virtualenv # if not already done
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ pip install grpcio grpcio-tools
(venv) $ pip install protobuf
(venv) $ cd pythonapi
```
### Python as the server

```bash
(venv) python $ python greeter_server.py
Server started, listening on 50051
```

If you receive 
```bash
    import helloworld_pb2
ModuleNotFoundError: No module named 'helloworld_pb2'
```
its because you havent yet generated the gRPC Python files: 
```bash
helloworld_pb2.py       helloworld_pb2.pyi      helloworld_pb2_grpc.py
```
You do this by making the `.proto` file in the `/proto/` folder and using `grpc_tools.protoc` to read that file, `./proto/helloworld.proto` in our case if you are currently within the main `rust-grpc-python-tonic/` directory, and then running this command:
```bash
rust-grpc-python-tonic $  python -m grpc_tools.protoc -I./proto --python_out=./pythonapi --pyi_out=./pythonapi --grpc_python_out=./pythonapi ./proto/helloworld.proto
```
After this command you should see the 3 `helloworld` files above appear in the `./pythonapi` folder you directed them to

### Python as the client

If you have a server running, can be python or rust, in a separate terminal, you can ping that server as the client:

```bash
(venv) python $ python greeter_client.py
Will try to greet world ...
Greeter client received: Hello you!
```

### Python as the server Rust as the client

```bash
(venv) python $ python greeter_server.py
```

in another terminal,start rust as the client

```bash
(venv) rust-grpc-python-tonic $ cargo run --bin helloworld-client
```


## Directory structures

```bash
├── proto
│   └── helloworld.proto
├── pythonapi
│   ├── greeter_client.py
│   ├── greeter_server.py
├── src
│   ├── client.rs
│   ├── server.rs
│   ├── main.rs
├── build.rs
├── Cargo.toml

```
