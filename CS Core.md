# Operating System 

## 1. Introduction to Operating Systems
### Core Concepts
- **Definition**: Software that manages hardware and provides services to applications
- **Purpose**: Acts as intermediary between users and hardware
- **Key Functions**:
  - Process management
  - Memory management
  - File system management
  - Device management
  - Security/Protection

### OS Types
- **Batch OS**: Executes jobs in batches without user interaction
- **Time-Sharing**: Multiple users share system resources simultaneously
- **Distributed**: Manages group of networked computers as single system
- **Real-Time**: Guarantees response within strict time limits
- **Embedded**: Designed for specific devices (ATMs, medical devices)

### Execution Modes
- **Kernel Mode**: Privileged mode with full hardware access
- **User Mode**: Restricted mode for applications

## 2. Process Management
### Fundamental Concepts
- **Process**: Program in execution (instance of running program)
- **Thread**: Lightweight process (shares memory with parent process)

### Process Lifecycle
1. New → 2. Ready → 3. Running → 4. Waiting → 5. Terminated

### Process Control
- **PCB (Process Control Block)**: Data structure storing process info
- **Context Switching**: Saving/restoring process state during switches

### Scheduling Algorithms
| Algorithm | Description | Pros | Cons |
|-----------|-------------|------|------|
| FCFS | First come, first served | Simple | Convoy effect |
| SJF | Shortest job first | Optimal | Hard to predict |
| Priority | Highest priority first | Important jobs first | Starvation |
| Round Robin | Time slices for each | Fair | High overhead |
| Multilevel | Multiple queues | Flexible | Complex |

### Threading Models
- **Many-to-One**: Many user threads to one kernel thread
- **One-to-One**: Each user thread gets kernel thread
- **Many-to-Many**: Flexible mapping

## 3. Synchronization & Deadlocks
### Synchronization Basics
- **Critical Section**: Code segment accessing shared resources
- **Race Condition**: Unexpected results from concurrent access

### Synchronization Tools
- **Mutex**: Lock/unlock mechanism
- **Semaphore**: Integer variable with wait/signal operations
- **Monitor**: High-level synchronization construct
- **Peterson's Solution**: Software solution for 2 processes

### Deadlock Analysis
- **4 Necessary Conditions**:
  1. Mutual Exclusion
  2. Hold and Wait
  3. No Preemption
  4. Circular Wait

### Deadlock Handling
- **Prevention**: Break one condition
- **Avoidance**: Banker's algorithm
- **Detection & Recovery**: Find and resolve deadlocks

## 4. Memory Management
### Address Spaces
- **Logical**: Virtual address seen by program
- **Physical**: Actual RAM address

### Allocation Techniques
- **Contiguous**: Allocate continuous blocks
  - Fixed Partitioning: Equal-size partitions
  - Dynamic Partitioning: Variable-size partitions
- **Fragmentation**:
  - Internal: Wasted space within partition
  - External: Wasted space between partitions

### Paging
- Divides memory into fixed-size pages
- **Page Table**: Maps virtual to physical addresses
- **TLB**: Cache for page table entries
- **Hierarchical Paging**: Multi-level page tables

### Virtual Memory
- **Demand Paging**: Load pages only when needed
- **Page Replacement**:
  - FIFO: First-in-first-out
  - LRU: Least recently used
  - Optimal: Replace page not needed longest
  - Clock: Circular list approximation of LRU
- **Thrashing**: Excessive page faults degrading performance

## 5. File Systems
### File Organization
- **Contiguous Allocation**: Files stored in consecutive blocks
- **Linked Allocation**: Files as linked lists of blocks
- **Indexed Allocation**: Index block points to file blocks

### Directory Structures
- **Single-Level**: All files in one directory
- **Tree-Structured**: Hierarchical organization
- **Acyclic Graph**: Allows sharing via links

### Disk Scheduling
| Algorithm | Description |
|-----------|-------------|
| FCFS | First come, first served |
| SSTF | Serve nearest request first |
| SCAN | Moves back and forth |
| C-SCAN | Circular scan |
| LOOK | Version of SCAN that reverses at last request |

## 6. I/O Systems
### Key Components
- **Device Controllers**: Hardware interfaces
- **Device Drivers**: Software to control devices

### Data Transfer Methods
- **Polling**: CPU checks device status
- **Interrupts**: Device signals CPU when ready
- **DMA**: Direct memory access without CPU

### Buffering Techniques
- **Single Buffer**: One buffer for I/O
- **Double Buffer**: Two buffers (one filling while other empties)
- **Circular Buffer**: Ring buffer implementation

## 7. Advanced Topics
### System Architecture
- **System Calls**: Interface between OS and programs
- **IPC Mechanisms**:
  - Shared Memory
  - Message Passing (Pipes, Sockets, RPC)

### Modern Concepts
- **Virtualization**: Multiple OS instances on single hardware
- **Distributed Systems**: Multiple computers as single system
- **RTOS**: Systems with strict timing constraints

### Security
- **Authentication**: Verifying identity
- **Authorization**: Access permissions
- **ACLs**: Lists defining access rights
- **Cryptography**: Data encryption/decryption

## 8. Linux/UNIX Specifics
### Key Commands
- **Process Control**:
  - `fork()`: Create new process
  - `exec()`: Replace current process
- **File Management**:
  - `chmod`: Change permissions
  - `chown`: Change ownership

### Shell Features
- **Scripting**: Automating tasks
- **Pipes**: Connecting command output to input

## 9. Performance Metrics
### Key Measures
- **CPU Utilization**: Percentage of CPU usage
- **Throughput**: Jobs completed per time unit
- **Turnaround Time**: Total execution time
- **Response Time**: Time to first response
- **Latency**: Delay in response

### Optimization
- **Caching**: Storing frequently used data
- **Prefetching**: Loading data before needed

## 10. Common Interview Questions
### Conceptual
1. **Process vs Thread**: 
   - Process = Independent execution unit
   - Thread = Lightweight process sharing memory
2. **Virtual Memory**: 
   - Extension of RAM using disk space
3. **Deadlock Prevention**: 
   - Break one of four conditions

### Practical
1. **Page Replacement**:
   - Choose algorithm based on workload
2. **Synchronization**:
   - Implement producer-consumer using semaphores
3. **Banker's Algorithm**:
   - Resource allocation safety check

## Interview Tips
1. **Focus Areas**:
   - Process synchronization
   - Memory management
   - Deadlock scenarios
2. **Preparation**:
   - Practice synchronization pseudocode
   - Understand real-world OS implementations
   - Solve numerical problems (scheduling, paging)
3. **Problem Solving**:
   - Approach systematically
   - Consider edge cases
   - Explain thought process clearly
   
   
 
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
