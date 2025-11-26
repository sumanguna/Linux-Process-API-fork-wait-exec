<img width="1051" height="825" alt="image_1" src="https://github.com/user-attachments/assets/26b8b48e-870d-4b20-8d19-035ad1f020fd" /># Linux-Process-API-fork-wait-exec-
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

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```
DEVELOPED BY : SUMAN 
REGISTER NO : 212223240163
```

```C
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}
```

## OUTPUT
<img width="799" height="708" alt="Screenshot 2025-11-26 112218" src="https://github.com/user-attachments/assets/82202e87-98fc-48e4-86d0-77d9a5c23a23" />
<img width="892" height="706" alt="Screenshot 2025-11-26 112256" src="https://github.com/user-attachments/assets/2fc43781-fa16-4e13-9daa-650bcce15177" />
<img width="1404" height="734" alt="Screenshot 2025-11-26 112344" src="https://github.com/user-attachments/assets/d6f5a945-373c-404b-b30b-63877fc92980" />



## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```C
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}
```


## OUTPUT

<img width="1120" height="928" alt="Screenshot 2025-11-26 111917" src="https://github.com/user-attachments/assets/09ed7322-813f-4fb2-9e53-1181aa17eb0d" />
<img width="1420" height="598" alt="Screenshot 2025-11-26 111856" src="https://github.com/user-attachments/assets/a760efb0-ca23-43bb-8caf-a21448f3d4e6" />






# RESULT:
The programs are executed successfully.
