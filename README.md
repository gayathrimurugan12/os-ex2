# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to print process ID and parent Process ID using Linux API system calls
```
#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
int main(void)
{	//variable to store calling function's process id
	pid_t process_id;
	//variable to store parent function's process id
	pid_t p_process_id;
	//getpid() - will return process id of calling function
	process_id = getpid();
	//getppid() - will return process id of parent function
	p_process_id = getppid();
	//printing the process ids
  printf("The process id: %d\n",process_id);
	printf("The process id of parent function: %d\n",p_process_id);
	return 0; 
 }
```
```
$ gcc -o pid.o pid.c
 ./pid.o
```
## OUTPUT
```
The process id: 97
The process id of parent function: 62
```
$ ps
```
PID   USER     TIME  COMMAND
    1 root      0:01 {init} /bin/sh /sbin/init
    2 root      0:00 [kthreadd]
    3 root      0:00 [kworker/0:0]
    4 root      0:00 [kworker/0:0H]
    5 root      0:00 [kworker/u2:0]
    6 root      0:00 [mm_percpu_wq]
    7 root      0:00 [ksoftirqd/0]
    8 root      0:00 [kdevtmpfs]
    9 root      0:00 [oom_reaper]
   10 root      0:00 [writeback]
   11 root      0:00 [kcompactd0]
   12 root      0:00 [crypto]
   13 root      0:00 [bioset]
   14 root      0:00 [kblockd]
   15 root      0:00 [kworker/0:1]
   16 root      0:00 [kswapd0]
   17 root      0:00 [bioset]
   34 root      0:00 [khvcd]
   35 root      0:00 [bioset]
   36 root      0:00 [bioset]
   37 root      0:00 [bioset]
   38 root      0:00 [bioset]
   39 root      0:00 [bioset]
   40 root      0:00 [bioset]
   41 root      0:00 [bioset]
   42 root      0:00 [bioset]
   43 root      0:00 [kworker/u2:1]
   56 root      0:00 settime -d /
   57 root      0:00 dhcpcd -q
   62 root      0:00 sh -l
   98 root      0:00 ps
```
## C Program to create new process using Linux API system calls fork() and exit()
```
#include <stdio.h>
#include<stdlib.h>
int main()
{ 
int pid; 
pid=fork(); 
if(pid == 0) 
{ 
printf("Iam child my pid is %d\n",getpid()); 
printf("My parent pid is:%d\n",getppid()); 
exit(0); 
} 
else{ 
printf("I am parent, my pid is %d\n",getpid()); 
sleep(100); 
exit(0);
} 
}
```
```
$ gcc -o fork.o fork.c
./fork.o
```
## OUTPUT:
```
I am parent, my pid is 130
Iam child my pid is 131
My parent pid is:130
```
## C Program to execute Linux system commands using Linux API system calls exec() family

```
#include <stdio.h>
#include <unistd.h>
#include <stdlib.h>
#include <sys/wait.h>
#include <sys/types.h>
int main()
{
        int status;
        printf("Running ps with execlp\n");
        execl("ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                printf("child did not exit successfully\n");
                printf("Done.\n");
                printf("Running ps with execlp. Now with path specified\n");
                execlp("/bin/ps", "ps", "ax", NULL);
        wait(&status);
        if (WIFEXITED(status))
                printf("child exited with status of %d\n", WEXITSTATUS(status));
        else
                printf("child did not exit successfully\n");
        printf("Done.\n");
        exit(0);
}
```
```
$ gcc -o exec.o exec.c
$ ./exec.o
```
## OUTPUT
```
Running ps with execlp
PID   USER     TIME  COMMAND
    1 root      0:01 {init} /bin/sh /sbin/init
    2 root      0:00 [kthreadd]
    3 root      0:00 [kworker/0:0]
    4 root      0:00 [kworker/0:0H]
    5 root      0:00 [kworker/u2:0]
    6 root      0:00 [mm_percpu_wq]
    7 root      0:00 [ksoftirqd/0]
    8 root      0:00 [kdevtmpfs]
    9 root      0:00 [oom_reaper]
   10 root      0:00 [writeback]
   11 root      0:00 [kcompactd0]
   12 root      0:00 [crypto]
   13 root      0:00 [bioset]
   14 root      0:00 [kblockd]
   15 root      0:00 [kworker/0:1]
   16 root      0:00 [kswapd0]
   17 root      0:00 [bioset]
   34 root      0:00 [khvcd]
   35 root      0:00 [bioset]
   36 root      0:00 [bioset]
   37 root      0:00 [bioset]
   38 root      0:00 [bioset]
   39 root      0:00 [bioset]
   40 root      0:00 [bioset]
   41 root      0:00 [bioset]
   42 root      0:00 [bioset]
   55 root      0:00 settime -d /
   56 root      0:00 dhcpcd -q
   61 root      0:00 sh -l
   62 root      0:00 [kworker/u2:1]
  192 root      0:00 ps ax
```

# RESULT:
The programs are executed successfully.
