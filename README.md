# IIT Kanpur IDEAL Lab Server

## Server Guide

This document provides a quick overview of the IDEAL Lab server, its storage organization, and guidelines for using computational resources responsibly.

---
### 1. System Configuration
---

| Component | Configuration                                              |
| --------- | ---------------------------------------------------------- |
| CPU       | 32-core AMD EPYC 9334, 2.7 GHz, 128 MB L3 cache, 210 W TDP |
| Memory    | 64 GB DDR5-4800 ECC Registered DIMMs (2 × 32 GB)           |
| Storage   | 1.8 TB NVMe SSD + 4 TB HDD                                 |
| GPU       | NVIDIA RTX PRO 5000 Blackwell, 48 GB VRAM, 300 W TDP       |

---
### 2. Disk Utilization
---

The server has two primary storage locations:

- **NVMe SSD (`1.8 TB`):** User home directories are stored here. Use this storage for active projects and experiments that benefit from fast disk access.
- **HDD (`4 TB`):** Mounted at `/data`. Use this storage for shared projects, datasets, and older projects that do not require the performance of NVMe storage.

#### Directory organization

| Directory                | Purpose                            | Storage       |
| ------------------------ | ---------------------------------- | ------------- |
| `~`                      | Private active projects            | `1.8 TB NVMe` |
| `/data/shared/projects/` | Shared projects                    | `4 TB HDD`    |
| `/data/shared/datasets/` | Shared datasets                    | `4 TB HDD`    |
| `/data/users/username/`  | Private storage for older projects | `4 TB HDD`    |

#### Private and shared storage

- User home directories are private and intended primarily for active work.

- The `/data/shared/projects/` and `/data/shared/datasets/` directories are intended for resources that need to be accessed by members of the `researchers` group. Access and modification rights are governed by directory ownership, Unix permissions, and ACLs. Do not assume that every shared directory or file is writable by every group member.

- If you want other researchers to modify a project or dataset, explicitly configure the appropriate permissions or ACLs. Coordinate with the server administrator if you are unsure how to do this.

- No disk quotas are currently enforced. Users are therefore requested to move stale or completed projects from their NVMe home directories to their private storage under `/data/users/username/` to preserve NVMe capacity for active experiments. Private directories under `/data/shared/` can be created upon request.

---
### 3. Important Rules
---

1. **Check resource utilization.** Use `btop` to inspect CPU and memory utilization. Use `nvidia-smi` to inspect GPU utilization, VRAM usage, temperature, and power consumption.

2. **Use parallel processes responsibly.** Avoid launching an unnecessarily large number of concurrent processes. Multiple experiments may compete for CPU cores, memory bandwidth, cache capacity, RAM, and GPU resources.

3. **Monitor experiment performance.** High CPU utilization alone does not necessarily indicate efficient execution. Where appropriate, compare experiment throughput and monitor indicators such as instructions per cycle (IPC) and L3 cache misses to identify potential resource contention.

4. **Keep active experiments in your home directory.** Use `/data/shared/` for resources that need to be shared with other researchers and `/data/users/username/` for older private projects.

5. **Respect shared resources.** Before launching computationally intensive or long-running experiments, check the server's current workload and avoid unnecessarily interfering with other users' jobs.

6. **Preserve shared data.** Do not modify or delete another researcher's files without authorization. Keep shared datasets and canonical model files unchanged unless you have explicit permission to modify them.

---

For assistance with storage permissions, shared directories, or computational resource management, contact the server administrator.

---
### 4. Additional Resources
---

Detailed instructions for common tasks are available in `/data/shared/resources/`.

| Document             | Description                                                             |
| -------------------- | ----------------------------------------------------------------------- |
| `llms.md`            | Guidelines for storing pretrained and fine-tuned LLMs                   |
| `custom-commands.md` | Reference for useful custom commands available on the server            |
| `venv.md`            | Instructions for creating and managing Python virtual environments      |

Refer to these documents before setting up a new experiment or installing additional software.