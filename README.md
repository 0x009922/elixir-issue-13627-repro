# elixir-issue-13627-repro

This is a reproduction for https://github.com/elixir-lang/elixir/issues/13627

I created this project by running `mix new sample_project` and than only adding a single Hex dependency in `mix.exs`:

```elixir
{:nimble_options, "~> 1.1.1"}
```

How to reproduce the error: open `iex` and run

```
iex(1)> Mix.install([{:sample_project, path: "."}])
Resolving Hex dependencies...
** (MatchError) no match of right hand side value: :error
    (hex 2.1.1) lib/hex/solver/package_lister.ex:47: anonymous fn/4 in Hex.Solver.PackageLister.dependencies_as_incompatibilities/4
    (elixir 1.16.3) lib/enum.ex:1700: Enum."-map/2-lists^map/1-1-"/2
    (hex 2.1.1) lib/hex/solver/package_lister.ex:46: Hex.Solver.PackageLister.dependencies_as_incompatibilities/4
    (hex 2.1.1) lib/hex/solver/solver.ex:123: Hex.Solver.Solver.choose_package_version/1
    (hex 2.1.1) lib/hex/solver/solver.ex:25: Hex.Solver.Solver.solve/2
    (hex 2.1.1) lib/hex/solver.ex:64: Hex.Solver.run/5
    (hex 2.1.1) lib/hex/remote_converger.ex:69: Hex.RemoteConverger.run_solver/5
    iex:1: (file)
```

Or add this project as a `path` dependency to any other project - the error remains the same.

