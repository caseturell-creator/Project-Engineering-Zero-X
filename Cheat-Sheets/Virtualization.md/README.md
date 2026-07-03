# Virtualization

## What is Virtualization?

Virtualization is the process of creating virtual versions of computers, allowing multiple operating systems or environments to run on a single physical machine.

---

## Hypervisor

A hypervisor is software that creates and manages virtual machines (VMs).

Examples:
- Oracle VirtualBox
- VMware
- Hyper-V

A hypervisor allows multiple operating systems to share the same physical hardware.

---

## Virtual Machine (VM)

A virtual machine is a software-based computer that behaves like a physical computer.

A VM has:
- Virtual CPU
- Virtual RAM
- Virtual Storage
- Virtual Network Adapter

---

## CPU Allocation

When assigning CPU cores to a VM:

- 1 Core = Very light workloads
- 2 Cores = Basic Linux or lightweight systems
- 4 Cores = Good balance for many Windows labs
- More Cores = Only if the workload requires them

More cores do **not** automatically mean better performance.

---

## Headroom

Headroom is the unused system capacity left available for future workloads or sudden spikes in resource usage.

Enough resources + healthy headroom = smooth performance.

---

## Resource Allocation

A hypervisor does **not** create CPU cores.

It allocates the physical CPU's resources to virtual machines.

The VM thinks it has dedicated hardware, but the hypervisor shares the physical hardware between the host and all VMs.

---

## Hypervisors vs Containers

Hypervisors:
- Run multiple operating systems.
- Each VM has its own operating system.

Containers:
- Run multiple applications.
- Share the host operating system's kernel.
- More lightweight than virtual machines.

---

## Engineering Notes

- Don't memorize settings.
- Understand why they were chosen.
- Match resources to the workload.
- Leave headroom whenever possible.
