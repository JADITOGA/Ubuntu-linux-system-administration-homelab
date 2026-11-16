![Linux System Administration Home Lab](assets/project-banner.svg)

# Linux System Administration Home Lab

**Ubuntu Server · Oracle VirtualBox · Linux Permissions · SSH · SCP · Networking**

> **Project status:** Completed  |  **Type:** Independent educational home lab  |  **Scenario:** Fictional company, Musterfirma GmbH

## Why I built this

I am preparing for a **Fachinformatiker für Systemintegration (FISI) Ausbildung in Germany**. This project was my first opportunity to go beyond memorizing Linux commands and practice the responsibilities of an IT administrator: controlling employee access, troubleshooting connectivity, working remotely, and validating changes before considering them complete.

I wanted each technical task to answer three questions: **What problem does it solve? How do I know the configuration works? How would a company use this?**

## Lab architecture

![Network architecture showing Windows 11 connecting via localhost TCP port 2222 through VirtualBox NAT to Ubuntu SSH port 22](assets/network-architecture.svg)

| Component | Configuration |
|---|---|
| Host | Windows 11 |
| Virtualization | Oracle VirtualBox |
| Guest | Ubuntu Server |
| Network | NAT |
| Guest IP during testing | `10.0.2.15` |
| SSH forwarding | `127.0.0.1:2222` → `10.0.2.15:22` |

**Design decision:** Binding the host port to `127.0.0.1` allowed testing from the Windows host without exposing the forwarded SSH port directly to other devices on the home network.

## Challenge 1: Give the right employees access, and nobody else

### Business problem

Musterfirma GmbH needs a shared directory for its IT team. Employees outside that team must not access it. Individual per-user permissions would be harder to maintain as staff change.

### My implementation

- Created accounts for **Max, Anna, David, and Sophie**.
- Created the `it-team` group and added Max, Anna, and David.
- Configured `/srv/it-share` with owner `root`, group `it-team`, and mode `2770`.
- Used the setgid directory bit so new files and directories inherit the team group, where applicable.

![Access control matrix for four fictional employees](assets/access-control.svg)

### How I verified it

I tested the share under different user identities. **Anna successfully appended** to a shared file after I enabled group write permissions on that file. **Sophie was denied access** because she was not in `it-team`.

### Issue I had to troubleshoot

Anna initially could access the directory but could not modify the shared file. I learned that **directory permissions and file permissions are separate**. Instead of granting everyone broad access, I targeted the file's missing group write permission:

```bash
sudo chmod g+w /srv/it-share/test.txt
```

I repeated the test and confirmed the edit succeeded.

**Real-world relevance:** Employees often report being able to browse a shared folder but not save changes. A system administrator needs to diagnose the precise permission boundary and fix it without weakening access controls.

## Challenge 2: Administer a server remotely with SSH

### Business problem

Servers are not always physically accessible. Administrators need a secure way to connect and diagnose problems remotely.

### My implementation

I enabled SSH on Ubuntu and connected from Windows PowerShell using a VirtualBox NAT port-forwarding rule.

```powershell
ssh -p 2222 <ubuntu-user>@127.0.0.1
```

### Troubleshooting experience

The initial connection was refused. I did not assume the SSH service was broken. I checked whether the service was running, tested the forwarded port using Windows tools, inspected the VirtualBox NAT rule, corrected its settings, then connected successfully. I also corrected an incorrect login username during testing.

**What I learned:** A connection failure can occur at several layers: service availability, addressing, port forwarding, or authentication. Testing each layer makes the investigation more efficient.

**Real-world relevance:** The same reasoning applies when an administrator cannot reach a remote server, whether it is a VM, an internal server, or a system in a data center.

## Challenge 3: Transfer files securely with SCP

### Business problem

Administrators need to exchange reports, configuration files, and other operational data between systems without relying on manual copy-and-paste through a VM console.

### My implementation

I transferred a test file from Windows to Ubuntu and a report back to Windows.

