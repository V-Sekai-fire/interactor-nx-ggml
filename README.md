# interactor-nx-ggml

A JIT-compiled Nx backend that lowers `Nx.Defn` expression graphs into ggml compute graphs on the CPU or Vulkan.

## What it is for

One compiler lowers a traced `defn` into a single ggml graph, cached by input signature, and eager tensor operations route through the same path. Gradients come from Nx's own differentiation of the expression graph, so the backend carries no autodiff code. An operation or type the compiler does not lower falls back to `Nx.Defn.Evaluator`. ggml is vendored by git subtree under `native/`, and `lean/` holds proofs of the lowering's algebraic claims; neither proofs nor tests are a runtime dependency.

## Build and test

```sh
mix deps.get
mix test
```

`mix compile` builds the NIF and ggml through CMake. To use it from another project:

```elixir
{:nx_ggml, git: "https://github.com/V-Sekai-fire/interactor-nx-ggml"}
```

## Licence

MIT. See [LICENSE](LICENSE). The vendored ggml carries its own MIT licence.
