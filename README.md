# Use WasmEdge-QuickJS to send HTTP(s) requests from inside WASM

This devcontainer is configured to provide you a WasmEdge installation equipped with `wasmedge_rustls` plugin and a Rust 
toolchain with `wasm32-wasi` target to compile the latest WasmEdge-QuickJS.

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/wasm-outbound-http-examples/wasmedge-quickjs)


## Instructions for this devcontainer

Tested with WasmEdge-QuickJS commit [f4a4f884](https://github.com/second-state/wasmedge-quickjs/tree/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d), Rustc 1.74.1.

### Preparation

1. Open this repo in devcontainer, e.g. using Github Codespaces.
   Type or copy/paste following commands to devcontainer's terminal.

### Building

1. Clone WasmEdge-QuickJS repo:

```sh
git clone --depth=1 https://github.com/second-state/wasmedge-quickjs.git
```

2. `cd` into the folder of WasmEdge-QuickJS sources:

```sh
cd wasmedge-quickjs
```

3. Compile the WasmEdge-QuickJS interpreter:

```sh
cargo build --target wasm32-wasi --release
```

4. Copy `wasmedge_quickjs.wasm` file to current directory, thus it requires pure JS modules from `modules` directory in this source distribution to run:

```sh
cp target/wasm32-wasi/release/wasmedge_quickjs.wasm ./
```

5. Optionally you can optimize the WASM file to run faster with `wasmedgec` "compiler":

```sh
wasmedgec wasmedge_quickjs.wasm wasmedge_quickjs.wasm
```

This will override the original copy with optimized (and a 1.5 times larger) one.

### Test with WasmEdge runtime

```sh
wasmedge --dir .:. wasmedge_quickjs.wasm example_js/wasi_https_fetch.js
```

This test may take about 20 seconds. You can also try lots of other examples in `example_js` directory, especially 
[`wasi_http_fetch.js`](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/example_js/wasi_http_fetch.js) and  
[`wasi_http_server.js`](https://github.com/second-state/wasmedge-quickjs/blob/f4a4f884ca4f2d1f2cce629f8d903b1d0020fa6d/example_js/wasi_http_server.js).

### Finish

Perform your own experiments if desired.

---

<sub>Created for (wannabe-awesome) [list](https://github.com/vasilev/HTTP-request-from-inside-WASM)</sub>
