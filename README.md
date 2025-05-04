
## Overview

**Flock** is a kernel-level implementation of advisory file locking for the educational OS **mCertiKOS**. It introduces a new system call (`flock`) that allows concurrent processes to safely coordinate access to shared files using *shared* and *exclusive* locks. This project mimics the behavior of the Linux `flock` system call and demonstrates how process synchronization and file system integration can be achieved at the OS level.

Developed as a final project for CSE 4502: Operating Systems.

---

## 📚 Concepts and Features

This project applies several core OS principles:

- **Reader-Writer Synchronization**  
  Implements shared (read) and exclusive (write) locks to manage concurrent access to files.

- **Thread Coordination via Condition Variables**  
  Uses monitors and condition variables to block and wake threads attempting conflicting lock operations.

- **System Call Extension**  
  Adds a new syscall (`flock`) to the kernel, exposing locking functionality to user-space programs.

- **Inode-Level Lock Management**  
  Locks are maintained per inode, ensuring consistent access control across multiple file descriptors.

- **Non-Blocking Support**  
  The `LOCK_NB` flag allows non-blocking attempts to acquire locks—helpful in interactive or high-performance scenarios.

---

## 🔧 Usage

The `flock(int fd, int operation)` system call can be invoked from user programs with the following options:

- `LOCK_SH`: Acquire a shared lock  
- `LOCK_EX`: Acquire an exclusive lock  
- `LOCK_UN`: Release the current lock  
- Add `LOCK_NB` to request non-blocking behavior (e.g., `LOCK_EX | LOCK_NB`)  

Locks are automatically released when a file is closed.

---

## 🧪 Testing and Demonstrations

Test programs are located under `user/flocktest/` and demonstrate:

- Correct acquisition and release of locks  
- Lock contention and blocking behavior  
- Non-blocking failures  
- Automatic release on `close()`  
- Upgrade/downgrade attempts  

You can also run demo programs simulating readers and writers:

```bash
make
make qemu-nox
