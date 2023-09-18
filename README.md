# Rust Protobuf Networking  
Rust TCP communication over protobuf protocol.  

## Cloning Repo  
This repo contains three seperate code bases:  
- **Client**  
- **Server**  
- **Proto** for common proto files among server and client  

To clone the repo and required submodules:  
```bash
git clone --recurse-submodules https://github.com/AktugHakan/rust-protobuf-networking.git
```
If you cloned the repo without ```--recurse-modules``` flag, you can get the submodule using:  
```bash
git submodule init
git submodule update
```
# Building  
## Building Rust Server  
In server directory, edit the `build.rs` file according to your proto folder:  
- Change `&["/home/ahmet/Documents/RustProtobufNetworking/protobuf]"` to directory where you cloned the .proto files  
In server directory run
```bash
cargo build
```
to build the server program.  
Program is generated as ```target/debug/server```.

## Building Rust Client
In client directory, edit the `build.rs` file according to your proto folder:  
- Change `&["/home/ahmet/Documents/RustProtobufNetworking/protobuf]"` to directory where you cloned the .proto files  
In client directory run  
```bash
cargo build
```
to build the server program.  
Program is generated as ```target/debug/client```.

### Cross-Compiling
Rust program and its libraries are fully cross-compilable. To cross compile:  
1. Set up cross-compiler  
In .cargo/config.toml change the ```linker``` argument according to your toolchain.
2. Install target platform directives for rust using [rustup](https://rust-lang.github.io/rustup/cross-compilation.html)
3. Build  
Build the server program using:  
```bash
 cargo build --target=<your-target-platform>
```
To see supported target platforms check out [rustc Platform Support](https://doc.rust-lang.org/nightly/rustc/platform-support.html).  

#### Example: Cross-Compiling for Armv7:
1. Install a toolchain (Tested with [GNU Arm Toolchain](https://developer.arm.com/downloads/-/gnu-a))
2. Install the `armv7-unknown-linux-gnueabihf` target for rust using:
```bash
rustup target add armv7-unknown-linux-gnueabihf
```
3. Configure the .cargo/config.toml for your toolchain
```toml
[target.armv7-unknown-linux-gnueabihf]
linker = "arm-linux-gnueabihf-gcc"
rustflags = ["-C", "target-feature=+crt-static"]
```
4. Build the program with
```bash
cargo build --target=armv7-unknown-linux-gnueabihf
```

# Usage
1. Launch the server using  
```bash
cargo run
```
command in server directory  
2. Start the client using
```bash
cargo run <ip_address> <port>
```
If you are running the program on the same device, use 127.0.0.1 as IP address.  
The hardcoded port is 2001 for server.

## Commands  
After starting the client; if it connects successfully it will show a prompt `_> `. You can use commands:  
- **led on**: Enable LEDs
- **led off**: Disable LEDs
- **info**: Get server IP and Port
- **file <file_name>**: Request a file. If file exists in file_storage/ folder in the same directory as executable


