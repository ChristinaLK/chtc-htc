---
title: "Life Cycle of a Job"
questions:
- "What steps does a job go through?"
- "How do I track my job's progress?"  
objectives:
- "Draw a diagram of the steps your job goes through."
keypoints:
- "Jobs may go through various states in the queue, and can be monitored by a queue command." 
---

Once we submit a job (or multiple jobs), what happens behind the scenes?  A
typical job will be submitted (which we just did), wait, run, and complete.  

## Idle 

HTCondor 
places jobs into the job queue -- the list of all jobs waiting to run.  We can 
look at our own jobs at the queue by running: 

~~~
$ condor_q
~~~
{: .bash}

> ## Check the queue
> 
> Run the `condor_q` command to check on your jobs.  To see all of the jobs 
> in the queue, run `condor_q -all`.  
{: .challenge}

## Running

Once the HTCondor program finds a place for a job to run, it will start the 
job. If you run `condor_q` again, you will see 
that your jobs have transitioned from the "Idle" to the "Run" column.  

In the background, HTCondor has created a new directory on the server where 
your job is running.  It then transfers your executable and any files listed 
in "transfer_input_files" to that directory.  Finally it runs the executable 
inside.  This is why it is important to make sure that your scripts and 
programs don't have paths that include `/home/` or similar -- your job won't 
be able to access files at that path when it runs.  

## Complete

> ## Done?
> 
> How can you know if your jobs have completed?  
{: .challenge}

When jobs complete, they leave the queue.  So if you run `condor_q` and don't 
have any jobs, that means they all finished (successfully or not).  

Any new files (but not sub-directories!) that were created as part of the job 
will return to the submit server automatically.  

## Other Job States

Sometimes your job might go on hold.  This is an indication of an error 
and will be covered in two episodes.  

It's also possible to manually change the state of your job instead of 
waiting for HTCondor do it.  You can't make your job run, but you can always: 

* remove a job yourself
~~~
condor_rm JobId
~~~
{: .bash}

* put a job on hold yourself
~~~
condor_hold JobId
~~~
{: .bash}