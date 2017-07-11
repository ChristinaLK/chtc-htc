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