```powershell
# Windows -> Ubuntu
scp -P 2222 "$HOME\Desktop	ransfer-test.txt" <ubuntu-user>@127.0.0.1:~/

# Ubuntu -> Windows
scp -P 2222 <ubuntu-user>@127.0.0.1:~/server-report.txt "$HOME\Desktop"
```

### Troubleshooting experience

My first SCP attempt produced an **access denied** error. I traced it to a missing `:` before the remote destination path. Once I corrected the syntax, the transfer succeeded. I verified the files at their destinations.

**What I learned:** Error messages are useful evidence; a small syntax error can make a command operate on the wrong path. Also, SCP uses uppercase `-P` for its port option, while SSH uses lowercase `-p`.

**Real-world relevance:** Secure file transfers are used for routine server administration, including retrieving reports and distributing files to managed systems.

## My troubleshooting method

![Six-step troubleshooting workflow](assets/troubleshooting-workflow.svg)

| Problem observed | Evidence / analysis | Targeted correction | Verification |
|---|---|---|---|
| Team member could not edit shared file | Directory access worked; file group write was missing | `chmod g+w` on the file | Anna could append successfully |
| SSH connection refused | Service and forwarding path checked | Corrected VirtualBox NAT forwarding | Connected from PowerShell |
| SSH login unsuccessful | Username did not match the created account | Used the correct username | Authenticated and ran remote commands |
| SCP transfer failed | Destination lacked remote-path `:` separator | Corrected SCP destination syntax | File arrived and was readable |
| Non-team employee attempted share access | User not in `it-team` | No change needed; denial was intended | Sophie denied access |

My process: **observe → inspect → hypothesize → change → verify → document**. I am learning to make changes that are narrow, reversible, and supported by evidence.

## Results and skills demonstrated

| Technical work | What it demonstrates to an employer |
|---|---|
| User and group management | Managing employee access consistently |
| Linux permissions and setgid | Applying least privilege and supporting team collaboration |
| Testing permitted and denied access | Verifying security controls rather than assuming they work |
| SSH over NAT | Understanding TCP ports and remote administration |
| SCP transfers in both directions | Moving operational files securely |
| Troubleshooting and documenting failures | Investigating causes instead of guessing |

### Completion evidence

- [x] Installed and operated Ubuntu Server in VirtualBox
- [x] Created simulated employee accounts and `it-team`
- [x] Configured `/srv/it-share` with group ownership and mode `2770`
- [x] Verified Anna's file edit and Sophie's access denial
- [x] Connected from Windows to Ubuntu using SSH
- [x] Transferred files with SCP in both directions

## Screenshots from my actual lab

I plan to add original, redacted evidence here. **These are intentionally placeholders, not fabricated terminal screenshots.**

| Evidence to capture | Suggested filename |
|---|---|
| Employee group membership (`id`, `groups`) | `screenshots/01-users-groups.png` |
| Share permission details (`ls -ld /srv/it-share`) | `screenshots/02-share-permissions.png` |
| Successful authorized access and denied unauthorized access | `screenshots/03-access-tests.png` |
| VirtualBox NAT SSH port-forwarding rule | `screenshots/04-nat-forwarding.png` |
| Successful SSH session from Windows | `screenshots/05-ssh-session.png` |
| SCP transfer and destination verification | `screenshots/06-scp-transfer.png` |

**Privacy note:** Before publishing, I will remove passwords, private keys, tokens, or any private information I do not want public. The network diagram uses lab-only/local addresses.

## Reflection: What changed in how I approach IT

Initially, I treated Linux commands as separate instructions to memorize. During this lab, I started connecting commands to **administrative objectives**: granting a team access, confirming that other users are blocked, establishing a working remote connection, and verifying transferred files.

The failed attempts were especially valuable. They taught me to look for the exact point of failure, read the evidence, and test a focused fix. I am still a beginner, but I now have a repeatable way to work through technical problems.

## Next project

**Project 2: Nginx Web Server** — deploying a website on Ubuntu Server, configuring HTTP access through VirtualBox NAT, separating HTML and CSS, and learning log-based troubleshooting.

---

*Independent educational home lab using a fictional business and fictional employee names. No production company systems were involved.*
