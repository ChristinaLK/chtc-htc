---
title: "Being a Good Citizen in CHTC"
teaching: 15
exercises: 0
questions:
- "How can I be a good citizen?"
objectives:
- "Given a CHTC policy, explain why that policy is in place."
keypoints:
- "It is important to follow your resource's policies and procedures."  
- "Have a data management plan in place before you start computing."  
---

CHTC's high throughput compute system has 100s of users and 1000s of 
jobs.  In a shared environment like this, one user's bad jobs can 
cause huge problems for not only themselves, but everybody else.   Thus it 
is imperative that everyone understand CHTC policies and 
follow them.  This episode explains what our policies are and why 
we have them.  

## Be kind to the submit node

The submit node is very busy managing lots and lots of jobs!  It doesn't 
have any extra space to run computational work.  Any true computation, or 
compilation, or anything that runs for more than a few minutes, should 
**not** be run on the submit server.  

> ## Submit Server Commands
> 
> Which of these commands would probably be okay to run on the submit server?
> 
> 1. python physics_sim.py
> 2. make
> 3. create_directories.sh
> 4. molecular_dynamics_2
> 5. tar -xzf R-3.3.0.tar.gz
> 
{: .challenge}

## Test consistently, scale gradually

Something that works for 10 jobs may not work for 10,000.  We always 
recommend running a few test jobs and then perhaps even a larger set 
before submitting a large new batch of work.  In particular, if you 
expect your jobs to be particularly "big", e.g.: 
* if your files are more than a few GB, especially input data
* if your jobs are looooooonnnnnggggg
* if you want to submit lots of jobs at once (more than 10,000)

Consult with a research computing facilitator, as we can provide the 
best way to handle these extreme cases for you and for everyone else.  

## Mange your data

CHTC has no backups of our filesystem and we have quotas on all of 
our filesystems.  You should have a plan of where you'll store all 
your results **before** you run jobs in CHTC.  You should also make 
sure that you run test jobs so that if you need a change in your quota, 
you know in advance.  

