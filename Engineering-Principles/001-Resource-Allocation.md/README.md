# Engineering Principle #001 - Resource Allocation

## The Principle

Resources should be allocated based on the workload, not the maximum available capacity.

---

## What I Learned

A virtual machine does not create new hardware.

A hypervisor allocates physical hardware resources such as CPU, RAM, storage, and networking to each virtual machine.

---

## CPU Cores

Giving a virtual machine more CPU cores does not automatically make it faster.

Instead, ask:

> Does this workload actually need more CPU?

---

## Headroom

Leave unused resources available for:

- The host operating system
- Other virtual machines
- Unexpected spikes in workload

Enough resources + healthy headroom = smooth performance.

---

## Example

Host Computer

- 16 CPU cores

Virtual Machine

- 4 CPU cores assigned

Result:

The VM performs well while the host still has enough resources to remain responsive.

---

## Engineering Takeaway

Don't maximize resources.

Optimize them.
