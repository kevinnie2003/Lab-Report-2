# Lab Report 2 By Kevin Nie
# Part 1


# Part 2
Here is one example from Lab 3 that has a bug, and I will show how I tested it and the systom, as well as the fixed code.


1. A failure inducing input for the buggy program as a test:
```
  import static org.junit.Assert.*;
  import org.junit.*;

  public class ArrayTests {
    @Test
    public void testReversed2() {
        int[] input1 = { 1, 2, 3, 4 };
        assertArrayEquals(new int[] { 4, 3, 2, 1 }, ArrayExamples.reversed(input1));
    }
  }
```

2. An input that doesn’t induce a failure, as a test:

```
  import static org.junit.Assert.*;
  import org.junit.*;

  public class ArrayTests {
    @Test
    public void testReversed1() {
    int[] input1 = {};
    assertArrayEquals(new int[] {}, ArrayExamples.reversed(input1));
    }
  }
```

3. The symptom, as the output:

<img width="926" alt="截屏2023-04-19 17 24 37" src="https://user-images.githubusercontent.com/122497019/233502796-1a96f092-209c-411b-b423-f251aa59274d.png">

The bug is that arr value should be passed to newArray, but the code did the opposite way so the empty newArray is passed to newArray. It should return the newArray instead of the original array “arr” as well.

4.
The original code with the bug:
```
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
```
The fixed code:
```
  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for (int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```

Change the code so that the reversed array of input array is stored in newArray and return the newArray.



# Part 3
One thing that I learned from labs that is very important and beneficial is that how to use Github and write a markdown file. Now I can use Github to explore thousands of projects I am interested in, as well as writing my own projects. I can also easily create a page of my own by writing a .md file one Github.
