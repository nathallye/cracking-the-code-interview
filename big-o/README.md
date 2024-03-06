# Cracking the code interview 

## Big O

<div align="center">
  <img width="500" src="https://github.com/nathallye/cracking-the-code-interview/assets/86172286/12a043b3-4982-461b-a767-3b3cbda84c91">
</div>

`Big 0 time` is the `language and metric we use to describe the efficiency of algorithms`. 
Not understanding it thoroughly can really hurt you in developing an algorithm. 
Not only might you be judged harshly for not really understanding big 0, but you will also struggle to judge when your algorithm is getting faster or slower.
Master this concept.

### ▶ An Analogy
- **Imagine the following scenario:**

You've got a file on a hard drive and you need to send it to your friend who lives across the country. You need to get the file to your friend as fast as possible. 

- **How should you send it?**

Most people's first thought would be email, FTP, or some other means of electronic transfer. That thought is reasonable, but only haif correct.

If it's a small file, you're certainly right, it would take 5-1 0 hours to get to an airport, hop on a flight, and then deliver it to your friend.

- **But what if the file were really, really large? Is it possible that it's faster to physically deliver it via plane?**

Yes, actually it is, A `one-terabyte (1 T8) file could take more than a day to transfer electronically`. It would be *much faster to just fly it across the country*. If your file is that urgent (and cost isn't an issue), you might just want to do that.

What if there were no flights, and instead you had to drive across the country? Even then, for a really huge file, it would be faster to drive.

### ▶ Time Complexity
This is what the concept of `asymptotic runtime`, or `big 0 time`, means. We could describe the data transfer "algorithm" runtime as:

1. **Electronic Transfer:** `0(s)`, where `s` is the **size of the file**. This means that `the time to transfer the file increases linearly with the size of the file`. (Yes, this is a bit of a simplification, but that's okay for these
purposes.)

2. **Airplane Transfer:** `0(1)` with respect to the size of the file. `As the size of the file increases, it won't take any longer` to get the file to your friend. The time is constant.

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

1. **Best Case:** If all elements are equal, then quick sort will, on average, just traverse `through the array once`.
This is `0(N)`. (This actually depends slightly on the implementation of quick sort. There are implementations, though, that will run very quickly on a sorted array.)

2. **Worst Case:** What if we get really unlucky and the `pivot is repeatedly the biggest element in the array`?
(Actually, this can easily happen. If the pivot is chosen to be the first element in the subarray and the array is sorted in reverse order, we'll have this situation.) 
In this case, our recursion doesn't divide the array in half and recurse on each half. 
It just shrinks the subarray by one element. This will degenerate to an `O(N^2)` runtime.

3. **Expected Case:** Usually, though, these wonderful or terrible situations won't happen. Sure, sometimes the pivot will be very low or very high, but it won't happen over and over again. We can expect a runtime of `0(N log N)`.

We rarely ever discuss best case time complexity, because it's not a very useful concept. 

After all, we could take essentially any algorithm, special case some input, and then get an `0(1)` time in the best case.

For many—probably most—algorithms, the worst case and the expected case are the same. 

Sometimes they're different, though, and we need to describe both of the runtimes.

### ▶ Space Complexity

`Time is not the only thing that matters in an algorithm`. We might also care about the `amount of memory—or space—required by an algorithm`.

**Space complexity is a parallel concept to time complexity**. If we need to create an array of size n, this will require 0(n) space. 
If we need a two-dimensional array of size nxn, this will require 0(nˆ2) space.

Stack space in recursive calls counts, too. For example, code like this would take `0(n) time` and `0(n) space`:

``` java
int sum(int n) {
  if (n <= 0) {
    return 0;
  }
  return n + sum(n-1);
}
```

> Each call adds a level to the stack.

``` java
sum(4)
  -> sum(3)
    -> sum(2)
      -> sum(1)
        -> sum(0)
```

> Each of these calls is added to the call stack and takes up actual memory.

However, **just because you have n calls total doesn't mean it takes O(n) space**. Consider the below function, which adds adjacent elements between 0 and n:

``` java
int pairSumSequence(int n) { 
  int sum = 0;
  for (int i = 0; i < n; i++) {
    sum += pairSum(i, i + 1);
  }
  return sum;
}

int pairSum(int a, int b) {
  return a + b;
}
```

> There will be roughly `O(n)` calls to `pairSum`. However, those calls do not exist simultaneously on the call stack, so you only need `0(1) space`.

### ▶ Drop the Constants

`It is very possible for 0(N) code to run faster than 0(1) code for specific inputs`. Big 0 just describes the rate of increase.

For this reason, we drop the constants in runtime. An algorithm that one might have described as `0(2N)` is actually `O(N)`. Many people resist doing this. They will see code that has two (non-nested) for loops and continue this 0(2N). They think they're being more "precise." They're not.

Consider the below code:

``` java
// Min and Max                    
int min = Integer.MIN_VALUE;
int max = Integer.MAX_VALUE;

for (int x : array) {
  if (x < min) min = x;
  if (x > max) max = x;
}

// Min and Max 2
int min = Integer.MIN_VALUE;
int max = Integer.MAX_VALUE;

for (int x : array) {
  if (x < min) min = x;
}

for (int x : array) {
  if (x > max) max = x;
}
```

Which one is faster? 

The first one does one for loop and the other one does two for loops. But then, the first solution has two lines of code per for loop rather than one.

If you're going to count the number of instructions, then you'd have to go to the assembly level and take into account that multiplication requires more instructions than addition, how the compiler would optimize something, and all sorts of other details.

This would be horrendously complicated, so don't even start going down this road. Big O allows us to express how the runtime scales. We just need to accept that it doesn't mean that 0(N) is always better than 0(N^2).

### ▶ Drop the Non-Dominant Terms

What do you do about ari expression such as 0(Nˆ2+ N)? That second N isn't exactly a constant. But it's not especially important.
We already said that we drop constants. Therefore, 0(Nˆ2+ Nˆ2) would be 0 (Nˆ2)- If we don't care about that latter Nˆ2 term, why would we care about N? We don't.

You should drop the non-dominant terms,
• 0(Nˆ2 + N) becomes O(Nˆ2).
• 0(N + log N) becomes O(N).
• 0(5*2ˆN + 1000Nˆ100) becomes 0(2ˆN).

We might still have a sum in a runtime. For example, the expression 0(Bˆ2 + A) cannot be reduced (without some special knowledge of A and B).

The following graph depicts the rate of increase for some of the common big 0 times.

[image]

As you can see, O(xˆ2) is much worse than 0(x), but it's not nearly as bad as 0(2ˆx) or 0(x!} . There are lots of runtimes worse than O(x!) too, suchas 0(xˆx) or 0(2ˆx * x!).

• Multi-Part Algorithms: Add vs. Multiply
Suppose you have an algorithm that has two steps. When do you multiply the runtimes and when do you add them?

This is a common source of confusion for candidates.

``` java
// Add the Runtimes: 0(A + B)
for (int a : arrA) {
  print(a);
}

for (int b : arrB) {
  print(b);
}

Multiply theRuntimes: 0(A*B)
for (int a : arrA) {
  for (int b : arrB) {
    print(a + "," + b);
  }
}
```

In the example on the left, we do A chunks of work then B chunks of work. Therefore, the total amount of work is O(A + B).
In the example on the right, we do B chunks of work for each element in A. Therefore, the total amount of work is O(A * B).

In other words:
• If your algorithm is in the form "do this, then, when you're all done, do that" then you add the runtimes.
• If your algorithm is in the form "do this for each time you do that" then you multiply the runtimes.

It's very easy to mess this up in an interview, so be careful.

### ▶ Amortized Time

An ArrayList, or a dynamically resizing array, allows you to have the benefits of an array while offering flexibility in size. You won't run out of space in the ArrayList since its capacity will grow as you insert elements.

An ArrayList is implemented with an array. When the array hits capacity, the ArrayList class will create a new array with double the capacity and copy all the elements over to the new array.

- How do you describe the runtime of insertion? This is a tricky question.

The array could be full. If the array contains N elements, then inserting a new element will take O(N) time. You will have to create a new array of size 2N and then copy N elements over. This insertion will take O(N) time.

However, we also know that this doesn't happen very often. The vast majority of the time insertion will be in 0(1) time.
We need a concept that takes both into account. This is what amortized time does. It allows us to describe that, yes, this worst case happens every once in a while. But once it happens, it won't happen again for so long that the cost is "a mortized."

- In this case, what is the amortized time?
As we insert elements, we double the capacity when the size of the array is a power of 2. So after X elements, we double the capacity at array sizes 1, 2, 4, 8, 16,..., X. That doubling takes, respectively, 1, 2, 4, 8, 16, 32, 64,..., X copies.

- What is the sum of 1 + 2 + 4 + 8 + 16 + ... + X?
If you read this sum left to right, it starts with 1 and doubles until it gets to X. If you read right to left, it starts with X and halves until it gets to 1.
