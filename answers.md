1. Unless the command is specifically designed to use multiple cores it will be running on one core.
2. You can look at the manual of the command to see if there is any information on how many cores, memory or what files it reqires to be run efficiently. If not found you may design a test case and run the command on the test in order to gain further insights about it.
3. The following code will run the ls -l command and will record the run stats in a file called "run_stat.txt", the "Maximum resident set size" line refers to the peak of memory use and the "System time" line refers to the time it took to run.

```
/usr/bin/time -v -o run_stat.txt ls -l
```

4. The units of the previous answer is in kbytes.
5. The following code looks for the file and see if it is empty or not:

```
if [[ -f "file_of_interest" && -s "file_of_interest" ]]; then 
    echo "exist and not empty"
else 
    echo "not exist or empty"; 
fi
```

6. Only use the first part of the if condition [-f "file_of_interest] with the expected output file and change the first statement to launch the job on hpc (qsub job)

7. no it wouldn't work, because of differences in the operating systems and different built in time. (you may install GNU-time and use that to get the run time for a program)

8. To ensure that the compute node has the required RAM for our job we can use the -l h_vmem=24G option in the qsub command, bearing in mind that this is the required memory per processor and if we know that the job requires two core then we need to set this value to 12G (2*12 = 24G). Here is a skeleton HPC script that asks for a node with 6 core available and (6*4=24G) available memory.

```
#!/bin/bash
#$ -N my_job
#$ -q pub64
#$ -pe openm 6
#$ -l h_vmem=4G
```

