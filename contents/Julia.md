#  Julia

1. Array index starts from 1
2. Space matters
   ```
   a = [1, 1, 1] # 3 element vector
   a = [1 1 1+1] # 1, 3 matrix
   a = [1 1 1 +1] # 1, 4 matrix
   ```
3. Initialization
   ```
   a = Int[] is the same as a = Vector{Int}()
   a = Vector{Float64}[] is the same as a = Vector{Vector{Float64}}()
   ```
4. `...` is the splat operator
   ```
   a = [[1, 1], [1, 2], [1, 4]] # 3 element vector
   vcat(a...) # 6 element vector
   ```
5. [Variable Scoping](https://docs.julialang.org/en/v1/manual/variables-and-scoping/)
   ```
   i = 0 # defined in global
   while i < 5
       i += 1     # ERROR: UndefVarError: `i` not defined
       println(i)
   end
   ```
   A fix is to change all global variable definitions into local definitions by wrapping the code in a let block or function.
   ```
   let
      i = 0
      while i < 5
          i += 1     # Now outer `i` is defined in the inner scope of the while loop
          println(i)
      end
   end
   ```
6. [Measure performance with @time and pay attention to memory allocation](https://docs.julialang.org/en/v1/manual/performance-tips/#Measure-performance-with-[@time](@ref)-and-pay-attention-to-memory-allocation)
   * in `REPL` mode
   * heap allocation, for either mutable objects or for creating/growing variable-sized containers (such as Array or Dict, strings, or "type-unstable" objects whose type is only known at runtime).
   * in stack, immutable values like numbers (except bignums), tuples, and immutable structs can be stored much more cheaply
   * [reset elements in a matrix with less memory allocation](https://discourse.julialang.org/t/how-to-reset-the-elements-of-a-3x3-matrix-without-any-memory-allocation/100257/2)
7. [Type inference](https://docs.julialang.org/en/v1/manual/performance-tips/#Type-inference)
   * In many languages with optional type declarations, adding declarations is the principal way to make code run faster. This is not the case in Julia. In Julia, the compiler generally knows the types of all function arguments, local variables, and expressions. However, there are a few specific instances where declarations are helpful.
   * [tools](https://docs.julialang.org/en/v1/manual/performance-tips/#tools)
   * type instability, use @code_warntype in `REPL` mode
   * [Cthulhu](https://github.com/JuliaDebug/Cthulhu.jl)
   * A thorough [benckmark.jl](https://github.com/JuliaCI/BenchmarkTools.jl) 
8. Julia is not object-oriented, [see](https://stackoverflow.com/questions/76674552/what-is-the-julia-equivalent-to-classes-and-instance-variables-in-java)
9. `vcat(a, b)` is the same as `[a; b]`, but they both create a new array in memory and can be slow. `append!(a, b)` is faster, only modifies existing memory
    ```
    a = Vector{Vector{Float64}}()
    for i in 1:3
        b = [[0.0, 0.0], [0.0, 0.2]]
        println(typeof(b)) # Vector{Vector{Float64}}
        # a = [a; b] # slower
        # a = vcat(a, b) # slower
        append!(a, b) # faster 
    end
    println(a)
    println(typeof(a))
    ```
11. push!() is also fast
    ```
    a = Vector{Vector{Float64}}()
    for i in 1:3
        b = [1., 2., 3.]
        println(typeof(b)) # Vector{Float64}
        push!(a, b)
    end
    println(a)
    println(typeof(a))
    ```
