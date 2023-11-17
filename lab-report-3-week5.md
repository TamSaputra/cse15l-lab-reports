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
   ```
   $ grep -v "we" technical/911report/preface.txt
   


            PREFACE
            We present the narrative of this report and the recommendations that flow from it to
                the President of the United States, the United States Congress, and the American
                people for their consideration. Ten Commissioners-five Republicans and five
                Democrats chosen by elected leaders from our nation's capital at a time of great
                partisan division-have come together to present this report without dissent.
            We have come together with a unity of purpose because our nation demands it.
                September 11, 2001, was a day of unprecedented shock and suffering in the history of
                avoid such tragedy again?
                Commission on Terrorist Attacks Upon the United States (Public Law 107-306, November
                27, 2002).
                relating to the terrorist attacks of September 11, 2001," including those relating
                to intelligence agencies, law enforcement agencies, diplomacy, immigration issues
                and border control, the flow of assets to terrorist organizations, commercial
                aviation, the role of congressional oversight and resource allocation, and other
                individuals in ten countries. This included nearly every senior official from the
                current and previous administrations who had responsibility for topics covered in
                our mandate. We have sought to be independent, impartial, thorough, and nonpartisan.
                public testimony from 160 witnesses.
            Our aim has not been to assign individual blame. Our aim has been to provide the
                fullest possible account of the events surrounding 9/11 and to identify lessons
                learned.
            We learned about an enemy who is sophisticated, patient, disciplined, and lethal. The
                enemy rallies broad support in the Arab and Muslim world by demanding redress of
                political grievances, but its hostility toward us and our values is limitless. Its
                purpose is to rid the world of religious and political pluralism, the plebiscite,
                targets. Collateral damage is not in its lexicon.
            We learned that the institutions charged with protecting our borders, civil aviation,
                and national security did not understand how grave this threat could be, and did not
                adjust their policies, plans, and practices to deter or defeat it. We learned of
                sharing information across a large and unwieldy government that had been built in a
                different era to confront different dangers.
                We hope that the terrible losses chronicled in this report can create something
                together as a nation. The test before us is to sustain that unity of purpose and
                meet the challenges now confronting us. We need to design a balanced strategy for
                the same time protecting our country against future attacks. We have been forced to
                think about the way our government is organized. The massive departments and
                accountability.
                Commissioners, whose dedication to this task has been profound. We have reasoned
                together over every page, and the report has benefited from this remarkable
                dialogue. We want to express our considerable respect for the intellect and judgment
            We want to thank the Commission staff. The dedicated professional staff, headed by
                Philip Zelikow, has contributed innumerable hours to the completion of this report,
                setting aside other important endeavors to take on this all-consuming assignment.
                They have conducted the exacting investigative work upon which the Commission has
                built. They have given good advice, and faithfully carried out our guidance. They
                have been superb. We thank the Congress and the President. Executive branch agencies
                have searched records and produced a multitude of documents for us. We thank
                insight. The PENTTBOM team at the FBI, the Director's Review Group at the CIA, and
                Inspectors General at the Department of Justice and the CIA provided great
                to detail, and readiness to share what they have learned. We have built on the work
                fine work helped us get started. We thank the City of New York for assistance with
                documents and witnesses, and the Government Printing Office and W.W. Norton
                & Company for helping to get this report to the broad public.
            We conclude this list of thanks by coming full circle: We thank the families of 9/11,
                whose persistence and dedication helped create the Commission. They have been with
                us each step of the way, as partners and witnesses. They know better than any of us
                every knowledgeable person or found every relevant piece of paper. New information
                inevitably will come to light. We present this report as a foundation for a better
                understanding of a landmark in the history of our nation.
            We have listened to scores of overwhelming personal tragedies and astounding acts of
                heroism and bravery. We have examined the staggering impact of the events of 9/11 on
                the American people and their amazing resilience and courage as they fought back. We
                have admired their determination to do their best to prevent another tragedy while
                preparing to respond if it becomes necessary. We emerge from this investigation with
                enormous sympathy for the victims and their loved ones, and with enhanced respect
                for the American people. We recognize the formidable challenges that lie ahead.
            We also approach the task of recommendations with humility. We have made a limited
                most important, whose implementation can make the greatest difference. We came into
                this process with strong opinions about what would work. All of us have had to
                considered the views of others. We hope our report will encourage our fellow
                citizens to study, reflect-and act.
            Thomas H. Kean, chair
            Lee H. Hamilton, vice chair
        


   ```
   ```
   $ grep -v "the" technical/biomed/1471-2490-3-2.txt
   



        Background
        of non-contrast enhanced CT over IVU and Ultrasonography [
        2 3 4 5 ] . Its sensitivity and specificity is reported to
        be more than 95% and 96 % respectively [ 1 2 3 4 5 6 ] . An
        patient [ 7 ] . Denton [ 8 ] noted a difference of 2.5 mSv
        IVU and UHCT performed for renal colic.
        Advantages of UHCT includes rapid scan time, avoidance
        of contrast related hazards, cost effectiveness, high
        accuracy, and its ability to suggest an alternative
        diagnosis for flank pain. This last characteristic of UHCT
        is valuable in diagnosing many significant diseases earlier
        associated morbidity. In this study, we are presenting our
        initial experience of diagnosing alternative or additional
        flank pain.


        Methods
        The radiologist's reports on CT, CT films and medical
        records of 233 consecutive patients, performed between July
        2000 and August 2001 at a University Hospital for suspected
        renal/ureteral colic were reviewed. The UHCT were obtained
        on a Cti/pro single slice helical CT scanner (General
        Electrical medical systems, Milwaukee, WI). The exposure
        factors setting were KVp 130 and mAS 200-250. All scans
        contrast material. Patients were placed in supine position
        needed a better description of suspected distal ureteric
        calculi. Radiological diagnoses of clinical entities
        radiological, biochemical, serological investigations as
        well as per-operative findings were also analyzed.


        Results
        From July 19, 2000 to August 15, 2001, 233 patients had
        calculi were identified in 148 examinations (64%), findings
        of recent passage of calculi in 10 (4%) and no calculus in
        specificity of UHCT in diagnosing calculi was 99% and 98%
        respectively while +ve and -ve predictive value was 99% and
        98% respectively. Twenty-eight patients (12%) had
        ureteric or bladder stone disease) diagnosed on UHCT.
        diagnoses.
        surgical procedure, biopsy and biochemical evaluation (in
        case of pancreatitis) as shown in Table 1.


        Discussion
        A wide variety of significant or potentially significant
        diagnoses can be identified on UHCT performed for suspected
        ureteral/renal colic [ 9 10 11 12 13 ] . Apart from its
        high sensitivity and specificity for diagnosing stone
        unsuspected significant clinical entities. Early diagnosis
        of diseases such as appendicitis, cholecystitis,
        pancreatitis, diverticulitis and leaking aortic aneurysm
        associated morbidity and mortality associated with such
        diseases. In a large series of 1000 UHCT for suspected
        renal/ureteric colic, Katz [ 13 ] reported 101 patients
        (10%) with alternative or incidental diagnosis.
        on this subject.
        was 10-15%. The disease pattern is remarkably similar in
        most series (Table 2). In one report from Albert Einstein
        Medical Center, Philadelphia, Marcella et al [ 8 ] noted an
        unusually high incidence of incidentally discovered renal
        cell cancer. There is low incidence of diverticulitis in
        South Asia and we have found no case of diverticulitis in
        should be taken to rule out alternative diagnosis for flank
        pain.
        In our series, early diagnosis of pancreatitis,
        cholecystitis, mesenteric lymphadenitis, pyelonephritis and
        appendicitis, initiated early treatment. The alternative
        diagnosis of eight tumors in our series and similar trends
        diagnosed late.


        Conclusion
        A wide variety of significant alternative or additional
        diagnoses can be reliably identified on UHCT performed for
        diseases were diagnosed in 12% of cases. Unlike most series
        diverticulitis.


        Competing interests
        None declared.


        Authors' contribution
        NAA collected data and participated in manuscript
        writing




   ```
   The invert match command-line displays the line within a file that does *not* have the word in the argument. In both examples, the output that was displayed are all the lines that does not have the word/substring "we" (for the first example) and the word/substring "the" (for the second example). The command could be useful to reduce clutter when trying to read a file with a lot of text or white space.
