# Process-Watchdog-Auditor

## Overview
This repository contains a Linux Kernel Module (LKM) written in 100% pure x86_64 Assembly (NASM) for Arch Linux. It handles system-space protection by intercepting system calls directly at the kernel boundary to check process security and verify data integrity.

---

## Code Flow
```mermaid
graph TD
    classDef default fill:#111827,stroke:#374151,stroke-width:2px,color:#9ca3af;
    classDef target fill:#1f2937,stroke:#4b5563,stroke-width:2px,color:#d1d5db;
    classDef logic fill:#1f2937,stroke:#d97706,stroke-width:2px,color:#d1d5db,font-weight:bold;
    classDef action fill:#1f2937,stroke:#ef4444,stroke-width:2px,color:#d1d5db,font-weight:bold;
    classDef secure fill:#1f2937,stroke:#10b981,stroke-width:2px,color:#d1d5db,font-weight:bold;

    A[User-Space Syscall] --> B(Kernel Boundary)
    B --> C{Assembly LKM Check}
    C -->|Unauthorized| D[Block Process]
    C -->|Authorized| E[Allow Execution]

    class A,B target;
    class C logic;
    class D action;
    class E secure;
```

---

## Build and Run
Make sure you have `nasm`, `make`, and `linux-headers` installed on your Arch Linux environment.

```bash
# Compile and build the kernel module automatically
make

# Insert the compiled module into the Linux kernel
sudo insmod watchdog_auditor.ko

# Remove the module from the kernel
sudo rmmod watchdog_auditor
```

---

## Project Structure (Makefile Code)
This is the Makefile used to track and build the assembly kernel module natively:

```makefile
ASM=nasm
ASMFLAGS=-f elf64
LD=ld

all: watchdog_auditor

watchdog_auditor: main.o
	\$(LD) main.o -o watchdog_auditor

main.o: main.asm
	\$(ASM) \$(ASMFLAGS) main.asm -o main.o

clean:
	rm -f *.o watchdog_auditor
```
