# virtual-Machine-Setup-and-Remote-Connection-Learning-Program
# Enterprise Cloud Infrastructure: Secure Virtual Machine Provisioning & Remote Access Management

## Project Overview
In a modern DevOps or Cloud Engineer role, physical access to server infrastructure is non-existent. Secure remote connection protocols form the baseline of all server administration, application deployment, and cloud system maintenance. 

This project simulates an enterprise deployment scenario on **Microsoft Azure**. It serves as a comprehensive, end-to-end technical report demonstrating how to establish secure cross-platform remote sessions, verify target environment baseline integrity, implement firewall rules utilizing the Principle of Least Privilege, and manage active session lifecycles cleanly.

---

## Logical Architecture Diagram
The layout below maps out the secure ingress connection route established during this project, highlighting the firewall inspection layer:


[Local Workstation / Developer Client]
│
▼ (Public IP Restriction via ISP Gateway)
[Azure Network Security Group Firewall]
│
▼ (Inspected Traffic via Inbound Port 22)
[Ubuntu Linux VM: vmhrdeveastus201]


## Core Technical Tasks & Implementation Report

### Task 1: Infrastructure Firewall Configuration (Networking & Security)
* **Objective:** Define and implement Network Security Group (NSG) traffic control filters for cloud server exposure management.
* **Technical Execution:** Navigated to the Network Security Group resource mapped to the target virtual network interface. Provisions an inbound security filter rule tailored for **TCP Port 22** (Standard Secure Shell protocol) to permit administrative system entry boundaries.

### Task 2: Public Endpoint Discovery
* **Objective:** Audit and isolate the external network routing location details of the running resource.
* **Technical Execution:** Queried the Azure Resource Manager (ARM) Essentials blade on the core Virtual Machine console. Inspected, isolated, and documented the uniquely assigned public-facing IPv4 address entry: `20.62.122.34`.

### Task 3: Remote Desktop Protocol Deployment (Windows VM)
* **Objective:** Establish an authenticated graphical session to a Windows-based instance via Port 3389.
* **Deployment Status:** *Explicitly Flagged as Not Applicable (N/A) for this Architecture.*
* **Architectural Justification:** The infrastructure design parameters for this environment specifically required an open-source **Linux (Ubuntu Server)** system configuration. Therefore, graphical shell layers (RDP/Port 3389) were intentionally avoided to decrease the instance attack surface area and minimize resource overhead.

