# Lab Report 5 (Week 9)
## Part 1
For part 1, I'll be covering a debugging scenario in the format of an EdStem post conversation between a student and a TA.

Throughout the scenario, I'll be providing the following information:
* The file & directory structure needed
* The contents of each file before fixing the bug
* The full command line (or lines) you ran to trigger the bug
* A description of what to edit to fix the bug

I'll also be using the materials from [Lab 6](https://ucsd-cse15l-f23.github.io/week/week6/). The Java file I'll be using is from [Lab 6 Student Submission](https://ucsd-cse15l-f23.github.io/week/week6/#student-submissions), specifically the [corrected version](https://github.com/ucsd-cse15l-f22/list-methods-corrected) (so that the bug shown is actually from the student's error rather that the submissions). As for the bash script, I'll be using my version of `grade.sh` that I built for the lab task from the provided [repository](https://github.com/ucsd-cse15l-s23/list-examples-grader) in Lab 6.

---
#### Student:
Hello, I seem to be having trouble in getting `TestListExamples.java` to run. Here's the symptom that I'm getting after running `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected` in the command line:
![Symptoms_Buggy](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/31108419-19f6-4d67-be31-2b7859db2d6e)

From the symptoms, it looks like the java file couldn't find the JUnit package. However, I did make sure that the `lib` directory exists inside `list-examples-grader` directory that I initially cloned from the lab. This is my file and directory structure after running the same `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected` command from earlier: 
![FileDirectoryStructure_Buggy](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/efd0a369-d087-4e00-a29a-b7f4f5de308a)

This is the content of my `grade.sh` file:
```
CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

# Draw a picture/take notes on the directory structure that's set up after
# getting to this point
# 
# list-examples-grader
#   |- grading-area
#   |- lib
#       |- hamcrest-core-1.3.jar
#       |- junit-4.13.2.jar
#   |- student-submission
#       |- <Cloned student submission goes here>
#   |- grade.sh
#   |- GradeServer.java
#   |- Server.java
#   |- TestListExamples.java


# Then, add here code to compile and run, and do any post-processing of the
# tests

submissionPath=`find */ListExamples.java`
echo "The path is $submissionPath"

if [[ -f $submissionPath ]]
then
    echo 'ListExamples.java found'
else
    echo -e 'ListExamples.java not found\n
            Please make sure the file is named "ListExamples.java" and not inside another directory'
    exit
fi

cp $submissionPath TestListExamples.java grading-area

cd grading-area

javac -cp "$CPATH" *.java

if [[ $? -ne 0 ]]
then
    echo -e "--------------------\nCompilation failed\n--------------------"
    exit
else
    echo -e "------------------------\nCompilation successful\n------------------------"
fi

java -cp "$CPATH" org.junit.runner.JUnitCore TestListExamples
```
And this is the `TestListExamples.java` that I use in my bash script:
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.Arrays;
import java.util.List;

class IsMoon implements StringChecker {
  public boolean checkString(String s) {
    return s.equalsIgnoreCase("moon");
  }
}

public class TestListExamples {
  @Test(timeout = 500)
  public void testMergeRightEnd() {
    List<String> left = Arrays.asList("a", "b", "c");
    List<String> right = Arrays.asList("a", "d");
    List<String> merged = ListExamples.merge(left, right);
    List<String> expected = Arrays.asList("a", "a", "b", "c", "d");
    assertEquals(expected, merged);
  }
}

```
Any help would be appreciated. Thanks!

---
#### TA:
It seems that you're right in that the Java file couldn't find the JUnit package. It may be worth investigating *why* that may be the case. One thing to look for is the current working directory when trying to run the `javac` command inside the bash script. Maybe you can try adding an `echo` command to see where your working directory is before bash runs the `javac` command. You can also try using the `-x` option when running your bash script to see which specific command caused the error to print out.

---
#### Student:
I've added `echo $(pwd)` right before the `javac` command to see where the working directory is. I also ran the `grade.sh` script with the `-x` command you suggested and the error is indeed caused by the `javac` command:
![Symptoms_Suggestion](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/d7ffc948-b894-4625-b255-3f3ef167f089)

The current directory when the script was running the `javac` command was `/c/Users/stama/Documents/GitHub/list-examples-grader/grading-area`. The `lib` directory is in the home directory which explains why the `TestListExamples.java` couldn't find the JUnit package. 

The bug seems to be that `grading-area` is missing that required `lib` directory. What I did to fix the bug was to create the `lib` directory *inside* `grading-area` and copy the `.jar` files from the original `lib` directory to the new `lib` directory *inside* `grading-area`. I added
```
mkdir lib
cp ../lib/*.jar ./lib
```
while inside `grading-area` to create the `lib` directory and copy the `.jar` files over. 

Now the `grade.sh` script looks like this:
```
CPATH='.;lib/hamcrest-core-1.3.jar;lib/junit-4.13.2.jar'

rm -rf student-submission
rm -rf grading-area

mkdir grading-area

git clone $1 student-submission
echo 'Finished cloning'

# Draw a picture/take notes on the directory structure that's set up after
# getting to this point
# 
# list-examples-grader
#   |- grading-area
#   |- lib
#       |- hamcrest-core-1.3.jar
#       |- junit-4.13.2.jar
#   |- student-submission
#       |- <Cloned student submission goes here>
#   |- grade.sh
#   |- GradeServer.java
#   |- Server.java
#   |- TestListExamples.java


# Then, add here code to compile and run, and do any post-processing of the
# tests

submissionPath=`find */ListExamples.java`
echo "The path is $submissionPath"

if [[ -f $submissionPath ]]
then
    echo 'ListExamples.java found'
else
    echo -e 'ListExamples.java not found\n
            Please make sure the file is named "ListExamples.java" and not inside another directory'
    exit
fi

cp $submissionPath TestListExamples.java grading-area

# Creates the lib directory inside grading-area (so the test could actually run)
cd grading-area
mkdir lib
cp ../lib/*.jar ./lib

echo "Working directory: $(pwd)"

javac -cp "$CPATH" *.java

if [[ $? -ne 0 ]]
then
    echo -e "--------------------\nCompilation failed\n--------------------"
    exit
else
    echo -e "------------------------\nCompilation successful\n------------------------"
fi

java -cp "$CPATH" org.junit.runner.JUnitCore TestListExamples
```
And this is the result of running `bash grade.sh https://github.com/ucsd-cse15l-f22/list-methods-corrected` in the terminal after fixing the bug:
![Symptoms_Fixed](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/daab7b40-fb53-410b-867a-79196b055ce6)
  
And this is the file structure afterwards:  
![FileDirectoryStructure_Fixed](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/c7453c40-ecdb-4416-8c92-a72095a910f9)

Thank you for the suggestions! It works as expected now.

---
(P.S. I've never been a TA or a tutor before so my scenario might have been a little out of touch. Sorry!)

## Part 2
Something I learned from the second half of the quarter is writing my own grading script and learning more detail about Vim. I've heard of scripts before and what it can do but I find it really cool to be able to write one on my own now. Since I'm in CSE 30 along with CSE 15L, I was already aware of Vim long before we actually used it in lab. But since CSE 30 assumes I know Vim from this class, navigating Vim was a nightmare so it's nice to actually be able to learn how to use Vim quickly during one of the labs. 
