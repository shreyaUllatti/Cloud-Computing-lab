# Cloud Computing Laboratory Report

## Performance observation of Type-1 and Type-2 hypervisors

**Experiment:** Ubuntu VM provisioning and CPU benchmarking  
**Platforms:** Proxmox VE (KVM) and VMware Workstation  
**Benchmark:** `sysbench cpu --cpu-max-prime=20000 run`

## 1. Objective

To configure an Ubuntu virtual machine on a Type-1 hypervisor and a Type-2 hypervisor, verify the guest system, monitor resources, and record CPU benchmark throughput and latency.

## 2. Background

A Type-1 hypervisor runs on the physical machine as the virtualization platform. Proxmox VE uses KVM with the Linux kernel to host virtual machines. A Type-2 hypervisor, such as VMware Workstation, runs as software on a host operating system. Both approaches can run guest operating systems; their management model, host environment, and resource scheduling differ.

## 3. Configuration 

| Setting | Proxmox VE | VMware Workstation |
|---|---|---|
| Guest OS | Ubuntu 24.04 desktop ISO / Ubuntu guest | Ubuntu guest |
| Virtual CPUs | 2 cores | 2 vCPU |
| Memory | 2,048 MB | 2 GB |
| Virtual disk | 20 GB | 20 GB |

## 4. Procedure

### Part A — Proxmox VE

1. Created a VM in Proxmox VE with 2 CPU cores, 2,048 MB memory, and a 20 GB disk.
2. Started the Ubuntu guest and opened its console.
3. Captured guest system configuration and resource monitoring screens.
4. Ran the Sysbench CPU workload with a prime limit of 20,000.

## Type-1 Hypervisor — Proxmox VE

| **Parameter**        | **Value**  |
| -------------------- | ---------- |
| Hypervisor           | Proxmox VE |
| Hypervisor Type      | Type-1     |
| Guest OS             | Ubuntu     |
| CPU                  | 2 vCPU     |
| Memory               | 2 GB       |
| Disk                 | 20 GB      |
| Total Execution Time | 10.0005 s  |
| Total Events         | 17,494     |
| Events per Second    | 1,749.16   |
| Average Latency      | 0.57 ms    |


### Part B — VMware Workstation

1. Created an Ubuntu VM using VMware Workstation.
2. Configured a 20 GB disk, 2 GB memory, and 2 virtual CPUs.
3. Started the guest and captured system checks for hostname, CPU, memory, disk, and process/resource state.
4. Installed Sysbench, checked its version, and ran the same CPU workload.

## Type-2 Hypervisor — VMware Workstation

| **Parameter**        | **Value**          |
| -------------------- | ------------------ |
| Hypervisor           | VMware Workstation |
| Hypervisor Type      | Type-2             |
| Guest OS             | Ubuntu             |
| CPU                  | 2 vCPU             |
| Memory               | 2 GB               |
| Disk                  | 20 GB              |
| Total Execution Time | 10.0006 s          |
| Total Events         | 7,077              |
| Events per Second    | 707.43             |
| Average Latency      | 1.41 ms            |

## Side-by-side comparison

| **Parameter**        | **Type-1 (Proxmox VE)** | **Type-2 (VMware Workstation)** |
| -------------------- | ----------------------- | ------------------------------- |
| Total Execution Time | 10.0005 s               | 10.0006 s                        |
| Total Events         | 17,494                  | 7,077                            |
| Events per Second    | 1,749.16                | 707.43                           |
| Average Latency      | 0.57 ms                 | 1.41 ms                          



<img width="2085" height="1497" alt="image" src="https://github.com/user-attachments/assets/204e920e-389b-4e3b-955b-f7132ba572cf" />

## What each term means?

Total execution time — how long the test ran. Lower is better.

Total Events — how many calculations were done. Higher is better.

Events per Second — main speed number. Higher = faster.

Average Latency — average time for one calculation. Lower is better.

Commands used in the Ubuntu guest:

```bash
hostnamectl
lscpu
free -h
df -h
top
sudo apt update
sudo apt install -y sysbench
sysbench --version
sysbench cpu --cpu-max-prime=20000 run
```

## 5. Results:

| Metric | Proxmox VE | VMware Workstation |
|---|---:|---:|
| Sysbench CPU speed | 1,749.16 events/sec | 975.67 events/sec |
| Total time | 10.005 s | 10.0006 s |
| Total events | 17,494 | 7,077 |
| Minimum latency | 0.57 ms | 0.53 ms |
| Average latency | 0.57 ms | 1.41 ms |
| Maximum latency | 2.43 ms | 3.66 ms |
 

Using the displayed throughput values, the difference between these runs is approximately:

```text
(1749.16 - 975.67) / 975.67 × 100 ≈ 79.3%
```


## 6. Conclusion

The experiment demonstrates VM creation and CPU benchmarking using Proxmox VE and VMware Workstation. In the measured runs, Proxmox VE achieved 1,749.16 events/sec, while VMware Workstation achieved 975.67 events/sec, indicating higher measured throughput for the Proxmox configuration. However, this result alone does not prove that Type-1 hypervisors are always faster than Type-2 hypervisors, because VM configuration and host-system conditions can also affect benchmark performance.

## 7. Screenshot index

- Proxmox setup and benchmark images: [`images/type1-proxmox/`](images/type1-proxmox/)
- VMware setup and benchmark images: [`images/type2-vmware/`](images/type2-vmware/)
