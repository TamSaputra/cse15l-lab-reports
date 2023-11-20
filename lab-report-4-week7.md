# Lab Report 4 (Week 7)
For this lab report, I'll be doing steps 4-9 from the following steps (taken from [week 7 lab](https://ucsd-cse15l-f23.github.io/week/week7/#baseline)):

1. **Setup** Delete any existing forks of the repository you have on your account
2. **Setup** Fork the repository
3. **The real deal** Start the timer!
4. Log into ieng6
5. Clone your fork of the repository from your Github account (using the SSH URL)
6. Run the tests, demonstrating that they fail
7. Edit the code file to fix the failing test
8. Run the tests, demonstrating that they now succeed
9. Commit and push the resulting change to your Github account (you can pick any commit message!)

   
For each of the steps (4-9), I'll be showing a screenshot, writing down the keys pressed to do the command(s), and summarizing what effect the keys did and the command used.
  
### Step 4: Log into ieng6
![Step4](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/74611eb0-f009-4f20-a772-f357cac9d815)
Keys pressed: ```ssh<space>cs15lfa23kg@eng6.ucsd.edu<enter>```  
The keys pressed are just the regular command to log into ieng6. Usually I would use the up arrow but since this is my first time logging in to ieng6 on a new terminal, there is no history for me to "scroll" through.

### Step 5: Clone your fork of the repository from your Github account (using the SSH URL)
![Step5](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/18bb84f4-63a3-48f4-8ab6-b4c38ebb04be)
Keys pressed: ```git<space>clone<space><CTRL + 'v'><enter>```  
I typed out the ```git clone``` command and then used ```CTRL + 'v'``` to paste the SSH link from the fork of the repository (and I copied the SSH link by clicking on the overlapping square next to SSH link). Pressing enter runs the command, as usual.

### Step 6: Run the tests, demonstrating that they fail
![Step6](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/f5dff59a-9249-46ff-833e-1841b66da517)
Keys pressed: ```cd<space>l<tab><enter>```, ```ls```, ```bash<space>t<tab><enter>```  
First, I ran the ```cd``` command to move my working directory into the ```lab7``` directory. After typing ```cd l```, I pressed the ```tab``` key which auto-completes to ```lab7/```. I then used the ```ls``` command to see the content of the ```lab7``` directory and ran the tests using the provided bash script. Similar to how I typed the ```cd``` command, I started by typing ```bash t``` and pressing ```tab``` which auto-completes to ```test.sh ```.
