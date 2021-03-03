# Removing a dependency removes compat for test dependencies

Happens on MacOS with Julia 1.5.3 or 1.6 rc1.

Reproduction:

```bash
git clone https://github.com/ericphanson/TestPkg.jl
cd TestPkg.jl
cat Project.toml
julia --project=. -e "using Pkg; Pkg.rm(\"DataFrames\")"
cat Project.toml
```
which gives
```bash
❯ git clone https://github.com/ericphanson/TestPkg.jl
cd TestPkg.jl
cat Project.toml
julia --project=. -e "using Pkg; Pkg.rm(\"DataFrames\")"
cat Project.toml
Cloning into 'TestPkg.jl'...
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 10 (delta 2), reused 10 (delta 2), pack-reused 0
Unpacking objects: 100% (10/10), done.
name = "TestPkg"
uuid = "37f6bc05-9e90-43d5-90c6-4d69d7097606"
authors = ["Eric Hanson <5846501+ericphanson@users.noreply.github.com>"]
version = "0.1.0"

[deps]
DataFrames = "a93c6f00-e57d-5684-b7b6-d8193f3e46c0"

[compat]
Aqua = "0.5"
DataFrames = "0.22"

[extras]
Aqua = "4c88cf16-eb10-579e-8560-4a9242c79595"

[targets]
test = ["Aqua"]
    Updating `~/TestPkg.jl/Project.toml`
  [a93c6f00] - DataFrames v0.22.5
    Updating `~/TestPkg.jl/Manifest.toml`
  [324d7699] - CategoricalArrays v0.9.3
  [34da2185] - Compat v3.25.0
  [a8cc5b0e] - Crayons v4.0.4
  [9a962f9c] - DataAPI v1.6.0
  [a93c6f00] - DataFrames v0.22.5
  [864edb3b] - DataStructures v0.18.9
  [e2d170a0] - DataValueInterfaces v1.0.0
  [59287772] - Formatting v0.4.2
  [41ab1584] - InvertedIndices v1.0.0
  [82899510] - IteratorInterfaceExtensions v1.0.0
  [682c06a0] - JSON v0.21.1
  [e1d29d7a] - Missings v0.4.5
  [bac558e1] - OrderedCollections v1.4.0
  [69de0a69] - Parsers v1.0.15
  [2dfb63ee] - PooledArrays v1.2.1
  [08abe8d2] - PrettyTables v0.11.1
  [189a3867] - Reexport v1.0.0
  [a2af1166] - SortingAlgorithms v0.3.1
  [856f2bd8] - StructTypes v1.4.0
  [3783bdb8] - TableTraits v1.0.0
  [bd369af6] - Tables v1.3.2
  [0dad84c5] - ArgTools
  [56f22d72] - Artifacts
  [2a0f44e3] - Base64
  [ade2ca70] - Dates
  [8bb1440f] - DelimitedFiles
  [8ba89e20] - Distributed
  [f43a241f] - Downloads
  [9fa8497b] - Future
  [b77e0a4c] - InteractiveUtils
  [b27032c2] - LibCURL
  [76f85450] - LibGit2
  [8f399da3] - Libdl
  [37e2e46d] - LinearAlgebra
  [56ddb016] - Logging
  [d6f4376e] - Markdown
  [a63ad114] - Mmap
  [ca575930] - NetworkOptions
  [44cfe95a] - Pkg
  [de0858da] - Printf
  [3fa0cd96] - REPL
  [9a3f8284] - Random
  [ea8e919c] - SHA
  [9e88b42a] - Serialization
  [1a1011a3] - SharedArrays
  [6462fe0b] - Sockets
  [2f01184e] - SparseArrays
  [10745b16] - Statistics
  [fa267f1f] - TOML
  [a4e569a6] - Tar
  [8dfed614] - Test
  [cf7118a7] - UUIDs
  [4ec0a83e] - Unicode
  [deac9b47] - LibCURL_jll
  [29816b5a] - LibSSH2_jll
  [c8ffd9c3] - MbedTLS_jll
  [14a3606d] - MozillaCACerts_jll
  [83775a58] - Zlib_jll
  [8e850ede] - nghttp2_jll
name = "TestPkg"
uuid = "37f6bc05-9e90-43d5-90c6-4d69d7097606"
authors = ["Eric Hanson <5846501+ericphanson@users.noreply.github.com>"]
version = "0.1.0"

[extras]
Aqua = "4c88cf16-eb10-579e-8560-4a9242c79595"

[targets]
test = ["Aqua"]
```

No more compat for Aqua!
