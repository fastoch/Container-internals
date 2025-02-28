# Container-internals

"Understanding Container Internals" by Joshua Jebaraj.  
https://www.youtube.com/watch?v=9ivFrXgB2Zg  

---

# Namespaces

Introduced in Linux kernel version 2.6.24 in **2008**, namespaces define the set of resources that a process can use and interact with.  
They partition kernel resources, allowing one specific set of processes to see one specific set of resources.   

Linux namespaces are a crucial feature for process isolation and resource management.  
They allow the creation of **separate environments within a single Linux system**, each with its own view of system resources.  

There are 7 types of namespaces in Linux, each isolating different aspects of the system:
- **PID** namespace: Isolates process IDs
- **NET** namespace: Isolates network interfaces
- **MNT** namespace: Isolates filesystem mount points
- **UTS** namespace: Isolates hostname and domain name
- **IPC** namespace: Isolates interprocess communication resources
- **USER** namespace: Isolates user and group IDs
- **CGROUP** namespace: Isolates the virtual cgroup filesystem

## Important System Calls

3 important system calls are commonly used with namespaces:
- **clone()**: used to create child processes and can be highly parameterized using flags.
  - It's more versatile than the legacy **fork()** call and can also create threads.
- **unshare()**: disables sharing a namespace with the parent process, effectively creating a new namespace without spawning a new process (except for PID namespaces).
- **setns()**: used to attach a process to an existing namespace.
  - It takes a file descriptor of a symbolic link representing a specific namespace and an optional namespace type check parameter.

These system calls are fundamental for creating and managing namespaces, which are essential for containerization, process isolation, and resource management in modern Linux systems.

## UTS namespace

A Linux feature that isolates the **hostname** and domain name system (DNS) **domain** of a process from the host system.  

- Let's create a new UTS namespace from the CLI: `unshare --uts`
- then, let's change the hostname to `demo` in the same terminal window via `hostname demo`
- if we run `hostname`, we'll get `demo`
- now, if we open a new terminal window and check the hostname, we'll see that the hostname hasn't changed there
  
![image](https://github.com/user-attachments/assets/50f3cf07-d49c-41db-8c6c-eb7e40945de4)

- if we run `exit` to exit the namespace, we'll see that the hostname hasn't changed outside of the namespace

![image](https://github.com/user-attachments/assets/f9abe2d9-f04b-4a7e-8d54-2fda02dd9463)

## IPC namespace

**Inter-Process Communication** namespace is a Linux feature that isolates the IPC resources of a process from the host system.  
IPC resources include message queues, semaphores, shared memory segments, etc.  

To create a new IPC namespace: `unshare --ipc`




@12/48
