# Big O Notations - Derek Banas

`Big O notation` is a way to `measure how well a computer algorithm scales as the amount of data involved increases`. It is not always a measure of speed as you'll see below.

This is a rough overview of Big O and doesn't cover topics such as asymptotic analysis, which covers comparing algorithms as data approaches infinity.

What we are defining is the part of the algorithm that has the greatest effect. For example:

- `45n^3 + 20n^2 + 19 = 84 (n=1)`
  - `45n^3 + 20n^2 + 19 = 459 (n=2)` 
  **Does 19 matter?** 
  No, it doesn't have much of an effect on the performance of our algorithm.
    - `45n^3 + 20n^2 + 19 = 47019 (n=10)` **Does the 20n^2 matter if 45n^3 = 45,000?** 
    Definiely 19 doesn't really have that much bearing in regards to the final answer and also when we think about it `20nˆ2` has very little to do with this answer, if in fact `45ˆ3` is gonna be `equal 45,000` in this situation. 
        - **Has an O(n^3) Order of n-cubed!**
        So we're going to be dealing with very large numbers we very quickly say that the part of this algorithm that has a lot to do with the final answer as this data set scales is not even gonna be `45` but it's gonna be the `n^3` hance we would say that this has an orden of `(0)nˆ3` and that is just a very basic look.

## O(1) 

- It's gonna be an algorithm that's gonna execute in the same amount of time regardless of amount of data or to put it in other word it's going to be code that executes in the same amount of time no matter how big the array is.

``` java
public class BigONotation {

	private int[] theArray;

	private int arraySize;

	private int itemsInArray = 0;

	static long startTime;

	static long endTime;

  public BigONotation(int size) {
    this.arraySize = size;
    this.theArray = new int[size];
  }

  // Method to add an item to theArray    
	public void addItemToArray(int newItem) {
    if (itemsInArray < arraySize) {
      theArray[itemsInArray++] = newItem; // Add newItem to theArray at current index and then increment index
    } else {
        System.out.println("Array is full, cannot add more items.");
    }
  }

  public void generateRandomArray() {
    for (int i = 0; i < arraySize; i++) {
      theArray[i] = (int) (Math.random() * 1000) + 10;
    }

    itemsInArray = arraySize; // Set itemsInArray to the actual number of items in the array
  }

  public static void main(String[] args) {
    BigONotation test = new BigONotation(10);
		test.addItemToArray(10);
    
		System.out.println(Arrays.toString(test.theArray));

    BigONotation test2 = new BigONotation(10);
		test2.addItemToArray(10000);
    
		System.out.println(Arrays.toString(test2.theArray));
  }
}
```
> [10, 0, 0, 0, 0, 0, 0, 0, 0, 0]
> This output represents an array with 10 elements, where the first element is 10 and the rest are initialized to 0, as no other items were added to the array.
> [10000, 0, 0, 0, 0, 0, 0, 0, 0, 0]
> This output represents an array with 10 elements, where the first element is 10000 and the rest are initialized to 0, as no other items were added to the array.
> So, it doesn't matter if this is a 10,000 item array or a 10 item array it is gonna perform in exactly the same way.

## 0(N) 

- An algorithm that's time to complete will grow in direct proportion to the amount of data. `The linear search` is an example of this. 
To find all values that match what we	are searching for we will have to look in exactly each item in the array.
If we just wanted to find one match the Big O	is the same because it describes the `worst case scenario` in which the `whole array must be searched`.

``` java
public class BigONotation {

	private int[] theArray;

	private int arraySize;

	private int itemsInArray = 0;

	static long startTime;

	static long endTime;

  public BigONotation(int size) {
    this.arraySize = size;
    this.theArray = new int[size];
  }

	public void linearSearchForValue(int value) {

		boolean valueInArray = false;
		String indexsWithValue = ""; // to force the issue so that it searches through the entire array, because the java compiler is actually smart enough if I don't tell it that it needs to more than one it will actually stop 

		startTime = System.currentTimeMillis(); // to see how long it takes for this guy to execute

		for (int i = 0; i < arraySize; i++) {
			if (theArray[i] == value) {
				valueInArray = true;
				indexsWithValue += i + " ";
			}
		}

		System.out.println("Value Found: " + valueInArray);

		endTime = System.currentTimeMillis();

		System.out.println("Linear Search Took " + (endTime - startTime) + "ms");
	}

  public void generateRandomArray() {
    for (int i = 0; i < arraySize; i++) {
      theArray[i] = (int) (Math.random() * 1000) + 10;
    }

    itemsInArray = arraySize; // Set itemsInArray to the actual number of items in the array
  }

  public static void main(String[] args) {
		BigONotation test1 = new BigONotation(100000);
		test1.generateRandomArray();

    BigONotation test2 = new BigONotation(200000);
		test2.generateRandomArray();

    BigONotation test3 = new BigONotation(300000);
		test3.generateRandomArray();

    BigONotation test4 = new BigONotation(400000);
		test4.generateRandomArray();

    test1.linearSearchForValue(20);
    test2.linearSearchForValue(20);
    test3.linearSearchForValue(20);
    test4.linearSearchForValue(20);
	}
}
```
> For the smaller array sizes (e.g., 100,000), the linear search operation might complete relatively quickly.
> As the array size increases (e.g., 200,000, 300,000, 400,000), the linear search operation may take longer to complete due to the increased number of elements to search through.
> So we can see as the number of elements scale get bigger the number of elements we have to deal with that is in direct relation to the number of elements and that is why it is known as `order of n`. 

## O(N^2) 

