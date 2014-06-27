# Docile

[![Build Status](https://travis-ci.org/MichaelHatherly/Docile.jl.svg?branch=master)](https://travis-ci.org/MichaelHatherly/Docile.jl)
[![Coverage Status](https://coveralls.io/repos/MichaelHatherly/Docile.jl/badge.png)](https://coveralls.io/r/MichaelHatherly/Docile.jl)

[Julia](www.julialang.org) package documentation system. [Mailing list discussion](https://groups.google.com/forum/#!topic/julia-users/k_SzJxcAoqA).

*Docile* extracts doc strings from source code to produce package
documentation. Output formats include markdown, html, and the standard
julia help system file. Help for packages can then be viewed at the REPL
and inline in LightTable and IJulia.

HTML files are generated using [Markdown.jl](https://github.com/one-more-minute/Markdown.jl).

The Docile documentation generated by this package can be found [here](https://github.com/MichaelHatherly/Docile.jl/blob/master/doc/help/docs.md).

## Install

*Docile* in not registered currently. So clone it using:

    julia> Pkg.clone("https://github.com/MichaelHatherly/Docile.jl")

To view help from the REPL (or other interactive environment) add the
following to the top of your `.juliarc.jl` file:

    import Docile
    Docile.patch!()

`patch!` modifies the builtin help system to allow external help files
to be loaded along with the help file included with Julia.

After adding those lines when you start Julia again you should see

    INFO: Patching Base.Help.init_help()...

## Usage

Viewing documentation for packages should work as it does for `Base`.

    julia> apropos("Docile")
    INFO: Loading help data...
    Docile.remove(package::String)
    Docile.html(package::String,docs::Vector{Doc})
    Docile.helpdb(package::String,docs::Vector{Doc})
    Docile.build(package::String,config::Dict)
    Docile.patch!()
    Docile.Doc{category}
    Docile.init(package::String)
    Docile.Docile
    Docile.plain(package::String,docs::Vector{Doc})
    Docile.@doc_mstr(text)

    help?> Docile.build
    Docile.build(package::String,config::Dict)

       Extract doc strings from all source files in `package`. Generate
       formatted documentation using the settings specified in `config`.

To document a package first initialise it using

    julia> Docile.init(PACKAGE_NAME)

This will create a config file `doc/docile.jl` in the package's
directory. To generate documentation for the package use the following
from the command line after `cd`ing into the `doc/` folder.
`$ julia docile.jl`. This builds the complete documentation for the package.

To create documentation from the Julia REPL use

    julia> using Docile
    julia> Docile.build(PACKAGE_NAME, [:output => [plain, html, helpdb]])

This will create plain (markdown-style), html, and helpdb files
containing the doc strings from the package.

## Doc string format

The doc strings are formatted using Markdown syntax. A doc string
documents the `function`, `macro`, `module`, `type`, or `global` that
appears directly afterward.

```julia
"""
Module docs go here...
"""
module Foo

"""
Doc string content goes here.
"""
function foo(x)
    # ...
end

end
```

## Feedback

Any thoughts, requests, or PRs are welcome.

## Issues list

* [#762](https://github.com/JuliaLang/julia/issues/762)
* [#1619](https://github.com/JuliaLang/julia/pull/1619)
* [#3407](https://github.com/JuliaLang/julia/issues/3407)
* [#3988](https://github.com/JuliaLang/julia/issues/3988)
* [#4579](https://github.com/JuliaLang/julia/issues/4579)
* [#5200](https://github.com/JuliaLang/julia/issues/5200)
* and elsewhere on the mailing lists.
