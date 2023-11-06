# Lab Report 3 (Week 5)
## Part 1
For part 1 of this week's lab report, I'll be using the Array Methods bugs from Lab 4.  
  
A failure inducing output for the Array Methods are:  
```
  //Test for the reverseInPlace() method
  @Test
  public void reverseInPlaceTest(){
    int[] input1 = {1, 2, 3, 4, 5};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, input1);
  }

  //Test for the reversed() method
  @Test
  public void reversedTest(){
    int[] input = {1, 2, 3, 4, 5};
    input = ArrayExamples.reversed(input);
    assertArrayEquals(new int[]{5, 4, 3, 2, 1}, input);
  }
```
  
An input that *doesn't* induce a failure are:
```
	@Test 
	public void testReverseInPlace() {
    int[] input1 = { 1, 1 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 1, 1 }, input1);
	}


  @Test
  public void testReversed() {
    int[] input1 = { 0, 0, 0};
    assertArrayEquals(new int[]{ 0, 0, 0}, ArrayExamples.reversed(input1));
  }
```
  
A symptoms from running the above (failure-inducing) inputs are:
![Symptoms](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/3c2b84b5-5f95-451b-b4cc-46cba5a6140e)

The following is the code before and after fixing the bugs in the Array Methods.  
Before:
```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }

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
    
After:
```
  // Changes the input array to be in reversed order
  static void reverseInPlace(int[] arr) {
    int[] tempArray = arr.clone();
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = tempArray[arr.length - i - 1];
    }
  }

  // Returns a *new* array with all the elements of the input array in reversed
  // order
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      newArray[i] = arr[arr.length - i - 1];
    }
    return newArray;
  }
```
The original reverseInPlace() method was trying to reverse the array by using the original array. What the line ```arr[i] = newArray[arr.length - i - 1];``` ends up doing instead is replacing the
first half of the array and attempted to use the already replaced first half to then work on the second half. The output creates an array with symmetrical values instead. To fix the code, I created a
temporary array to store the original value of the arrays and use the temporary array instead to reverse the order.  

For the reversed() method, the bug was that the new array was uninitialized so the array was filled with all zeroes. To fix the bug, all I needed to do was switch ```arr[i] = newArray[arr.length - i - 1];``` to ```newArray[i] = arr[arr.length - i - 1];``` and return ```newArray``` instead.
