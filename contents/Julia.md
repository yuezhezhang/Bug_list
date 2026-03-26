# Julia

1. Array index starts from 1
2. Space matters
   ```
   a = [1, 1, 1] # 3 element vector
   a = [1 1 1+1] # 1, 3 matrix
   a = [1 1 1 +1] # 1, 4 matrix
   ```
3. `...` is the splat operator
   ```
   a = [[1, 1], [1, 2], [1, 4]] # 3 element vector
   vcat(a...) # 6 element vector
   ```
4. [Variable Scoping](https://docs.julialang.org/en/v1/manual/variables-and-scoping/)
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
