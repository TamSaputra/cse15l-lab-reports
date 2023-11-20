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
Commands ran: ```sssh cs15lfa23kg@ieng6.ucsd.edu```  
The keys pressed are just the regular command to log into ieng6. Usually I would use the up arrow but since this is my first time logging in to ieng6 on a new terminal, there is no history for me to "scroll" through.
  
### Step 5: Clone your fork of the repository from your Github account (using the SSH URL)
![Step5](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/18bb84f4-63a3-48f4-8ab6-b4c38ebb04be)
Keys pressed: ```git<space>clone<space><ctrl + 'v'><enter>```  
Commands ran: ```git clone git@github.com:TamSaputra/lab7.git```  
I typed out the ```git clone``` command and then used ```<ctrl + 'v'>``` to paste the SSH link from the fork of the repository (and I copied the SSH link by clicking on the overlapping square next to SSH link). Pressing enter runs the command, as usual.
  
### Step 6: Run the tests, demonstrating that they fail
![Step6](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/f5dff59a-9249-46ff-833e-1841b66da517)
Keys pressed: ```cd<space>l<tab><enter>```, ```ls<enter>```, ```bash<space>t<tab><enter>```  
Commands ran: ```cd lab7/ ```, ```ls```, ```bash test.sh ```
First, I ran the ```cd``` command to move my working directory into the lab7 directory. After typing ```cd l```, I pressed the ```<tab>``` key which auto-completes to ```lab7/```. I then used the ```ls``` command to see the content of the lab7 directory and ran the tests using the provided bash script. Similar to how I typed the ```cd``` command, I started by typing ```bash t``` and pressing ```<tab>``` which auto-completes to ```test.sh ```.
  
### Step 7: Edit the code file to fix the failing test
![Step7Part1](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/92991d84-01e2-4f17-ba3c-294923b6304f)
![Step7Part2](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/bedbf0c7-afbc-48f9-8416-571266ce515c)  
Keys pressed: ```vim<space>L<tab>.<tab><enter>```, ```/index1<enter>```, ```nnnnnnnnnexi2<esc>:wq<enter>```  
Commands ran: ```vim ListExamples.java```  
Similar to the previous step, I first typed out ```vim L``` and pressed ```<tab>``` to auto-complete the command into ```vim ListExamples```. I then pressed `.` and `<tab>` to then auto-complete it to the final command `vim ListExamples.java` before pressing `<enter>` to run it. The command then opens ListExamples.java in Vim where I searched for "index1" by pressing `/index1` and pressing enter. Then pressing `n` 9 times would bring the cursor to the index1 that needs to be changed. `e` brings the cursor to the end of the word, `x` deletes the letter the cursor is currently on, `i2` opens insert mode and enters 2, `<esc>` exits the insert mode back to normal mode in Vim, and finally, `:wq<enter>` to write (or save) the file and quit Vim.
  
### Step 8: Run the tests, demonstrating that they now succeed
![Step8](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/f39adf68-2020-41a8-8394-92c530a499d9)  
Keys pressed: `<up arrow><up arrow><enter>`  
Commands ran: `bash test.sh `  
The up arrow scrolls through the history of commands that was used before. Since I used `bash test.sh` in step 6, I simply pressed the up arrow twice and press `<enter>` to run the `test.sh` script.

### Step 9: Commit and push the resulting change to your Github account (you can pick any commit message!)
![Step9](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/976c15e0-7aec-4c63-89eb-f2977b7af8b1)  
Keys pressed: `git<space>add<space>L<tab>.j<tab><enter>`, `git<space>commit<space>-m<space>"Fixed<space>ListExamples.java"<enter>`, `git<space>push<enter>`  
Commands ran: `git add ListExamples.java`, `git commit -m "Fixed ListExamples.java"`, `git push`  
For the first command, I typed `git add L`, pressed `<tab>`, typed in `.j` and `<tab>` again which auto-completes to `git add ListExamples.java`. Then the commit command, there wasn't much shortcut except for using the `-m` flag which skips having to write the commit message in Vim. In the end, I just typed the full commit command and the message and pressed `<enter>`. There's also no shortcut to push so I just typed the full command: `git push`.
