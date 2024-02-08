# Evan Wu - Lab 2 Report
---
## Part 1 - Bugs
---
For this part, I've chosen to look at the `reverseInPlace()` command in `ArrayExamples.java` and `ArrayTests.java`.

1. My failure inducing input was my custom test for `reverseInPlace()`:
```
@Test
  public void testReverseInPlace2() {
    int[] input1 = {1, 2, 3, 4, 5};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, input1);
	}
```
2. Non-failure inducing input that was provided for us for `reverseInPlace()`:
```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```
3. Symptom:
4. Bug fix:
Before:
```
  Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
After:
```
    // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for (int i = 0; i < arr.length/2; i++) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
``` 
