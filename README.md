# Rust Wasm Example

## Installation

Assuming you already have cargo installed:

```bash
cargo --version
```

Install [wasm-pack](https://rustwasm.github.io/wasm-pack/)

```bash
cargo install wasm-pack
```

Create a new Rust library project

```bash
cargo new --lib hello-wasm
```

Add these lines to your `cargo.toml`

```yaml
[lib]
crate-type=["cdylib"]

[dependencies]
wasm-bindgen = "0.2"
```

In your `lib.rs` add a simple example function that you want to test:

```rust
use wasm_bindgen::prelude::*;

#[wasm_bindgen]
pub fn add(a: i32, b: i32) -> i32 {
    a + b
}
```

Build the project using `wasm-pack` and target the web:

```bash
wasm-pack build --target web
```

Create a new `index.html` file to test this out and add the following js:

```html
<script type="module">
    import init, {add} from './pkg/hello_wasm.js';

    await init();

    console.log(add(1,2));
</script>
```

Serve the html page in a browser using python simple http server and open the console to see the result of calling the native Rust function via JS in the browser!

```
python3 -m http.server
```

## Further reading

Checkout the [MDN Compiling from Rust to WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly/Rust_to_Wasm) docs.