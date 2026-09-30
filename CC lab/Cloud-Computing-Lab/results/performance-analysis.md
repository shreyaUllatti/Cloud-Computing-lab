# Performance Analysis Results

## What We Tested

- Command used: `sysbench cpu --cpu-max-prime=20000 run`
- This command finds all prime numbers up to 20,000.
- It uses the CPU as much as possible.
- More events per second = faster CPU performance.

## Type-1 Hypervisor — Proxmox VE

| Parameter | Value |
|---|---|
| Hypervisor | Proxmox VE |
| Hypervisor Type | Type-1 |
| Guest OS | Ubuntu |
| CPU | 2 vCPU |
| Memory | 2 GB |
| Disk | 20 GB |
| Total Execution Time | 10.0005 s |
| Total Events | 17,494 |
| Events per Second | 1,749.16 |
| Average Latency | 0.57 ms |

## Type-2 Hypervisor — VMware Workstation

| Parameter | Value |
|---|---|
| Hypervisor | VMware Workstation |
| Hypervisor Type | Type-2 |
| Guest OS | Ubuntu |
| CPU | 2 vCPU |
| Memory | 2 GB |
| Disk | 20 GB |
| Total Execution Time | 10.0006 s |
| Total Events | 7,077 |
| Events per Second | 707.43 |
| Average Latency | 1.41 ms |

## Side-by-Side Comparison

| Parameter | Type-1 (Proxmox VE) | Type-2 (VMware Workstation) |
|---|---:|---:|
| Total Execution Time | 10.0005 s | 10.0006 s |
| Total Events | 17,494 | 7,077 |
| Events per Second | 1,749.16 | 707.43 |
| Average Latency | 0.57 ms | 1.41 ms |

## What Each Term Means

- Total Execution Time — The total time taken by the benchmark. Lower is better.
- Total Events — The number of calculations completed. Higher is better.
- Events per Second — The main CPU performance metric. Higher means faster performance.
- Average Latency — The average time taken to complete one calculation. Lower is better.

## Conclusion

- Proxmox VE (Type-1) is faster than VMware Workstation (Type-2).
- Proxmox VE achieved 1,749.16 events/sec.
- VMware Workstation achieved 707.43 events/sec.
- Proxmox VE is approximately 2.5 times faster.
- Proxmox VE also has lower latency: 0.57 ms compared to 1.41 ms.
- Proxmox VE is a Type-1 hypervisor that runs directly on the physical hardware.
- VMware Workstation is a Type-2 hypervisor that runs on top of a host operating system.
- The additional software layer in a Type-2 hypervisor can introduce extra overhead.
- Therefore, in this CPU benchmark, Proxmox VE provided significantly better CPU performance than VMware Workstation.
- Final conclusion: For CPU-intensive workloads, Type-1 hypervisors can provide better performance than Type-2 hypervisors.
