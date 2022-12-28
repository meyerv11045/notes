# Julia

## Setup

1. `brew install --cask julia`
    - `brew uninstall --cask julia` if upgrading versions and previous installation already exists
2. `julia --version` should be latest version
3. Enter pkg in the julia repl `]`
4. `activate env/project_name` to setup an environment for your project
5. `status` to see if any packages need to be installed (if so, run `instantiate`- should only have to do this once per project)

## Development

- When developing a file or pkg and wanting to test its functionality in the repl, can use the `Revise` pkg to prevent the need from re-importing everytime you make a change to the file/pkg

- `using Revise` in the repl

- `using YourPkg` or `includet('myfile.jl')`

    

## Macros

- [YT video](https://www.youtube.com/watch?v=e6LGMeoQhfs)
- macros work on pieces of julia code vs. functions work on values
    - julia code is represented as a data structure itself

## Syntax Tricks

### Unpack Arguments from array into function

- `f(args...)`
- [link](https://discourse.julialang.org/t/unpack-arguments-from-an-array-into-function/29656)

### do-block syntax

``` julia
map([A, B, C]) do x
    if x < 0 && iseven(x)
        return 0
    elseif x == 0
        return 1
    else
        return x
    end
end

# cleaner version of 

map(x->begin
           if x < 0 && iseven(x)
               return 0
           elseif x == 0
               return 1
           else
               return x
           end
       end,
    [A, B, C])
```

## Flux

- [Flux in 60 minutes](https://fluxml.ai/tutorialposts/2020-09-15-deep-learning-flux/)
- 