### Task 4: Secure Handshake & Linux Session Initiation
* **Objective:** Authenticate safely to a remote Linux CLI using asymmetric cryptographic key-pairs instead of volatile passwords.
* **Technical Execution:** Spawned a local shell container (Windows PowerShell) and initialized a secure OpenSSH network socket connection. Executed authentication verification targeting the administrative account using an encrypted identity key file (`.pem`) against the monitored public routing location:
  ```powershell
  ssh -i "C:\Users\MARTHA2025\Downloads\<private-key-file>.pem" azureuser@20.62.122.34


  Task 5: OS Environment Verification & Compliance Auditing
Objective: Conduct live terminal interactions to audit active host system health, folder structures, and software update indices.

Technical Execution: Upon receiving an authenticated secure prompt terminal string (azureuser@vmhrdeveastus201:~#), synchronization flags were pushed to the Advanced Package Tool (apt) package system. Executed system verification tasks to guarantee all dependencies matched enterprise stability baselines

sudo apt update && sudo apt upgrade -y


Task 6: Security Hardening & Perimeter Access Isolation
Objective: Restrict internet-facing entry vectors to block brute-force scripts and third-party unauthorized connection attempts.

Technical Execution: Upgraded the security policy from open testing states to production-grade posture. Inside the Azure Network Security Group console, altered the Source Access Profile configuration dropdown from a wide wildcard (* or Any) to My IP. This programmatically binds firewall ingress permission exclusively to the administrator's localized public network gateway location.

Task 7: Session Lifecycle Closure & Socket Termination
Objective: Implement proper session termination policies to protect server connection limits and secure dormant background processes.

Technical Execution: Closed down the interactive terminal shell safely using standard exit arguments to drop cleanly back into local workstation operations. (For comprehensive performance observations, see the Engineering Troubleshooting Log below).

Engineering Troubleshooting Log
Symptom Profiling:
During the final execution of Task 5 software validation updates, the active remote bash shell encountered an unexpected input/output socket lockup. The terminal screen stopped responding to active keyboard keystrokes, refusing to register or echo back the terminal cleanup command (exit).

Root Cause Analysis:
The host-side SSH daemon (sshd) experienced a socket runtime hang or a broken pipe state, causing the local terminal client to sit in an unacknowledged wait loop. This unresponsiveness prevented standard downstream terminal keyboard inputs from passing through the established tunnel.

Remediation Blueprint:
Force Connection Termination: Rather than leaving an unmonitored socket hanging on the terminal client, the host window parent process container was manually closed out (Alt + F4 / clicking window container termination limits), severing the local client attachment loop.

Environment Reset Verification: Spawned a fresh, isolated local Windows PowerShell terminal shell.

Boundary Confirmation: Inspected the working path root directory string to confirm the local machine context was successfully restored to default local prompts (PS C:\Users\MARTHA2025>), verifying no lingering cloud connections or active remote handles were leaked.

Artifact Directory & Verification Index
Visual evidence items validating task-by-task execution parameters are structured sequentially within the root /Screenshots folder path:

🖼️ Screenshots/Task 1 - Configure Networking and Security.png

Evidence Focus: Verifies the structural existence of the Inbound Security rules matrix controlling Port 22 connectivity within Azure.

🖼️ Screenshots/Task 2 - Public IP Address.png

Evidence Focus: Proves precise validation and location tracking of public cloud routing paths (20.62.122.34).

🖼️ Screenshots/Task 4 - Active SSH Connection.png

Evidence Focus: Validates a clean cryptographic authentication handshake onto the remote terminal environment prompt.

🖼️ Screenshots/Task 5 - System Verification CLI.png

Evidence Focus: Documents successful execution of the system package update sequences without any underlying dependency faults.

🖼️ Screenshots/Task 6 - Secure the Environment.png

Evidence Focus: Displays absolute alignment with cloud compliance policies by verifying Port 22 source targets are hardened to a single client network location.

🖼️ Screenshots/Task 7 - Terminated Session.png

Evidence Focus: Captures local computer shell prompt execution, proving total teardown of active remote cloud sessions.


---

### File 2: `SUMMARY.md`

```markdown
# Executive Summary: Enterprise Infrastructure Access Controls

This concise technical specification summary aggregates the Network Security Group (NSG) protection matrix configurations deployed during this project execution cycle.

##  Network Access Rule Architecture Matrix

| Priority | Security Rule Name | Port Destination | Transport Protocol | Bound Source Profile | Network Destination | Security Action | Applied Use-Case Lifecycle |
| :---: | :--- | :---: | :---: | :--- | :--- | :---: | :--- |
| **1000** | `Allow-SSH-Inbound` | `22` | TCP | **My IP** *(Restricted IP Profile)* | Virtual Network | **ALLOW** | Restricts admin terminal connections solely to the engineer's active workstation location. |
| *N/A* | *Allow-RDP-Inbound* | *3389* | *TCP* | *Explicitly Blocked* | *Virtual Network* | **DENY** | Graphical remote terminal paths disabled to align with Linux attack surface minimization practices. |

##  Enterprise Security Compliance Summary

1. **Adherence to Principle of Least Privilege (PoLP):** Initial cloud firewall testing states often use loose configuration profiles (`Source: Any / *`). This deployment represents a fully hardened system where perimeter entry fields are bounded directly to a verifiable network client destination, removing any risks associated with botnet scanning grids.
   
2. **Cryptographic Identity Management:** Administrative interaction bypasses legacy, unencrypted, or crackable entry systems. Connections rely purely on asymmetric public/private keys (`RSA / Ed25519` architecture hosted within a `.pem` data structure) to ensure all terminal command pipelines are encrypted during transit across the open internet.
