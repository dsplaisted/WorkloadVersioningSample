# WorkloadVersioningSample

## Current wasm-tools dependency graph

```mermaid
  graph TD;
      subgraph Mono.ToolChain
      wasm-tools([wasm-tools])-->Microsoft.NET.Runtime.WebAssembly.Sdk[WebAssembly.Sdk];
      wasm-tools-->Microsoft.NETCore.App.Runtime.Mono.browser-wasm[Mono.browser-wasm];
      wasm-tools-->Microsoft.NETCore.App.Runtime.AOT.Cross.browser-wasm[AOT.Cross.browser-wasm];
      wasm-tools---->|extends|microsoft-net-runtime-mono-tooling;
      microsoft-net-runtime-mono-tooling(["microsoft-net-runtime-mono-tooling<BR><I>(abstract)</I>"])-->Microsoft.NET.Runtime.MonoAOTCompiler.Task[MonoAOTCompiler.Task];
      microsoft-net-runtime-mono-tooling-->Microsoft.NET.Runtime.MonoTargets.Sdk[MonoTargets.Sdk];
      end
      
      wasm-tools---->|extends|microsoft-net-sdk-emscripten;
      
      subgraph workload.emscripten
      microsoft-net-sdk-emscripten(["microsoft-net-sdk-emscripten<BR><I>(abstract)</I>"])-->Microsoft.NET.Runtime.Emscripten.Node[Emscripten.Node];
      microsoft-net-sdk-emscripten-->Microsoft.NET.Runtime.Emscripten.Python[Emscripten.Python];
      microsoft-net-sdk-emscripten-->Microsoft.NET.Runtime.Emscripten.Sdk[Emscripten.Sdk];
      end
```

### Workload packs

- **WebAssembly.Sdk**: Build logic for WASM / AOT
- **Mono.browser-wasm**: Mono browser-wasm runtime pack.  Not imported as SDK, but via KnownFrameworkReference or KnownRuntimePack items.
- **AOT.Cross.browser-wasm**: AOT Compiler EXE (mono-aot-cross.exe)
- **MonoAOTCompiler.Task**: Includes (only) the MonoAOTCompiler task
- **MonoTargets.Sdk**: Mono MSBuild logic and tasks shared between ios, android, and wasm
- **Emscripten.Node**: Includes Node
- **Emscripten.Python**: Includes Python
- **Emscripten.Sdk**: Includes Emscripten
