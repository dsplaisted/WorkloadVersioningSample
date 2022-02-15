# WorkloadVersioningSample

# Current wasm-tools dependency graph

```mermaid
  graph TD;
      wasm-tools([wasm-tools])-->Microsoft.NET.Runtime.WebAssembly.Sdk[WebAssembly.Sdk];
      wasm-tools-->Microsoft.NETCore.App.Runtime.Mono.browser-wasm[Mono.browser-wasm];
      wasm-tools-->Microsoft.NETCore.App.Runtime.AOT.Cross.browser-wasm[AOT.Cross.browser-wasm];
      wasm-tools---->microsoft-net-runtime-mono-tooling;
      wasm-tools---->microsoft-net-sdk-emscripten;
      microsoft-net-runtime-mono-tooling([microsoft-net-runtime-mono-tooling])-->Microsoft.NET.Runtime.MonoAOTCompiler.Task[MonoAOTCompiler.Task];
      microsoft-net-runtime-mono-tooling-->Microsoft.NET.Runtime.MonoTargets.Sdk[MonoTargets.Sdk];
      microsoft-net-sdk-emscripten([microsoft-net-sdk-emscripten])-->Microsoft.NET.Runtime.Emscripten.Node[Emscripten.Node];
      microsoft-net-sdk-emscripten-->Microsoft.NET.Runtime.Emscripten.Python[Emscripten.Python];
      microsoft-net-sdk-emscripten-->Microsoft.NET.Runtime.Emscripten.Sdk[Emscripten.Sdk];
```


### WebAssembly.Sdk

Build logic for WASM / AOT

### Mono.browser-wasm

Mono browser-wasm runtime pack

### AOT.Cross.browser-wasm

AOT Compiler EXE (mono-aot-cross.exe)

### MonoAOTCompiler.Task

Includes (only) the MonoAOTCompiler task

### MonoTargets.Sdk

Mono MSBuild logic and tasks shared between ios, android, and wasm

### Emscripten.Node

Includes Node and MSBuild .props file pointing to it

### Emscripten.Python

Includes Python and MSBuild .props file pointing to it

### Emscripten.Sdk

Includes Emscripten and MSBuild .props file pointing to it.
