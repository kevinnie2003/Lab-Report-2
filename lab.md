# Lab Report 2 By Kevin Nie


# Part 2
Here is one example from Lab 3 that has a bug, and I will show how I tested it and the systom, as well as the fixed code.
1.
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
2. A failure inducing input for the buggy program as a test:
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

# Part 3
One thing that I learned from labs that is very important and beneficial is that how to use Github and write a markdown file. Now I can use Github to explore thousands of projects I am interested in, as well as writing my own projects. I can also easily create a page of my own by writing a .md file one Github.
