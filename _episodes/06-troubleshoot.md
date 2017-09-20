---
title: "Troubleshooting and Interactive Jobs"
questions:
- "How can jobs fail?"  
- "How can I figure out what went wrong?"
objectives:
- "Identify files with troubleshooting information."
- "Identify 3 ways jobs can fail."  
keypoints: 
- "Always run a test job before submitting a full scale job."  
- "To test a new job, use an interactive session beore submitting."  
- "You can use log, standard output, and standard error information to determine why jobs fail." 
---

> ## Broken Script
> 
> Edit your `hello-chtc.sh` script: 
> * Delete the first line
> * Add a command at the end that says `cat my_files.txt`
> 
> Then submit the same submit file as before.  
{: .challenge}

## Debugging Job Failures

Jobs can fail in lots of different ways!  Sometimes the program you 
want to run doesn't work, there can be a problem with the server, HTCondor 
isn't matching jobs properly... the list goes on and on!  Here are 
some common problems and how to solve them.  

### Held Jobs

Let's check in on the job we just submitted.  If we run `condor_q`, we'll see 
that these jobs are in a new state -- they're not running, or idle, but on hold.  
 
~~~
condor_q
~~~
{: .bash}

~~~
-- Schedd: learn.chtc.wisc.edu : <128.104.100.43:9618?... @ 09/20/17 17:31:38
OWNER  BATCH_NAME            SUBMITTED   DONE   RUN    IDLE   HOLD  TOTAL JOB_IDS
alice CMD: hello-chtc.sh   9/20 16:40      _      _      _      3      3 36260.0-2

3 jobs; 0 completed, 0 removed, 0 idle, 0 running, 3 held, 0 suspended
~~~ 
{: .output}

We can find out why jobs are on hold by looking in the *log* file, or by running 
a special version of the `condor_q` command that gives us the *Hold Reason*.

> condor_q -af holdreason
{: .bash}

The hold reason for this job is: 
~~~
Error from slot1_6@e231.chtc.wisc.edu: Failed 
to execute '/var/lib/condor/execute/slot1/dir_7462/condor_exec.exe' with 
arguments 0: (errno=8: 'Exec format error')
~~~
{: .source}

That's pretty obscure, but in this case, means that something is wrong 
with our executable.  We deleted the first line of the script, which 
it needs to run successfully.  

> ## Fixed Script, Part I
> 
> Fix the `hello-chtc` script by adding the header back to the top: 
> ~~~
> #!/bin/bash
> ~~~
> {: .source}
> 
> Then release the held jobs by running `condor_release` with your username.  
{: .challenge}

> ## Other Common Hold Reasons
> 
> * "Disk quota exceeded": Output files can't be returned to 
> the submit node if you have reached your quota. See this page 
> for instructions on managing your quota.
> *"Job has gone over memory limit of X": Look at the resource usage table 
> in your log files - are you requesting enough memory for your jobs?
> * "Job failed to complete in 72 hrs"
{: .callout}

> ## Windows/Linux Error
> 
> Do you have a Windows computer? Did your job go on hold with an error like this?  
> 
> ~~~
> Error from slot1_11@e189.chtc.wisc.edu: Failed to execute 
> '/var/lib/condor/execute/slot1/dir_4086540/condor_exec.exe' with 
> arguments 2: (errno=2: 'No such file or directory')
> ~~~
> {: .output}
> 
> Your script may not work due to a Windows/Linux incompatibility. Files 
> written in Windows (based on the DOS operating system) and files written 
> in Mac/Linux (based on the UNIX operating system) use different invisible 
> characters to mean "end of a line" in a file. Normally this isn't a problem, 
> **except** when writing bash scripts; bash will not be able to run scripts 
> if they have the Windows/DOS line endings. 
> To check if this is the problem, you can open the script in 
> the vi text editor, using its "binary" mode:
> ~~~
> vi -b hello-chtc.sh
> ~~~
> {: .bash}
> If you see `^M` characters at the end of each line, those 
> are the DOS line endings and that's the problem. 
> (Type `:q` to quit vi)
>
> Luckily, there is an easy fix!  To convert the script to 
> unix line endings so that it will run correctly, you can run: 
> ~~~
> dos2unix hello-chtc.sh
> ~~~
> {: .output}
> on the submit node and it will change the format for you.  If you 
> release your held jobs (using `condor_release`) or 
> re-submit the jobs, you should no longer get the same error.  
{: .callout}

### Jobs with Errors 



## Preventing Job Failures

> Run test jobs / interactive jobs.  

## Asking For Help

Sometimes you might not be able to figure out what's going on with your jobs, or 
why.  Don't hesitate to email chtc@cs.wisc.edu with questions.  A good troubleshooting 
request has the following information: 

* Tell which submit server you log into
* Describe your problem:
  * What are you trying to do?
  * What did you expect to see?
  * What was different than what you expected?
  * What error messages have you received (if any)?
* Attach any relevant files (output, error, log, submit files, scripts) or 
tell which directory on the submit server where we can find these files.



> ## Optional Exercise: Can't Start
> 
> Edit your `hello-chtc.sub` submit file by adding one line: 
> ~~~
> requirements = (OpSysMajorVer == 5)
> ~~~
> {: .source}
> 
> Then submit the jobs.  Even if you wait 5-10 minutes, they probably 
> won't start running.  To see why, choose one of the JobIds and run: 
> 
> ~~~
> condor_q -better-analyze JobId
> ~~~
> {.bash}
> 
> This will print out an analysis of why your job isn't running.  
{: .challenge}