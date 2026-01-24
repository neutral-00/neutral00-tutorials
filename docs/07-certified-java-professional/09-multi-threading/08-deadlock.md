# Deadlock

It is a situation in multithreading where two or more thread are holding some resource and waiting indefinitely for more resource. None of the threads are releasing the resources leading to indefinite waiting.

Deadlocks typically occure when 4 conditions are met simultaneously.

1. Mutual Exclusion: Only one thread can access a resource at a time.
2. Hold and Wait: A thread is holding atleast one resource and waiting to acquire additional resource held by other threads.
3. No Preemption: Resources can not be forcibly taken from threads holding them.
4. Circular Wait: A set of threads is waiting for each other in a circular chain.


## Code example 


