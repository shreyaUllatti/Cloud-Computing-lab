# Cloud Computing Laboratory Report

## Performance observation of Type-1 and Type-2 hypervisors

**Experiment:** Ubuntu VM provisioning and CPU benchmarking  
**Platforms:** Proxmox VE (KVM) and VMware Workstation  
**Benchmark:** `sysbench cpu --cpu-max-prime=20000 run`

## 1. Objective

To configure an Ubuntu virtual machine on a Type-1 hypervisor and a Type-2 hypervisor, verify the guest system, monitor resources, and record CPU benchmark throughput and latency.

## 2. Background

A Type-1 hypervisor runs on the physical machine as the virtualization platform. Proxmox VE uses KVM with the Linux kernel to host virtual machines. A Type-2 hypervisor, such as VMware Workstation, runs as software on a host operating system. Both approaches can run guest operating systems; their management model, host environment, and resource scheduling differ.

## 3. Configuration documented in the screenshots

| Setting | Proxmox VE | VMware Workstation |
|---|---|---|
| Guest OS | Ubuntu 24.04 desktop ISO / Ubuntu guest | Ubuntu guest |
| Virtual CPUs | 2 cores | 2 vCPU |
| Memory | 2,048 MB | 2 GB |
| Virtual disk | 20 GB | 20 GB |
| Network | VirtIO bridge (`vmbr0`) shown | Not established from supplied images |

The supplied screenshots are the source for these configuration details. Any settings not visible in the screenshots are left unspecified.

## 4. Procedure

### Part A — Proxmox VE

1. Created a VM in Proxmox VE with 2 CPU cores, 2,048 MB memory, and a 20 GB disk.
2. Started the Ubuntu guest and opened its console.
3. Captured guest system configuration and resource monitoring screens.
4. Ran the Sysbench CPU workload with a prime limit of 20,000.

### Part B — VMware Workstation

1. Created an Ubuntu VM using VMware Workstation.
2. Configured a 20 GB disk, 2 GB memory, and 2 virtual CPUs.
3. Started the guest and captured system checks for hostname, CPU, memory, disk, and process/resource state.
4. Installed Sysbench, checked its version, and ran the same CPU workload.

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

## 5. Results transcribed from the supplied screenshots

| Metric | Proxmox VE | VMware Workstation |
|---|---:|---:|
| Sysbench CPU speed | 1,749.16 events/sec | 975.67 events/sec |
| Total time | 10.005 s | 10.0003 s |
| Total events | 17,494 | 9,760 |
| Minimum latency | 0.57 ms | 0.53 ms |
| Average latency | 0.57 ms | 1.02 ms |
| Maximum latency | 2.43 ms | 3.66 ms |
| 95th percentile latency | 0.58 ms | Not visible in supplied VMware summary |

Using the displayed throughput values, the difference between these runs is approximately:

```text
(1749.16 - 975.67) / 975.67 × 100 ≈ 79.3%
```

This calculation describes the measured runs only. The VMware summary screenshot does not show a 95th percentile value, so none is inferred.

## 6. Discussion

The Proxmox run recorded higher throughput and a lower average and maximum latency than the VMware run. The minimum latency was slightly lower in the VMware run. Individual benchmark outcomes can be affected by host CPU model, background processes, guest configuration, number of benchmark threads, power settings, and measurement variation. The screenshots document VM allocations, but they do not establish that every condition was identical during both runs. Therefore the observed gap should not be attributed solely to hypervisor type.

## 7. Conclusion

The lab demonstrates VM creation and guest verification on Proxmox VE and VMware Workstation, along with a Sysbench CPU benchmark on both. In the submitted measurements, Proxmox recorded 1,749.16 events/sec and VMware Workstation recorded 975.67 events/sec. Repeated runs under controlled host conditions would be needed to make a stronger performance comparison.

## 8. Screenshot index

- Proxmox setup and benchmark images: [`images/type1-proxmox/`](images/type1-proxmox/)
- VMware setup and benchmark images: [`images/type2-vmware/`](images/type2-vmware/)
