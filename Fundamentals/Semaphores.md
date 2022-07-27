Semaphore is simply an integer variable that is shared between [[Threads]]. This variable is used to solve the critical section problem and to achieve process synchronization in the multiprocessing environment.

**Semaphore is always initialized to 1**

Semaphores are of two types:
1.  **Binary Semaphore –**   
    This is also known as mutex lock. It can have only two values – 0 and 1. Its value is initialized to 1. It is used to implement the solution of critical section problems with multiple processes.
2.  **Counting Semaphore –**   
    Its value can range over an unrestricted domain. It is used to control access to a resource that has multiple instances.

Semaphore has 2 operations -
1. Wait
``` 
Wait(Semaphore s) {
	while(s == 0); // wait until s = 0
	s--;
}
```

2. Signal
```
signal(Semaphore s) {
	s++;
}
```