- `Time to complete` will be `proportional to the square(quadrado) of the amount of data`(Bubble Sort).
Algorithms with more nested iterations will result in O(N^3), O(N^4), etc. performance.
`Each pass through the outer loop(laço externo) (0)N requires usto go through the entire list again` so N multiplies	against itself or it is squared.

``` java
public class BigONotation {

	private int[] theArray;

	private int arraySize;

	private int itemsInArray = 0;

	static long startTime;

	static long endTime;

  public BigONotation(int size) {
    this.arraySize = size;
    this.theArray = new int[size];
  }

  public void bubbleSort() {
		startTime = System.currentTimeMillis();

		for (int i = arraySize - 1; i > 1; i--) {
			for (int j = 0; j < i; j++) {
				if (theArray[j] > theArray[j + 1]) {
					swapValues(j, j + 1);
				}
			}
		}

		endTime = System.currentTimeMillis();

		System.out.println("Bubble Sort Took " + (endTime - startTime) + "ms");
	}

  public void generateRandomArray() {
    for (int i = 0; i < arraySize; i++) {
      theArray[i] = (int) (Math.random() * 1000) + 10;
    }

    itemsInArray = arraySize; // Set itemsInArray to the actual number of items in the array
  }

  public void swapValues(int indexOne, int indexTwo) {
		int temp = theArray[indexOne];
		theArray[indexOne] = theArray[indexTwo];
		theArray[indexTwo] = temp;
	}

  public static void main(String[] args) {
		BigONotation test1 = new BigONotation(10000);
		test1.generateRandomArray();

    BigONotation test2 = new BigONotation(20000);
		test2.generateRandomArray();

    test1.bubbleSort();
    test2.bubbleSort();
	}
}
```
> The bubble sort algorithm will sort each array in ascending order.
> For the array of size 10000, the bubble sort operation might take a relatively short amount of time, likely less than a second.
> For the array of size 20000, the bubble sort operation will likely take longer than for the smaller array, as bubble sort has a time complexity of O(n^2) and its performance degrades quickly with larger input sizes. It might take a few seconds or more to complete.
> We can sse how dramatically slower the bubble sort gets depending upon the amount of data
> And that is why orden of N squared is very bad and to be avoided.

<!-- falta arrumar -->

``` java
public class BigONotation {
	public static void main(String[] args) {	

		BigONotation testAlgo2 = new BigONotation(100000);
		testAlgo2.generateRandomArray();

		BigONotation testAlgo3 = new BigONotation(200000);
		testAlgo3.generateRandomArray();

		BigONotation testAlgo4 = new BigONotation(30000);
		testAlgo4.generateRandomArray();

		BigONotation testAlgo5 = new BigONotation(400000);
		testAlgo5.generateRandomArray();

		/*
		 * 
		 * // 0 (log N) Test
		 * 
		 * testAlgo2.binarySearchForValue(20);
		 * testAlgo3.binarySearchForValue(20);
		 */

		// O (n log n) Test

		startTime = System.currentTimeMillis();

		testAlgo2.quickSort(0, testAlgo2.itemsInArray);

		endTime = System.currentTimeMillis();

		System.out.println("Quick Sort Took " + (endTime - startTime));

	}

	// O (log N) Occurs when the data being used is decreased
	// by roughly 50% each time through the algorithm. The
	// Binary search is a perfect example of this.

	// Pretty fast because the log N increases at a dramatically
	// slower rate as N increases

	// O (log N) algorithms are very efficient because increasing
	// the amount of data has little effect at some point early
	// on because the amount of data is halved on each run through

	public void binarySearchForValue(int value) {

		startTime = System.currentTimeMillis();

		int lowIndex = 0;
		int highIndex = arraySize - 1;

		int timesThrough = 0;

		while (lowIndex <= highIndex) {

			int middleIndex = (highIndex + lowIndex) / 2;

			if (theArray[middleIndex] < value)
				lowIndex = middleIndex + 1;

			else if (theArray[middleIndex] > value)
				highIndex = middleIndex - 1;

			else {

				System.out.println("\nFound a Match for " + value
						+ " at Index " + middleIndex);

				lowIndex = highIndex + 1;

			}

			timesThrough++;

		}

		// This doesn't really show anything because
		// the algorithm is so fast

		endTime = System.currentTimeMillis();

		System.out.println("Binary Search Took " + (endTime - startTime));

		System.out.println("Times Through: " + timesThrough);

	}

	// O (n log n) Most sorts are at least O(N) because
	// every element must be looked at, at least once.
	// The bubble sort is O(N^2)
	// To figure out the number of comparisons we need
	// to make with the Quick Sort we first know that
	// it is comparing and moving values very
	// efficiently without shifting. That means values
	// are compared only once. So each comparison will
	// reduce the possible final sorted lists in half.
	// Comparisons = log n! (Factorial of n)
	// Comparisons = log n + log(n-1) + .... + log(1)
	// This evaluates to n log n

	public void quickSort(int left, int right) {

		if (right - left <= 0)
			return;

		else {

			int pivot = theArray[right];

			int pivotLocation = partitionArray(left, right, pivot);

			quickSort(left, pivotLocation - 1);
			quickSort(pivotLocation + 1, right);

		}

	}

	public int partitionArray(int left, int right, int pivot) {

		int leftPointer = left - 1;
		int rightPointer = right;

		while (true) {

			while (theArray[++leftPointer] < pivot)
				;

			while (rightPointer > 0 && theArray[--rightPointer] > pivot)
				;

			if (leftPointer >= rightPointer) {

				break;

			} else {

				swapValues(leftPointer, rightPointer);

			}

		}

		swapValues(leftPointer, right);

		return leftPointer;

	}

	BigONotation(int size) {

		arraySize = size;

		theArray = new int[size];

	}
}
```