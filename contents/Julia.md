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

   @btime SA[1.1; 1.2; 1.3; 1.4] # 0.980 ns (0 allocations: 0 bytes)
   @btime SVector(1.1, 1.2, 1.3, 1.4, 1.5) # 0.980 ns (0 allocations: 0 bytes)
   @btime SVector{5}([1.1, 1.2, 1.3, 1.4, 1.5]) # 8.710 ns (1 allocation: 64 bytes)
   ```
4. [Julia package setup](https://bjack205.github.io/tutorial/2021/07/16/julia_package_setup.html)
5. `...` is the splat operator
   ```
   a = [[1, 1], [1, 2], [1, 4]] # 3 element vector
   vcat(a...) # 6 element vector
   @btime vcat($a...) # 40.232 ns (2 allocations: 112 bytes)
   ```
6. slicing
   ```
   a = SA[1.; 2.; 4.; 5.]
   a[2:3] # Vector
   
   idx = SVector(2, 3)
   a[idx] # SVector
   @btime $a[$idx] #2.039 ns (0 allocations: 0 bytes)

   @SVector [a[i] for i in 2:3] # SVector
   @btime @SVector [$a[i] for i in 2:3] # 1.769 ns (0 allocations: 0 bytes)

   SVector(a[2:3]...) # SVector, splat creates a new vector
   @btime SVector($a[2:3]...) # 497.990 ns (7 allocations: 208 bytes)
   
   ```
7. [Variable Scoping](https://docs.julialang.org/en/v1/manual/variables-and-scoping/)
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
8. [Measure performance with @time and pay attention to memory allocation](https://docs.julialang.org/en/v1/manual/performance-tips/#Measure-performance-with-[@time](@ref)-and-pay-attention-to-memory-allocation)
   * in `REPL` mode
   * heap allocation, for either mutable objects or for creating/growing variable-sized containers (such as Array or Dict, strings, or "type-unstable" objects whose type is only known at runtime).
   * in stack, immutable values like numbers (except bignums), tuples, and immutable structs can be stored much more cheaply
   * [reset elements in a matrix with less memory allocation](https://discourse.julialang.org/t/how-to-reset-the-elements-of-a-3x3-matrix-without-any-memory-allocation/100257/2)
9. [Type inference](https://docs.julialang.org/en/v1/manual/performance-tips/#Type-inference)
   * In many languages with optional type declarations, adding declarations is the principal way to make code run faster. This is not the case in Julia. In Julia, the compiler generally knows the types of all function arguments, local variables, and expressions. However, there are a few specific instances where declarations are helpful.
   * [tools](https://docs.julialang.org/en/v1/manual/performance-tips/#tools)
   * type instability, use @code_warntype in `REPL` mode
   * [Cthulhu](https://github.com/JuliaDebug/Cthulhu.jl)
   * A thorough [benckmark.jl](https://github.com/JuliaCI/BenchmarkTools.jl) 
10. Julia is not object-oriented, [see](https://stackoverflow.com/questions/76674552/what-is-the-julia-equivalent-to-classes-and-instance-variables-in-java)
11. `vcat(a, b)` is the same as `[a; b]`, but they both create a new array in memory and can be slow. `append!(a, b)` is faster, only modifies existing memory
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
12. push!() is also fast
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
13. test time, [see](https://discourse.julialang.org/t/time-vs-btime/9879/5)
    * @btime (from BenchmarkTools.jl) is designed for accurate benchmarking by running code multiple times, discarding compilation, and reporting the minimum time. 
    * @time is a built-in macro that reports the time and allocations of a single run, including compilation overhead, making it better for a quick check. 
    * Using @benchmark is unbiased, also reports the mean and standard deviation
    * In the code, you can use the macros:
      * `@time a = rand(1000, 1000)`
      * `@btime b = rand(1000, 1000)`
    * In the terminal `REPL` mode, run:
      * `@benchmark f_function()`
14. `map(f, array)` applies a function to each value of an array/StaticArray and returns a **new** array/StaticArray containing the resulting values.
    * ```
      julia> map(x -> x * 2, [1, 2, 3])
      3-element Vector{Int64}:
       2
       4
       6
      ```
    * `map!(f, array)` stores the result in the same array.
15. `mapslices(f, A, dims)` transforms the given dimensions of array A using function f. The dims argument determines which dimensions are sliced (e.g., dims=1 for columns, dims=2 for rows).
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
18. copy vs deepcopy
* copy: A shallow copy creates a new "container",  but the elements inside the container still point to the exact same memory locations as the original.
   * For simple values (like Float64, Int, or StaticArrays): It behaves like a full copy because these types are immutable.
   * For **nested** mutable objects: It only copies the references.
* deepcopy: A deepcopy is recursive. It looks at the object, copies it, and then looks at every object inside that object and copies those too. It continues until everything in the entire structure has its own unique spot in memory.
* For a a Vector{Float64} or Vector{SVector}, copy and deepcopy are identical because Float64 and SVector are immutable. And copy is faster than deepcopy.
* For a Vector{Vector{Float64}} or LibGEOS.Polygon, copy is dangerous, deepcopy is necessary.
   * LibGEOS object is essentially a Julia wrapper around a C pointer, copy simply duplicates that pointer address.
19. Be careful about the global variable in benchmark.
* We define
  ```
  function test_deepcopy(polygon)
      deepcopy(polygon)
  end
  ```
* and in REPL, run `free_space = LibGEOS.Polygon([[[0., 0.], [1.0, 0.], [1.0, 1.0], [0., 1.0], [0., 0.]]])`
  ```
   @benchmark deepcopy(free_space1)
   BenchmarkTools.Trial: 10000 samples with 719 evaluations per sample.
    Range (min … max):  153.656 ns … 74.655 μs  ┊ GC (min … max):  0.00% … 99.59%
    Time  (median):     251.708 ns              ┊ GC (median):     0.00%
    Time  (mean ± σ):   257.591 ns ±  1.096 μs  ┊ GC (mean ± σ):  11.04% ±  4.06%
   
       █▇                           ▂▂   ▂                         
     ▂▅██▅▃▂▂▂▃▅▃▂▂▂▁▂▂▁▂▂▁▁▁▂▂▂▂▁▂▅██▇▆▇██▅▃▄▃▃▄▅▄▃▂▂▂▂▂▂▂▂▂▂▂▂▂ ▃
     154 ns          Histogram: frequency by time          336 ns <
   
    Memory estimate: 400 bytes, allocs estimate: 6.

   @benchmark test_deepcopy(free_space1)
   BenchmarkTools.Trial: 10000 samples with 842 evaluations per sample.
    Range (min … max):  118.431 ns …  65.417 μs  ┊ GC (min … max):  0.00% … 99.61%
    Time  (median):     209.131 ns               ┊ GC (median):     0.00%
    Time  (mean ± σ):   216.129 ns ± 976.950 ns  ┊ GC (mean ± σ):  12.42% ±  4.75%
   
      ▃█▃     ▁                    ▅                                
     ▄███▄▃▂▂▆█▅▃▂▂▂▂▂▂▂▂▂▂▂▃▅▇▅▅▆███▅▆▅▄▅▅▄▃▃▂▂▂▂▂▂▂▂▂▁▁▁▂▂▂▂▂▂▂▂ ▃
     118 ns           Histogram: frequency by time          333 ns <
   
    Memory estimate: 400 bytes, allocs estimate: 6.

  ```
* the difference is because:
  * `@benchmark deepcopy(free_space1)`: Every time the benchmark runs (thousands of times), Julia has to look up free_space1, check its type to make sure it hasn't changed (since globals are mutable), and then find the correct version of deepcopy to call. This "dynamic lookup" adds a huge overhead of ~40 nanoseconds.
  * `@benchmark test_deepcopy(free_space1)`: While the initial call to test_clone also has a lookup, once you are inside the function, the variable polygon becomes a local variable. Julia knows exactly what type it is for the duration of that function. The compiler "specializes" the code, making the call to the C-library much more direct.
* In Julia benchmarking, you should never pass a global variable directly. You must use the $ sign to "interpolate" the variable. This tells BenchmarkTools to "freeze" the variable and its type before the timing starts.
  ```
  @benchmark deepcopy($free_space1)
   BenchmarkTools.Trial: 10000 samples with 846 evaluations per sample.
    Range (min … max):  117.564 ns …  66.667 μs  ┊ GC (min … max):  0.00% … 99.59%
    Time  (median):     205.778 ns               ┊ GC (median):     0.00%
    Time  (mean ± σ):   206.840 ns ± 970.879 ns  ┊ GC (mean ± σ):  12.86% ±  4.67%
   
        █▃                                                          
     ▂▃███▅▃▂▂▂▂▂▂▂▂▂▂▂▂▂▁▂▂▂▁▂▁▂▂▁▂▁▂▂▁▂▂▂▃▅▆▆▅▄▅▆▆▅▄▃▄▄▄▄▄▃▃▃▃▂▂ ▃
     118 ns           Histogram: frequency by time          251 ns <
   
    Memory estimate: 400 bytes, allocs estimate: 6.
  ```
* LibGEPS.clone is more efficient than deepcopy
  ```
   @benchmark LibGEOS.clone($free_space1)
   BenchmarkTools.Trial: 10000 samples with 982 evaluations per sample.
  
    Range (min … max):  60.081 ns …  1.060 μs  ┊ GC (min … max): 0.00% … 0.00%
    Time  (median):     76.934 ns              ┊ GC (median):    0.00%
    Time  (mean ± σ):   76.602 ns ± 11.089 ns  ┊ GC (mean ± σ):  0.00% ± 0.00%
   
                          ▂           ▄▆█▇█▅▂▁▂▁▂                 
     ▁▂▂▂▂▂▂▁▁▁▁▁▁▁▁▁▁▁▁▃███▇▅▃▂▁▁▂▃▅█████████████▆▅▄▄▃▄▃▃▃▂▂▂▂▂ ▃
     60.1 ns         Histogram: frequency by time        87.1 ns <
   
    Memory estimate: 32 bytes, allocs estimate: 1.
  ```
20. Static Type Information = Compile-Time Constants.
* For SMatrix and SVector, calling size() is effectively asking the compiler for the number it already knows.
* ```
  function f(p::NamedTuple)
     M = size(p.A, 1)
     for i in 1:M
     # ...
     end
  end
  p = (A = SA[0. 0.; 1. 2.], B = SA[0.; 0.])
  ```
  Here `M` is known at compile time. Even though it looks like a standard variable assignment, Julia’s compiler performs Constant Folding. How it works under the hood:
  * Specialization: Every time you call `f` with a new "shape" of data, Julia creates a new version of the function specialized for those exact types.
  * Type Information: Because p.A is a SMatrix{M, 2, T}, the number M is literally part of its Type.
  * Compiler Logic: When the compiler sees size(p.A, 1), it doesn't look at the data in RAM. It looks at the Type Metadata. It says: "I'm compiling the version of this function where the first argument is an SMatrix with 2 rows. Therefore, M is 2."
  * Replacement: The compiler replaces the variable M with the literal number 2 everywhere in the code before it even finishes generating the machine instructions.
  check the "LLVM" (the machine code instructions), you won't see a single "find size" or "allocate" command.
  ```
  @code_typed f(p)
  ```
* **When would it NOT be known at compile time?**
The only way to break this is by losing Type Stability. This happens if you store your matrices in a way that hides their dimensions from the compiler, such as:
  * Using a standard Array (e.g., Matrix{Float64}) instead of SMatrix.
  * Passing the NamedTuple as a NamedTuple{..., Any}.
  * Storing your p inside a Vector{Any}.
* to extract elements from namedtyple, do `(; A, B) = p`
  * The semicolon `;` tells Julia to ignore the order and match the variables to the names (keys) inside the NamedTuple.
  * `(; B, A) = p` --> `A = SA[0. 0.; 1. 2.], B = SA[0.; 0.]`
* `(A, B) = p`
  * This treats p like a standard list/tuple. It ignores the names and looks only at the index (order).
  * `(B, A) = p` --> `B = SA[0. 0.; 1. 2.], A = SA[0.; 0.]` Wrong!
21. [Make entire function constant fold](https://discourse.julialang.org/t/make-entire-function-constant-fold/45229) and [generated function](https://docs.julialang.org/en/v1/manual/metaprogramming/#Generated-functions-1)
22. [Pure function](https://discourse.julialang.org/t/can-programming-in-julia-be-pure/71165)
* A pure function in Julia is a function that produces the same output for the same input and has no side effects, such as modifying global state or input arguments. While Julia is imperative and encourages mutation, pure functions are valuable for performance optimizations, such as compile-time evaluation.
* rand() is impure: It changes the internal state of the "seed".
  * If the compiler deleted a call to rand(), the next time you called rand(), you would get the "wrong" number because the seed wouldn't have advanced.
  * The compiler is forbidden from deleting code that has "side effects" like updating a global state.
23. Symbol
* [what is a symbol](https://stackoverflow.com/questions/23480722/what-is-a-symbol-in-julia)
* ```
  a = 1
  :a # a symbol
  i=2
  b = Symnol("name_", i)
  ```
24. [inline](https://aviatesk.github.io/posts/inlining-101/)
    * it eliminates the overhead of the function call
    * it may increase the chances of other optimizations
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
