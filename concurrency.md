
# What is Channels in Go?

Channel mainly acts as a concurrency synchronization technique.


**don't (let computations) communicate by sharing memory, (let them) share memory by communicating (through channels)**

Meaning:
- Computations to exchange data through communication channels rather than directly accessing shared memory.
- Each computation can send data into a channel, and other computations can receive data from that channel.
- This approach helps avoid the data integrity issues (data race)
- Instead, we create a secure communication interface between computations, where data is only transmitted through tightly managed communication channels.-> `ensures data integrity` +  `prevents simultaneous data write conflicts`.
- enhances parallelism and efficiency in the system, as computations can operate independently and send/receive data through channels without the need for synchronizing access to shared memory.

**sum up: enhance the stability and reliability of parallel computing systems.**
## concurrency synchronization
Concurrent computations may share resources, generally memory resource. 
<br>
The following are some circumstances that may occur during concurrent computing:
- In the same period : one computation is **WRITING** data to a memory segment,another computation is **READING** data from the same memory segment.*Then the integrity of the data read by the other computation might be not preserved.*
Reference: [Race Condition](#race-condition)
- In the same period that one computation is **WRITING** data to a memory segment, another computation is also **WRITING** data to the same memory segment. Then the integrity of the data stored at the memory segment might be not preserved.

==> *These circumstances are called data races*


To Sum up:  concurrency synchronizations, or data synchronizations Is:
- duties in concurrent programming is to control resource sharing among concurrent computations, so that data races will never happen

Other duties in concurrent programming:
- determine how many computations are needed.
- determine when to start, block, unblock and end a computation.
- determine how to distribute workload among concurrent computations.

### Race condition

Abstract: 

A race condition occurs when the behavior and outcome of the computations depend on the relative timing and interleaving of their operations

If the reading computation accesses the memory segment before the writing computation completes its write operation, the reading computation may end up reading inconsistent or partially updated data. 

To ensure data integrity and avoid race conditions, synchronization mechanisms are typically employed. These mechanisms include:
- locks
- semaphores
- etc... (other concurrency control constructs)

locks, semaphores, and other concurrency control constructs. By using such mechanisms, computations can coordinate their access to shared memory segments, allowing only one computation to read or write at a time while preventing simultaneous access.

Scenario:

When multiple computations attempt to write to the same memory segment concurrently, several issues can arise, such as:
- **Race condition**: The order in which the computations write to the memory segment may be non-deterministic. As a result, the final value stored in the memory may not be the desired or expected value.
- **Overwriting data**: If two computations attempt to write to the same memory location simultaneously, there is a possibility of overwriting each other's data. This can lead to data loss or corruption, as the values written by one computation may get overwritten by the other.

==> To ensure data integrity in such scenarios, synchronization mechanisms like locks, semaphores, or atomic operations can be used. These mechanisms enforce mutual exclusion, **allowing only one computation to access and write to the memory segment at a time**. By coordinating access, you can prevent simultaneous writes and maintain the integrity of the stored data.
