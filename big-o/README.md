# Cracking the code interview 

## Big O

`Big 0 time` is the `language and metric we use to describe the efficiency of algorithms`. 
Not understanding it thoroughly can really hurt you in developing an algorithm. 
Not only might you be judged harshly for not really understanding big 0, but you will also struggle to judge when your algorithm is getting faster or slower.
Master this concept.

### ▶ An Analogy
> **Imagine the following scenario:**

You've got a file on a hard drive and you need to send it to your friend who lives across the country. You need to get the file to your friend as fast as possible. 

> **How should you send it?**

Most people's first thought would be email, FTP, or some other means of electronic transfer. That thought is reasonable, but only haif correct.

If it's a small file, you're certainly right, it would take 5-1 0 hours to get to an airport, hop on a flight, and then deliver it to your friend.

> **But what if the file were really, really large? Is it possible that it's faster to physically deliver it via plane?**

Yes, actually it is, A `one-terabyte (1 T8) file could take more than a day to transfer electronically`. It would be *much faster to just fly it across the country*. If your file is that urgent (and cost isn't an issue), you might just want to do that.

What if there were no flights, and instead you had to drive across the country? Even then, for a really huge file, it would be faster to drive.

### ▶ Time Complexity
This is what the concept of `asymptotic runtime`, or `big 0 time`, means. We could describe the data transfer "algorithm" runtime as:

> 1. **Electronic Transfer:** `0(s)`, where `s` is the **size of the file**. This means that `the time to transfer the file increases linearly with the size of the file`. (Yes, this is a bit of a simplification, but that's okay for these
purposes.)

> 2. **Airplane Transfer:** `0(1)` with respect to the size of the file. `As the size of the file increases, it won't take any longer` to get the file to your friend. The time is constant.

No matter how big the constant is and how slow the linear increase is, `linear will at some point surpass constant`.

[image]

There are many more runtimes than this. Some of the most common ones are `0(log N)`, `0(N log N)`, `0(N)`, `O(N^2)` and `0(2ˆN)`. There's no fixed list of possible runtimes, though.

You can also have multiple variables in your runtime. For example, the time to paint a fence that's `w` meters wide and `h` meters high could be described as `0(wh)`. If you needed `p` layers of paint, then you could say
that the time is `O(whp)`.

#### ▹ Best Case, Worst Case, and Expected Case

We can actually describe our runtime for an algorithm in three different ways.

Let's look at this **from the perspective of quicksort**. Quick sort `picks a random element as a "pivot"` and then swaps values in the array such that the elements `less than pivot appear before elements greater than pivot`.
This gives a "partial sort". 

Then it recursively sorts the left and right sides using a similar process.

> 1. **Best Case:** If all elements are equal, then quick sort will, on average, just traverse `through the array once`.
This is `0(N)`. (This actually depends slightly on the implementation of quick sort. There are implementations, though, that will run very quickly on a sorted array.)

> 2. **Worst Case:** What if we get really unlucky and the `pivot is repeatedly the biggest element in the array`?
(Actually, this can easily happen. If the pivot is chosen to be the first element in the subarray and the array is sorted in reverse order, we'll have this situation.) 
In this case, our recursion doesn't divide the array in half and recurse on each half. 
It just shrinks the subarray by one element. This will degenerate to an `O(N^)2` runtime.

> 3. **Expected Case:** Usually, though, these wonderful or terrible situations won't happen. Sure, sometimes the pivot will be very low or very high, but it won't happen over and over again. We can expect a runtime of `0(N log N)`.

We rarely ever discuss best case time complexity, because it's not a very useful concept. 

After all, we could take essentially any algorithm, special case some input, and then get an `0(1)` time in the best case.

For many—probably most—algorithms, the worst case and the expected case are the same. 

Sometimes they're different, though, and we need to describe both of the runtimes.