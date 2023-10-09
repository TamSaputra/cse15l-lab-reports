# Lab Report 1 (Week 1)  
For this week's lab report, I'll be going over 3 commands we learned in week 1 lectures which are: ```cd```, ```ls```, and ```cat```.  

And for each of the commands, I'll be showing an example of:  
* Using the command with *no* argument
* Using the command with a path to a *directory* as an argument
* Using the command with a path to a *file* as an argument

For the examples, I'll be using the file structure that was cloned from [https://github.com/ucsd-cse15l-f23/lecture1](https://github.com/ucsd-cse15l-f23/lecture1) into the EdStem workspace where all of the example screenshots will be taken from.  

## Commands
1. ```cd``` command
  ![cdNoArgs](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/b7531845-a632-4a3c-be9c-da86be0b667e)
    * Working directory: ```/home/lecture1```
    * ```cd``` stands for "change directory". Since there is no argument, the working directory doesn't move and goes back to the parent directory.
    * Using the command with no argument doesn't throw out an error.
  
  ![cdDirectory](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/8da23ee1-0972-4ea0-9935-8f4bca6c6d81)  
     * Working directory: ```/home```
     * When giving a directory as an argument, the command will change the working directory into the directory specified in the argument.
     * Using the command with a directory as an argument doesn't throw out an error.
  
  ![cdFile](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/668e0343-c386-433e-bda9-0b626fd3ee60)  
     * Working directory: ```/home/lecture1```
     * When giving a file as an argument, it will throw out an error indicating that the file isn't a directory.
     * As the name of the command ```cd``` implies, it changes the directory. So when the argument is a file, it throws out an error because we can't have a file as a working directory.

2. ```ls``` command
  ![lsNoArgs](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/e7df6be9-fd4e-46fb-b57c-53b7d734bffa)
     * Working directory: ```/home/lecture1```
     * Even with no argument, the command lists the content of the current working directory which in this case is ```lecture1```.
     * Using the command with no argument doesn't throw out an error.
  
  ![lsDirectory](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/396dba20-6b68-476c-9ba9-352d8b3cc452)
     * Working directory: ```/home/lecture1```
     * The ```ls``` command takes in the argument and prints the content of the directory specified in the argument, in this case, ```messages```
     * Using the command with a directory as an argument doesn't throw out an error. 
  ![lsFile](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/8449e7ba-f921-4360-9d46-5592754a68f8)
     * Working directory: ```/home/lecture1```
     * The ```ls``` command accepts file as an argument but since it's not a directory, it only "list" the name of the file in the argument instead of the content of the file.
     * Using the command with a file as an argument doesn't throw out an error (although it doesn't exactly "list" anything). 
  
3. ```cat``` command
![catNoArgs](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/c290cbca-47f9-4f02-bde4-c87f55dfbd5f)
     * Working directory: ```/home```
     * Using the command with no argument seems to take in user input and duplicate it into the terminal. Unless stopped using ```ctrl + d```, it "locks up" the terminal and will continue duplicating the input since there is no argument.
     * It doesn't throw an error but it also doesn't seem to be its intended use.
![catDirectory](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/afa9c63d-6310-480c-8931-7ed87d01f7fd)
     * Working directory: ```/home```
     * The command ```cat``` displays the content of a file. It throws an error since ```lecture1``` is a directory instead of a file.
     * Note: If ```ls``` displays the content of a *directory*, then ```cat``` displays the content of a *file*.
![catFile](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/93de5160-ac93-426f-a990-a552b73185ba)
     * Working directory: ```/home```
     * The output is the content of the file specified in the argument which in this case is ```README```. So ```cat``` displays the content of a file and that's what we see in the output of the command.
     * It doesn't throw out an error.
  

  PS: Sorry for the terrible formatting. I can't get the nested list to work properly for some reason.
     
