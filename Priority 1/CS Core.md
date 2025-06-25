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
   
   
   
   
# DATABASE MANAGEMENT SYSTEM

```

1. INTRODUCTION TO DBMS
-------------------------------------------------
1.1 Core Concepts
- DBMS: Software system for creating, managing and manipulating databases
- Key Features:
  * Data organization
  * Efficient retrieval
  * Multi-user access control
  * Data integrity and security

1.2 Database Models
- Relational (Tables with rows/columns) - MySQL, Oracle
- NoSQL (Flexible schemas) - MongoDB, Cassandra
- Hierarchical (Tree structure) - IBM IMS
- Network (Graph structure) - IDMS
- Object-oriented (Objects with attributes) - ObjectDB

2. RELATIONAL DATABASE CONCEPTS
-------------------------------------------------
2.1 Fundamentals
- Relation = Table
- Tuple = Row
- Attribute = Column
- Domain = Set of allowed values

2.2 Keys
- Primary Key: Unique identifier (StudentID)
- Foreign Key: Reference to another table (DeptID in Students table)
- Candidate Key: Potential primary keys
- Super Key: Combination that identifies records
- Alternate Key: Candidate keys not chosen as primary

3. DATABASE DESIGN
-------------------------------------------------
3.1 Normalization
1NF: Atomic values, no repeating groups
2NF: No partial dependencies (all non-key attributes depend on full primary key)
3NF: No transitive dependencies (non-key attributes don't depend on other non-keys)
BCNF: Stronger 3NF (every determinant is candidate key)
4NF: No multi-valued dependencies

3.2 ER Modeling
Entities: Rectangle (Student, Course)
Relationships: Diamond (Enrolls)
Attributes: Oval (StudentID, CourseName)
Cardinality: 1:1, 1:N, M:N

4. TRANSACTION MANAGEMENT
-------------------------------------------------
4.1 ACID Properties
- Atomicity: All or nothing
- Consistency: Valid state transitions
- Isolation: Concurrent transactions don't interfere
- Durability: Committed changes persist

4.2 Concurrency Problems
- Dirty Read: Reading uncommitted data
- Lost Update: Overwriting changes
- Non-repeatable Read: Different values in same transaction
- Phantom Read: New rows appearing

5. INDEXING AND PERFORMANCE
-------------------------------------------------
5.1 Index Types
- B-Tree: Balanced tree structure (default in most DBMS)
- Hash: Direct key-value mapping
- Bitmap: For low-cardinality columns
- Clustered: Data physically ordered by index
- Non-clustered: Separate index structure

5.2 Query Optimization
- Execution plans
- Join strategies
- Cost-based optimization

6. SQL COMMANDS
-------------------------------------------------
6.1 DDL (Data Definition)
CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE

6.2 DML (Data Manipulation)
SELECT, INSERT, UPDATE, DELETE

6.3 DCL (Data Control)
GRANT, REVOKE

6.4 TCL (Transaction Control)
COMMIT, ROLLBACK, SAVEPOINT

7. ADVANCED TOPICS
-------------------------------------------------
7.1 Distributed Databases
- CAP Theorem (Consistency, Availability, Partition Tolerance)
- Sharding
- Replication

7.2 NoSQL Databases
- Document stores (MongoDB)
- Key-value stores (Redis)
- Column-family stores (Cassandra)
- Graph databases (Neo4j)

7.3 Big Data Technologies
- Hadoop ecosystem
- Spark processing
- Data lakes

8. PRACTICAL DB ADMINISTRATION
-------------------------------------------------
8.1 Backup Strategies
- Full backup
- Incremental backup
- Differential backup

8.2 Security
- Authentication
- Authorization (RBAC)
- Encryption
- Auditing

9. INTERVIEW PREPARATION
-------------------------------------------------
9.1 Common Questions
- Explain normalization
- ACID vs BASE
- SQL vs NoSQL
- Indexing strategies

9.2 Design Problems
- Design database for:
  * E-commerce site
  * Library system
  * Social network

10. RESOURCES
-------------------------------------------------
- Books: "Database System Concepts" by Silberschatz
- Online: SQLZoo, LeetCode Database problems
- Tools: MySQL Workbench, pgAdmin, MongoDB Compass


```

# Computer Networks

