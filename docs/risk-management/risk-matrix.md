# ⚖️ Risk & Impact Matrix (MRI)

This document identifies potential threats to the **IRONVAULT** infrastructure and defines the mitigation strategies implemented in the architecture.

## 📊 Threat Assessment

| Threat ID | Threat Category | Probability | Impact | Mitigation Strategy |
| :--- | :--- | :--- | :--- | :--- |
| **R-01** | **Physical Node Failure** | High | Medium | 3-node cluster with automated failover (K3s). |
| **R-02** | **Data Loss (Disk)** | Medium | High | ZFS Mirroring/RAID + Offsite encrypted backups. |
| **R-03** | **Unauthorized Remote Access** | Medium | Critical | SSH Key-only auth + Zero-trust WireGuard mesh. |
| **R-04** | **Physical Theft of Node** | Low | Critical | Full Disk Encryption (LUKS) with remote unlock. |
| **R-05** | **Power Outage** | Medium | Medium | UPS (Uninterruptible Power Supply) + Graceful shutdown. |
| **R-06** | **Supply Chain Attack** | Low | High | NixOS Hermetic builds & Flake lockfile pinning. |

## 🛡️ Mitigation Details

### R-01 & R-02: Resilience
The choice of **3 physical nodes** (ADR-001) ensures that the quorum is maintained even if one node goes offline. Data integrity is managed at the filesystem level via ZFS.

### R-03 & R-04: Security Hardening
By disabling password authentication and enforcing **LUKS encryption**, we ensure that even if a physical server is stolen, the data remains unreadable without the cryptographic keys.

### R-06: Traceability
Using **NixOS Flakes** allows us to know exactly which version of which software is running at any given time, reducing the "Black Box" risk common in traditional distributions.