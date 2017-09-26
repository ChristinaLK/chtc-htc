---
title: "Submitting a Job"
questions: 
- "How do you submit jobs using a scheduling program like HTCondor?"
objectives:
- "Write a list describing what information the scheduler needs to know."  
- "Create a submit file from a template."
- "Explain what each line of the submit file does."  
keypoints:
- "A submit file tells the job scheduler information like resource requirements, 
software and data requirements, and what commands to run."
---

> ## Log in
> 
> [This page](http://chtc.cs.wisc.edu/connecting#login) has 
> information about how to log into the submit 
> server.  If you already have an account in CHTC, log into 
> the submit server where your account was created.  If you 
> don't already have a CHTC account, you'll be logging into 
> `learn.chtc.wisc.edu`.  
{: .challenge}

> ## Information Wanted
> 
> Before we go further, what information do you think the scheduler
> needs to know to run your job successfully?  Make a list with your 
> neighbor.  
{: .challenge}

## Information in Submit File

The submit file needs to contain the following information: 

* What to run
* What files and software you need
* How many standard resources you need (CPUs, memory, disk)
* Where to record data about the job
* Special requirements: GPUs, access to Gluster, a certain operating system
* How many jobs you want to run

## Sample Submit File

This is a sample HTCondor submit file that includes all the information 
from the list above for a simple job.  

~~~
universe = vanilla

log = hello-chtc_$(Cluster).log
error = hello-chtc_$(Cluster)_$(Process).err
output = hello-chtc_$(Cluster)_$(Process).out

executable = hello-chtc.sh
arguments = $(Process)

should_transfer_files = YES
when_to_transfer_output = ON_EXIT
# transfer_input_files = file1,/absolute/pathto/file2,etc

request_cpus = 1
request_memory = 1GB
request_disk = 1MB

queue 3
~~~
{: .source}

The `executable` (which we'll create below) is what we want the job to 
actually run.  For this example, it will be a simple shell script.  Our 
script will also take a single argument, which is provided by the `arguments` line. 
The `log`, `output` and `error` files all track information printed by the job or 
about the job (and we'll learn more after we submit the job).  

The "transfer files" lines all tell HTCondor what to do with output and input 
files.  We'll cover the `transfer_input_files` line in a later part of the lesson.  

The `request_` lines tell HTCondor how many resources on the computer that you 
need to run your jobs.  

The final `queue` statement actually creates a job when the submit file is 
submitted.  In this example, `queue 3` means that three separate jobs will be 
submitted.  These jobs will each have a unique "Process" number assigned by 
HTCondor, and wherever you see `$(Process)` in the submit file above, that 
variable will be replaced by the process number for that job.  

> ## Create a submit file
> 
> Create a file called `hello-chtc.sub` as shown above. 
{: .challenge}


## Sample Executable

~~~
#!/bin/bash

echo "Hello CHTC from Job $1 running on `whoami`@`hostname`"
ls -lh
sleep 120
~~~
{: .bash}

> ## Create the executable
> 
> Create a file called `hello-chtc.sh` as shown above.  Give it 
> executable permissions by running: 
> ~~~
> chmod +x hello-chtc.sh
> ~~~
> {: .bash}
{: .challenge}