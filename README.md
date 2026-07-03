# Boutaba-Kernel-Hardening
A lightweight Linux Kernel Module (LKM) written in pure C for advanced kernel space subsystem protection and modular safe-vault telemetry.
#  Boutaba Linux Kernel Hardening Module (v1.0)

A lightweight Linux Kernel Module (LKM) written in pure C, optimized for modern **Arch Linux** kernel headers. It explores the foundational hooks of kernel space programming to establish an isolated safe-vault subsystem framework.

##  Architectural Features

* **Low-Level Subsystem Hooking:** Operates directly inside Ring 0 (Kernel Space), bypassing standard User Space limitations to interface with CPU memory vectors.
* **Synchronized Lifecycle Management:** Implements precise macros (`__init` and `__exit`) linked to core kernel runtime modules for smooth injection (`insmod`) and removal (`rmmod`).
* **Kernel Telemetry Logging:** Uses atomic subsystem log triggers (`printk`) aligned with high-priority macros (`KERN_INFO`) for forensic tracing.

## 🛠️ Compilation & Testing

To compile this module, you need the official kernel headers for your Arch distribution.

Create a `Makefile`:
```make
obj-m += main.o
all:
	make -C /lib/modules/(shell uname -r)/build M=(PWD) modules
clean:
	make -C /lib/modules/(shell uname -r)/build M=(PWD) clean
```

Compile the module:
```bash
make
```

Load it into the Kernel:
```bash
sudo insmod main.ko
```

Check logs:
```bash
sudo dmesg | tail -n 10
```

