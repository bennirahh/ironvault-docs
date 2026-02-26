# ADR-001: Physical Infrastructure Selection

**Status:** Accepted  
**Date:** 2026-02-26  
**Decider:** IRONVAULT Architect

---

## 1. Context and Problem Statement
The **IRONVAULT** project requires a hosting environment for high-criticality services (Banking, Health, State Infrastructure). We need to decide between Public Cloud (AWS/GCP), a single powerful server (Monolith), or a multi-node physical cluster. 

The main constraints are **data sovereignty**, **high availability**, and **total control** over the hardware-to-software stack.

## 2. Decision Drivers
* **Sovereignty:** Data must remain under local jurisdiction and physical control.
* **Resilience:** The system must survive a hardware failure without service interruption.
* **Cost Efficiency:** Long-term CAPEX (buying hardware) vs. OPEX (monthly cloud subscriptions).
* **Security & Control:** Full mastery of the hardware-to-software stack to eliminate "black-box" dependencies and supply chain risks.

## 3. Considered Options
* **Option A: Public Cloud:** Scalable but fails sovereignty and long-term cost-predictability tests.
* **Option B: Single Server:** Cost-effective but represents a Single Point of Failure (SPOF).
* **Option C: 3-Node Physical Cluster:** High resilience through distributed quorum.

## 4. Decision Outcome
**Chosen Option: Option C (3-Node Physical Cluster)**

### Consequences
* **Positive:**
    * **Quorum:** With 3 nodes, the orchestrator (Kubernetes) maintains a majority even if one node fails.
    * **Trustless Design:** We own the encryption keys and the physical disks.
    * **Zero RTO:** High availability allows for "rolling updates" without downtime.
* **Negative:**
    * Requires manual networking setup (VLANs/Switch).
    * Initial hardware investment (CAPEX) required.

## 5. Validation
This choice will be validated during the "Chaos Engineering" phase, where we will simulate a total power failure on one node to prove the system's self-healing capabilities.