```
COMPUTER NETWORKS FUNDAMENTALS

1. NETWORK BASICS
-------------------------------------------------
1.1 What is a Network?
- Interconnected devices that can communicate
- Purpose: Share resources and information

1.2 Network Types by Scale:
- PAN (Personal Area Network): <10m (Bluetooth)
- LAN (Local Area Network): Building/campus
- MAN (Metropolitan Area Network): City-wide
- WAN (Wide Area Network): Country/global

1.3 Network Topologies:
- Star (Central hub)
- Bus (Single backbone cable)
- Ring (Circular connection)
- Mesh (Every device connected)
- Hybrid (Combination)

2. NETWORK MODELS
-------------------------------------------------
2.1 OSI Model (7 Layers):
7. Application  - HTTP, FTP, SMTP
6. Presentation - Encryption, compression
5. Session      - Connections, sessions
4. Transport    - TCP, UDP
3. Network      - IP, routing
2. Data Link    - MAC, switches
1. Physical     - Cables, signals

2.2 TCP/IP Model (4 Layers):
4. Application (Combines OSI 5-7)
3. Transport
2. Internet (Network in OSI)
1. Network Access (Data Link + Physical)

3. PROTOCOLS
-------------------------------------------------
3.1 Key Protocols:
- HTTP/HTTPS: Web browsing
- FTP: File transfer
- SMTP/POP/IMAP: Email
- DNS: Domain to IP resolution
- DHCP: Automatic IP assignment

3.2 Transport Protocols:
- TCP: Connection-oriented, reliable
- UDP: Connectionless, faster

4. IP ADDRESSING
-------------------------------------------------
4.1 IPv4 vs IPv6:
- IPv4: 32-bit (4.3B addresses)
- IPv6: 128-bit (340 undecillion addresses)

4.2 Address Classes:
- Class A: 1.0.0.1 - 126.255.255.254
- Class B: 128.1.0.1 - 191.255.255.254
- Class C: 192.0.1.1 - 223.255.254.254

4.3 Special Addresses:
- 127.0.0.1: Localhost
- 192.168.x.x: Private network
- 255.255.255.255: Broadcast

5. NETWORK DEVICES
-------------------------------------------------
5.1 Hardware Components:
- Hub: Basic connector (dumb)
- Switch: Intelligent traffic director
- Router: Connects networks
- Modem: Converts digital<->analog
- Gateway: Protocol translator

6. NETWORK SECURITY
-------------------------------------------------
6.1 Common Threats:
- DDoS attacks
- Man-in-the-middle
- Phishing
- Malware

6.2 Protection Methods:
- Firewalls
- VPNs
- Encryption (SSL/TLS)
- IDS/IPS (Intrusion Detection/Prevention)

7. WIRELESS NETWORKING
-------------------------------------------------
7.1 Wi-Fi Standards:
- 802.11a: 5GHz, 54Mbps
- 802.11b: 2.4GHz, 11Mbps
- 802.11g: 2.4GHz, 54Mbps
- 802.11n: MIMO, 600Mbps
- 802.11ac: 5GHz, 1Gbps+

7.2 Cellular Generations:
- 3G: Mobile internet
- 4G LTE: Fast mobile broadband
- 5G: Ultra-low latency

8. INTERNET TECHNOLOGIES
-------------------------------------------------
8.1 How Internet Works:
- ISPs connect to backbone
- Packet switching
- DNS resolution
- Routing protocols (BGP)

8.2 Cloud Networking:
- SaaS, PaaS, IaaS
- CDNs (Content Delivery Networks)
- Virtual Private Clouds

9. NETWORK TROUBLESHOOTING
-------------------------------------------------
9.1 Common Tools:
- ping: Tests connectivity
- traceroute: Shows path
- ipconfig/ifconfig: Shows config
- netstat: Shows connections
- nslookup: DNS queries

10. INTERVIEW PREPARATION
-------------------------------------------------
10.1 Common Questions:
- Explain three-way handshake
- Difference between TCP/UDP
- How DNS works
- Explain subnetting
- What happens when you visit a website?

10.2 Practical Skills:
- Configuring routers
- Analyzing packets (Wireshark)
- Troubleshooting connectivity
- Setting up basic networks

REFERENCES:
- Books: "Computer Networking: A Top-Down Approach"
- Tools: Wireshark, Cisco Packet Tracer
- Certifications: CCNA, Network+

```
   
 
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
