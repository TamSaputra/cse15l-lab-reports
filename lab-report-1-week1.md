# Lab Report 1 (Week 1)  
For this week's lab report, I'll be going over 3 commands we learned in week 1 lectures which are: ```cd```, ```ls```, and ```cat```.  

And for each of the commands, I'll be showing an example of:  
* Using the command with *no* argument
* Using the command with a path to a *directory* as an argument
* Using the command with a path to a *file* as an argument

For the examples, I'll be using the file structure that was cloned from [https://github.com/ucsd-cse15l-f23/lecture1](https://github.com/ucsd-cse15l-f23/lecture1) into the EdStem workspace where all of the example screenshots will be taken from.  

## Commands
1. ```cd```
![cdNoArgs](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/b7531845-a632-4a3c-be9c-da86be0b667e)
    * Working directory: ```/home/lecture1```
    * ```cd``` stands for "change directory". Since there is no argument, the working directory doesn't move and goes back to the parent directory.
    * Using the command with no argument doesn't throw out an error.
  
![cdDirectory](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/8da23ee1-0972-4ea0-9935-8f4bca6c6d81)  
    * Working directory: ```/home```
    * When giving a directory as an argument, the command will change the working directory into the directory specified in the argument.
    * Using the command with no argument doesn't throw out an error.
  
![cdFile](https://github.com/TamSaputra/cse15l-lab-reports/assets/112127930/668e0343-c386-433e-bda9-0b626fd3ee60)  
    * Working directory: ```/home/lecture1```
    * When giving a file as an argument, it will throw out an error indicating that the file isn't a directory.
    * As the name of the command ```cd``` implies, it changes the directory. So when the argument is a file, it throws out an error because we can't have a file as a working directory.

2. ```ls```
