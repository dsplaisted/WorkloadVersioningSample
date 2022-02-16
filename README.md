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

## Proposed dependency graph for .NET 6 and 7

```mermaid
graph TD;

      subgraph workload.emscripten.net6
      microsoft-net-sdk6-emscripten(["microsoft-net6-sdk-emscripten<BR><I>(abstract)</I>"])-->Microsoft.NET.Runtime.6.Emscripten.Node[Emscripten.Node.6];
      Microsoft.NET.Runtime.6.Emscripten.Node-->|alias|Microsoft.NET.Runtime.Emscripten.Node.v6["Emscripten.Node v6.0.0"]
      microsoft-net-sdk6-emscripten-->Microsoft.NET.Runtime.6.Emscripten.Python[Emscripten.Python.6];
      Microsoft.NET.Runtime.6.Emscripten.Python-->|alias|Microsoft.NET.Runtime.Emscripten.Python.v6["Emscripten.Python v6.0.0"]
      microsoft-net-sdk6-emscripten-->Microsoft.NET.Runtime.6.Emscripten.Sdk[Emscripten.Sdk.6];
      Microsoft.NET.Runtime.6.Emscripten.Sdk-->|alias|Microsoft.NET.Runtime.Emscripten.Sdk.v6["Emscripten.Sdk v6.0.0"]
      end
      
      subgraph workload.emscripten.net7
      microsoft-net-sdk7-emscripten(["microsoft-net7-sdk-emscripten<BR><I>(abstract)</I>"])-->Microsoft.NET.Runtime.7.Emscripten.Node[Emscripten.Node.7];
      Microsoft.NET.Runtime.7.Emscripten.Node-->|alias|Microsoft.NET.Runtime.Emscripten.Node["Emscripten.Node v7.0.0"]
      microsoft-net-sdk7-emscripten-->Microsoft.NET.Runtime.7.Emscripten.Python[Emscripten.Python.7];
      Microsoft.NET.Runtime.7.Emscripten.Python-->|alias|Microsoft.NET.Runtime.Emscripten.Python["Emscripten.Python v7.0.0"]
      microsoft-net-sdk7-emscripten-->Microsoft.NET.Runtime.7.Emscripten.Sdk[Emscripten.Sdk.7];
      Microsoft.NET.Runtime.7.Emscripten.Sdk-->|alias|Microsoft.NET.Runtime.Emscripten.Sdk["Emscripten.Sdk v7.0.0"]
      end

```
