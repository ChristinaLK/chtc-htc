---
title: "Understanding Job Output"
questions:
- "How do I know if my job has run successfully?"
- "What do all the job output files mean?"
objectives:
- "Compare and contrast the different output files created by the job and what information you can learn from each."
- "Determine when a job started and completed."  
keypoints:
- "Successful jobs leave the queue, bring back output files, and have no errors."
- "Log files tell when and where a job waited and ran, and how many resources it used."
- "Output files capture any general information printed by the job's executable."
- "Error files capture any errors that printed when the job executable ran."
---

How do you know if your job ran successfully?  Usually, there are a few signs: 
* the job exited the queue and didn't go on hold (more on that soon)
* any files that capture error messages are empty
* you get the expected results or output

One way to determine this information is by looking at the different output files 
created by the job.  Below are the three standard output files types 
and what information you can learn from each one: 

## Log

The log file contains information that HTCondor tracks for each job, 
including when it was submitted, started, and stopped. It also 
describes resource use, and where the job ran. 

## Output

The "output" file contains any information that would normally have 
been printed to the terminal if you were running the script/program 
yourself from the command line. It can be useful for figuring out 
what went right/wrong inside your program, or simply to measure a job's progress. 

In the case of our example script, we expected it to print a message 
and we would want to check the "output" files to see if that happened.  

## Error

The error file contains any errors that would normally have been printed 
to the terminal if you were running the script/program yourself from the 
command line. This is a good place to look first if you think your code 
triggered an error. 

> ## Review
> 
> Which lines in the submit file create these files?  
{: .challenge}

> ## Finding Out Information
> 
> Looking at your output files, try answering the following questions.  
> 
> 1. How long did your jobs have to wait before they started?  Which file has this information?  
> 2. Which server did the job run on?  Which file(s) have this information?  
> 3. How much disk space did the job use?  Which file has this information?  
{: .challenge}