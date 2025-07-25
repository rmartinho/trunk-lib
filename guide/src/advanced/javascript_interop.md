# JavaScript interoperability

Trunk will create the necessary JavaScript code to bootstrap and run the WebAssembly based application. It will also
include all JavaScript snippets generated by `wasm-bindgen` for interfacing with JavaScript functionality.

By default, functions exported from Rust, using `wasm-bindgen`, can be accessed in the JavaScript code through the global
variable `window.wasmBindings`. This behavior can be disabled, and the name can be customized. For more information
see the [`rust` asset type](../assets/index.md#rust).

## Order of initialization

The bindings will only be available and working when the application initialization has been completed.

If your WebAssembly application renders code into the web page/DOM tree, which then calls from JavaScript into the
WebAssembly application, then this will not be an issue, as the application is already initialized.

However, if you want to call into the WebAssembly application from, for example, the `index.html` file itself, then
you must delay that call until the application is started.

This can be ensured by executing that code with the `TrunkApplicationStartup` event. Also see
[Startup Event](startup_event.md). 
