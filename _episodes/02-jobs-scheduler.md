---
title: "Jobs and Scheduling"
questions:
- "What is a job?"
- "How is a large-scale compute system organized?"
- "What is a scheduling program?"  
objectives:
- "Describe the role of a batch scheduler."
- "Explain why large, shared computing systems use a scheduling program." 
keypoints:
- "A job consists of a computational task, usually defined by input data and a piece of software, producing output data."  
- "Most large scale systems consist of a head node for logging in and submitting jobs, where jobs are performed on worker nodes."  
- "A batch scheduler controls where and when jobs run on the worker nodes."  
---

## Job basics

A job is one task that you want to run.  In a high throughput computing 
system, the idea is to submit many jobs so they can run simultaneously, 
thus saving you time overall.  

Most jobs can be thought of as having three main parts: 

> image w/ input, program output

The **input** is anything that the program needs to run.  While this 
includes input files with data or parameters, it can also include things 
like software installations, reference, or configuration files.  Input 
may not even be a file, but an argument that you pass to the program.  

The main work of the job is done by the **program** (also called the 
**executable**).  Sometimes the executable is the main program you want 
to run; sometimes it's a script that runs a program, sometimes it's a 
script that calls other scripts.  An important requirement for this piece 
of the job is that it can be run from the command line.  

Finally, the job will produce some kind of **output**, usually in the form 
of output files.  

> ## Your jobs
>
> Write out what pieces will go into your job. 
{: .challenge}

## Scheduling basics

Using a large-scale, shared system, is different than running a program 
on your own computer.  On your own computer, you can run a program directly, 
by just typing in a command.  

On our high throughput system, there are two complications.  First, you want 
to run the program many times -- it would be tedious to log into 1000 computers 
so that you could start 1000 jobs.  Second, our computers are being 
shared by all CHTC users -- someone has to decide who gets to use which computer 
when.  

To solve these problems, we use a program called a *batch scheduler* on the 
HTC system.  The scheduler is a program that runs on all of our computers and 
assigns (or schedules) jobs to run on them.  To run work on CHTC, you log into 
a submit server and submit your jobs to the scheduler.  

> insert image here

> ## Job scheduling roleplay
> 
> Your instructor will divide you into groups taking on 
> different roles in the HTC system (users, compute nodes 
> and the scheduler).  Follow their instructions as they 
> lead you through this exercise.  You will be emulating 
> how a job scheduling system works on the HTC system.  
{: .challenge}

> ## Our HTC Scheduler: HTCondor
> 
> The scheduling program we use on CHTC's high throughput system is 
> [HTCondor](https://research.cs.wisc.edu/htcondor/).  HTCondor is 
> used all over the world for different compute systems and is developed 
> here at CHTC.  We use HTCondor for our HTC system because it is 
> optimized for managing many jobs submitted in parallel. 
{: .callout}

In the next part of the lesson, we'll describe exactly how to use 
the HTCondor scheduler to submit jobs.  
