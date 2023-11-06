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
  
## Part 2
I'll be using the ```grep``` command for this part. The command line that I'll be going over is the ```-i```, ```-c```, ```-v```, and ```-w``` commands.  
The file structure I'll be using for this part is the same file structure as the one from [Lab 5](https://github.com/ucsd-cse15l-s23/docsearch). All the commands were found from this [manual page](https://man7.org/linux/man-pages/man1/grep.1.html#OPTIONS).
### Commands
1. ```-i``` Ignore case
   ```
   $ grep -i "bAsE pAiR" technical/plos/*.txt
   technical/plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
   technical/plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
   technical/plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
   ```
   ```
   $ grep -i "BASE PAIR" technical/plos/*.txt
   technical/plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial 
   technical/plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
   technical/plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
   ```
   The command ignore the all the case in the given string. This command-line is probably useful when you want to find all instance of the word, instead of being restricted due to upper or lower case letters.
  
2. ```-c``` Count match
   ```
   $ grep -c "alcohol" technical/government/Alcohol_Problems/*.txt
   technical/government/Alcohol_Problems/DraftRecom-PDF.txt:53
   technical/government/Alcohol_Problems/Session2-PDF.txt:97
   technical/government/Alcohol_Problems/Session3-PDF.txt:168
   technical/government/Alcohol_Problems/Session4-PDF.txt:164 
   ```
   ```
   $ grep -c "Commission" technical/government/Post_Rate_Comm/*.txt 
   technical/government/Post_Rate_Comm/Cohenetal_comparison.txt:5
   technical/government/Post_Rate_Comm/Cohenetal_Cost_Function.txt:6
   technical/government/Post_Rate_Comm/Cohenetal_CreamSkimming.txt:2
   technical/government/Post_Rate_Comm/Cohenetal_DeliveryCost.txt:6
   technical/government/Post_Rate_Comm/Cohenetal_RuralDelivery.txt:5
   technical/government/Post_Rate_Comm/Cohenetal_Scale.txt:3
   technical/government/Post_Rate_Comm/Gleiman_EMASpeech.txt:25
   technical/government/Post_Rate_Comm/Gleiman_gca2000.txt:20
   technical/government/Post_Rate_Comm/Mitchell_6-17-Mit.txt:7
   technical/government/Post_Rate_Comm/Mitchell_RMVancouver.txt:7
   technical/government/Post_Rate_Comm/Mitchell_spyros-first-class.txt:5
   technical/government/Post_Rate_Comm/Redacted_Study.txt:24
   technical/government/Post_Rate_Comm/ReportToCongress2002WEB.txt:64
   technical/government/Post_Rate_Comm/WolakSpeech_usps.txt:0 
   ```
   The command-line counts the number of times the given word is mentioned in a file. It's useful to see how often a word may be used in a file.
  
3. ```-v``` Invert match
   (I most likely didn't finish, but the format for the other two command will roughly be the same as the first two command I covered. Sorry :c)
