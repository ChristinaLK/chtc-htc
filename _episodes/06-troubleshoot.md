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

> Run test jobs / interactive jobs.  

> Where can jobs fail?  Answer: scheduler/hardware issue, software issue, etc...

> Where to find answers: out/error/log files, 

> How to write a good email to ask for help: describe problem, what you 
> expected, what you saw instead.  

> callout for common bash scripting error w/ ^M line endings

> ## Windows/Linux Error
> 
> Do you have a Windows computer? Did your job go on hold with an error like this?  
> 
> > Error from slot1_11@e189.chtc.wisc.edu: Failed to execute 
> > '/var/lib/condor/execute/slot1/dir_4086540/condor_exec.exe' with 
> > arguments 2: (errno=2: 'No such file or directory')
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
> > vi -b hello-chtc.sh
> {: .bash}
> If you see `^M` characters at the end of each line, those 
> are the DOS line endings and that's the problem. 
> (Type `:q` to quit vi)
>
> Luckily, there is an easy fix!  To convert the script to 
> unix line endings so that it will run correctly, you can run: 
> > dos2unix hello-chtc.sh
> {: .output}
> on the submit node and it will change the format for you.  If you 
> release your held jobs (using `condor_release`) or 
> re-submit the jobs, you should no longer get the same error.  

{: .callout}
