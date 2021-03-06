# Finding the largest product in a series

This project contains the solution for the 8th problem. The task is to find the largest product of 13 adjacent digits in the following
1000-digit number:

                                      73167176531330624919225119674426574742355349194934
                                      96983520312774506326239578318016984801869478851843
                                      85861560789112949495459501737958331952853208805511
                                      12540698747158523863050715693290963295227443043557
                                      66896648950445244523161731856403098711121722383113
                                      62229893423380308135336276614282806444486645238749
                                      30358907296290491560440772390713810515859307960866
                                      70172427121883998797908792274921901699720888093776
                                      65727333001053367881220235421809751254540594752243
                                      52584907711670556013604839586446706324415722155397
                                      53697817977846174064955149290862569321978468622482
                                      83972241375657056057490261407972968652414535100474
                                      82166370484403199890008895243450658541227588666881
                                      16427171479924442928230863465674813919123162824586
                                      17866458359124566529476545682848912883142607690042
                                      24219022671055626321111109370544217506941658960408
                                      07198403850962455444362981230987879927244284909188
                                      84580156166097919133875499200524063689912560717606
                                      05886116467109405077541002256983155200055935729725
                                      71636269561882670428252483600823257530420752963450

Solution
---

```fsharp
open System.IO

File.ReadLines "Series.txt" 
|> Seq.concat 
|> Seq.map (fun i -> int64 i - int64 '0')
|> Seq.windowed 13  
|> Seq.map (Array.reduce (*))
|> Seq.max 
|> printfn("%i")
```

Walkthrough
---

The 1000-digit number is stored in a tex file . So in order to begin we have to open each line of the text file, convert the resulting string array into one char array and finally convert the char array into a int64 array. 

```fsharp
open System.IO

File.ReadLines "Series.txt" 
|> Seq.concat 
|> Seq.map (fun i -> int64 i - int64 '0')
```
So after doing this we end up with one int64 array that contains all the digits of the original 1000-digit number. The type int64 has to be used because in later operations the numbers exceed the int range.

Now that we have the int array of all digits we only have to calculate all products of 13 adjacent numbers store them in a list and find the largest. 

```fsharp
|> Seq.windowed 13  
|> Seq.map (Array.reduce (*))
|> Seq.max 
|> printfn("%i")
```

In order to get all combinations of 13 adjacent elements in a sequence, I have used the Seq.windowed command. This command takes an int value and a sequence as arguments and returns a sequece which yields sliding windows with the size of the int value containing elements drawn from the input sqeuence. The numbers in every array in the new sequence are then all multiplied. The resulting sequence does now only contain int64 values and thus we can pipe it into then Seq.max function.

Result
---
The result equals to 23514624000.
