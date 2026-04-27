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
12. test time, [see](https://discourse.julialang.org/t/time-vs-btime/9879/5)
    * @btime (from BenchmarkTools.jl) is designed for accurate benchmarking by running code multiple times, discarding compilation, and reporting the minimum time. 
    * @time is a built-in macro that reports the time and allocations of a single run, including compilation overhead, making it better for a quick check. 
    * Using @benchmark is unbiased, also reports the mean and standard deviation
    * In the code, you can use the macros:
      * `@time a = rand(1000, 1000)`
      * `@btime b = rand(1000, 1000)`
    * In the terminal `REPL` mode, run:
      * `@benchmark f_function()`
13. `map(f, array)` applies a function to each value of an array/StaticArray and returns a **new** array/StaticArray containing the resulting values.
    * ```
      julia> map(x -> x * 2, [1, 2, 3])
      3-element Vector{Int64}:
       2
       4
       6
      ```
    * `map!(f, array)` stores the result in the same array.
14. `mapslices(f, A, dims)` transforms the given dimensions of array A using function f. The dims argument determines which dimensions are sliced (e.g., dims=1 for columns, dims=2 for rows).
 * sum along the col dimension
   ```
   julia> A = [1 2 3; 4 5 6; 7 8 9];

   julia> mapslices(sum, A, dims=1)
   3×1 Matrix{Int64}:
    12
    15
    18
   ```
* product along the row dimension
   ```
   julia> B = [1 2 3; 4 5 6; 7 8 9; 10 11 12];
   julia> mapslices(prod, B, dims=2)
   4×1 Matrix{Int64}:
      6
    120
    504
   1320
   ```
* mean of all elements in the matrix
    ```
    julia> C = [1 2 3; 4 5 6; 7 8 9; 10 11 12];
   
    julia> mapslices(mean, C, dims=[1, 2])
    1×1 Matrix{Float64}:
     6.5
    ```
* mapslices not working on StaticArray, mapslices is designed to be Type-Unstable—it works by slicing up the array into little pieces and then trying to glue them back together at runtime. For similar behaviour of `mapslices(f, a, dims=1)` for StaticArray, you can do Comprehension or Broadcasting on the columns/rows directly
  * results = [f(col) for col in eachcol(a)]
15. `round(a)`, round a number to integer (round half to even) round a number to integer `round(a, digits=3)` round a number with given digits
    * round(2.5) --> 2
    * round(3.5) --> 4
    * ```
      a = [1.099, 2.999, 3.28]
      map(x->round(x, digits=3), a)

      round.(a, digits=3) # using broadcasting
      ```
16. [map vs broadcasting](https://discourse.julialang.org/t/when-to-use-broadcasting-with-vs-map/58078/2)
    * map is designed to handle sequences **generic iterables**, while broadcasting is designed to handle **arrays/dimensions**. Broadcasting will try to convert the geenric iterables to arrays by collect(seq), which creates memory allocation for new data
    * Use Broadcasting (.) when your data is already in Arrays or Matrices and you want to do math across dimensions (like adding a column to every column of a matrix).
    * Use map (or comprehensions [f(x) for x in seq]) when your input is a Set, a Generator, or a Lazy Iterator where you just want to transform a sequence of values without worrying about "grid alignment."
17. **Generic Iterables** usually refers to collections that don't have a fixed grid-like structure or indices:
    * Generators: Objects created by syntax like (x^2 for x in 1:10). These don't store data in memory; they calculate the next value on the fly.
    * Sets (Set): Collections of unique elements where the order doesn't matter and there are no "axes" or "coordinates."
    * Dictionaries (Dict): Collections of Key-Value pairs
    * Tuples and NamedTuples: Immutable sequences of fixed length.
    * Strings: Technically a collection of characters.
    * Lazy Collections: Like those provided by Iterators.filter or Iterators.flatten.

    

# Parallelization
* Physical core: number of physical cores, actual hardware components.
* Logical cores are the number of physical cores times the number of threads that can run on each core through the use of hyperthreading.
   * With HTT, one physical core appears as two processors to the operating system, allowing concurrent scheduling of two processes per core. See [hyper-threading](https://en.wikipedia.org/wiki/Hyper-threading)
* run `lscpu`:
  ```
   Architecture:                         x86_64
   CPU op-mode(s):                       32-bit, 64-bit
   Byte Order:                           Little Endian
   Address sizes:                        48 bits physical, 48 bits virtual
   CPU(s):                               32
   On-line CPU(s) list:                  0-31
   Thread(s) per core:                   2
   Core(s) per socket:                   16
   Socket(s):                            1
  ```
  it shows:
   * Physical Cores: 16 (Core(s) per socket)
   * Logical Threads: 32 (CPU(s))
* [julia-for-hpc](https://enccs.github.io/julia-for-hpc/multithreading/)
* save data as a named tuple
  ```
  results = fill((sol=MVector(0.,0.,0.), solved=false, merit=Inf), 2*n_threads)
  @threads for i in 1:2*n_threads
     sol, solved, _, merit = run_f()
     results[i] = (sol, solved, merit)
  end

  best_merit, best_id = findmin(r -> r.solved ? r.merit : Inf, results)
  ```
  * `r ->` is an [anonymous function](https://docs.julialang.org/en/v1/manual/functions/#man-anonymous-functions), it will take `r` as input and do the operations
  * you can pass an anonymous function to map, so that it can operate on arrays
    ```
    julia> map(x -> x^2 + 2x - 1, [1, 3, -1])
    3-element Vector{Int64}:
      2
      14
      -2
    ```
  * we also use anonymous function in getting autodiff jacobian
