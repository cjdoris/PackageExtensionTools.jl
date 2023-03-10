# PackageExtensionTools

Julia introduced
[package extensions](https://docs.julialang.org/en/v1.10-dev/manual/code-loading/#man-extensions)
in v1.9. This package makes these extensions backwards-compatible to earlier Julia versions,
with zero overhead on new versions.

Internally, this uses
[Requires.jl](https://github.com/JuliaPackaging/Requires.jl)
on earlier versions.

## Usage

Supposing you have a package called `Foo`:

1. Set up package extensions for `Foo` as usual. This means adding `[weakdeps]` and
   `[extensions]` to `Project.toml` and adding extension code to `ext/`.

2. Add `PackageExtensionTools` as a dependency to `Foo`.

3. Add the following code to `src/Foo.jl`:
   ```julia
   using PackageExensionTools
   function __init__()
       @require_extensions
   end
   ```

That's it! Your package extensions will now be loaded as expected on any Julia version!
