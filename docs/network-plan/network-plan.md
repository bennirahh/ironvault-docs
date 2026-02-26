# 🌐 Network Addressing Plan (Abstract)

> **Security Policy:** To prevent internal reconnaissance, specific IP ranges and subnets are abstracted in public documentation. Implementation details are stored in encrypted NixOS secrets.

## 🏗️ Layer 2: Segmentation (VLANs)

| VLAN ID | Name | Traffic Type | Isolation Level |
| :--- | :--- | :--- | :--- |
| `VLAN_MGMT` | **Management** | SSH, NixOS Rebuild, Monitoring | Critical (Isolated) |
| `VLAN_SRV` | **Services** | K3s, Public APIs, Web Traffic | Restricted |
| `VLAN_DATA` | **Data** | Database Replication, Storage (ZFS/Ceph) | High (No External Route) |

## 📍 Layer 3: Addressing Logic

The cluster follows a deterministic IP assignment logic:
* **Node-01:** `SUBNET_PREFIX.X.11`
* **Node-02:** `SUBNET_PREFIX.X.12`
* **Node-03:** `SUBNET_PREFIX.X.13`

*Where `X` represents the Functional VLAN ID.*

---
![License](https://img.shields.io/badge/license-MIT-blue)
![Author](https://img.shields.io/badge/author-Bennirahh-white?style=flat&logo=github)
