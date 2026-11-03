# Kylin Linux Security Agent

![Header](https://capsule-render.vercel.app/api?type=waving&color=0:1A2980,100:26D0CE&height=220&section=header&text=Kylin%20Linux%20Security%20Agent&fontSize=55&fontColor=ffffff&animation=twinkling&fontAlignY=35&desc=Enterprise%20Grade%20Protection%20For%20Your%20Linux%20Infrastructure&descAlignY=55&descSize=20)

<div align="center">

![Version](https://img.shields.io/badge/version-3.2.0-26D0CE?style=for-the-badge&logo=git&logoColor=black)
![Downloads](https://img.shields.io/badge/downloads-91.2K-1A2980?style=for-the-badge&logo=download&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-FFB300?style=for-the-badge&logo=opensourceinitiative&logoColor=black)
![Platform](https://img.shields.io/badge/platform-kylin%20%7C%20ubuntu%20%7C%20centos-00E676?style=for-the-badge&logo=linux&logoColor=white)

</div>

---

## 🛡️ A Modern Approach to Linux Hardening

Linux is inherently secure, but "default" is not "hardened". In enterprise environments, servers are constantly under attack from brute-force attempts, zero-day exploits, and insider threats. While tools like SELinux and AppArmor exist, they are often complex to configure and manage at scale.

**Kylin Linux Security Agent** is a lightweight, open-source security daemon designed specifically for Kylin OS, Ubuntu, and CentOS. It acts as an autonomous security guard for your servers. Instead of just logging events, it actively responds to threats in real-time. It monitors system calls, network traffic, and file integrity, automatically blocking malicious IPs and quarantining compromised processes.

This repository is built for DevOps engineers and system administrators who need a "set and forget" security solution. It provides a beautiful web dashboard to visualize alerts and a highly efficient C-based backend that consumes less than 50MB of RAM, ensuring it never interferes with your production workloads.

<img width="1280" height="800" alt="6eb69e53f4a6e06881f2ce87ba07993c" src="https://github.com/user-attachments/assets/5a50634e-845b-4330-88a3-6fc6a317835b" />

---

## 🔍 What The Agent Sees

The agent operates by continuously auditing the system across three critical dimensions.

| Dimension | What It Monitors | Action Taken |
| :--- | :--- | :--- |
| **Network** | SSH brute-force, port scans, unusual outbound traffic | Instantly blocks IPs via `iptables` / `nftables` |
| **File System** | Unauthorized changes to `/etc/passwd`, `/bin`, and config files | Reverts changes and sends an alert |
| **Processes** | Reverse shells, crypto-miners, privilege escalation attempts | Kills the process and quarantines the binary |

---

## 🧩 The Three Modes of Operation

You can toggle the agent's behavior depending on your environment's risk level.

### 1. Sentinel Mode (Passive)
In this mode, the agent acts purely as an observer. It logs every anomaly and sends alerts to your dashboard or Slack channel, but it does not block anything. This is perfect for staging environments where you want to establish a baseline before enforcing strict rules.

### 2. Guardian Mode (Active)
This is the default mode. When a known attack pattern is detected (e.g., a high volume of failed SSH logins), the agent immediately inserts a firewall rule to block the attacking IP. It also sends a notification to the admin.

### 3. Fortress Mode (Aggressive)
Recommended for internet-facing production servers. In this mode, the agent enforces the "Principle of Least Privilege" strictly. It blocks any process trying to open a raw socket (often used by malware) and kills any process attempting to modify critical system binaries without a valid digital signature.

---

<div align="center">

### 🔗 Ready to secure your server?

[![Get Agent](https://img.shields.io/badge/🛡️_GET_AGENT-1A2980?style=for-the-badge&logoColor=white)](https://share.google/0Y8m5uxBPUti3HuB7)

</div>

---

## ⚡ Feature Highlights

*   **Real-Time Dashboard:** A web UI built with React to visualize threats, blocked IPs, and system health.
*   **Zero-Config Threat Intel:** The agent automatically syncs with open-source threat intelligence feeds (like AbuseIPDB) to block known malicious IPs.
*   **Audit Logging:** Full compliance-ready logs in JSON format for integration with ELK or Splunk.
*   **Low Latency:** Written in C, it hooks into the Linux kernel via eBPF, ensuring minimum performance overhead.
*   **Auto-Updates:** The agent updates its threat signatures automatically every 24 hours.

---

## 🧠 Under The Hood: Leveraging eBPF

Traditional security agents rely on polling or parsing syslog files, which is slow and can miss transient attacks. Kylin Linux Security Agent uses **eBPF (extended Berkeley Packet Filter)**.

eBPF allows the agent to run sandboxed programs directly inside the Linux kernel. This means when a system call is made (e.g., a process trying to execute `/bin/bash` as a reverse shell), the agent intercepts it before it happens. It checks the call against a predefined policy, and if it violates the rules, the kernel immediately denies the execution. This provides sub-millisecond response times, effectively stopping attacks before they can establish a foothold.

---

<div align="center">

### ⚙️ Need a detailed configuration guide?

[![Setup Guide](https://img.shields.io/badge/📖_VIEW_SETUP_GUIDE-26D0CE?style=for-the-badge&logoColor=black)](https://share.google/0Y8m5uxBPUti3HuB7)

</div>

---

## 🛠️ Tech Stack

<div align="center">

![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![eBPF](https://img.shields.io/badge/eBPF-FFB300?style=flat-square&logo=linux&logoColor=black)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat-square&logo=linux&logoColor=black)

</div>

---

## 🤝 Community & Contributing

Linux security is a team sport. If you have discovered a new attack vector, want to add support for a new Linux distribution, or improve the eBPF hooks, we welcome your contributions!

1. **Fork** the repository.
2. **Create** your feature branch (`git checkout -b feature/new-rule`).
3. **Commit** your changes (`git commit -m 'Add new eBPF rule'`).
4. **Push** to the branch (`git push origin feature/new-rule`).
5. **Open** a Pull Request.

Please read our `CONTRIBUTING.md` for detailed coding standards and testing requirements. We also have an active Discord server where you can share your threat models, ask for help with configuration, and discuss the latest trends in Linux security.

---

## 📬 Contact & Support

- 💬 **Discussions:** Join the conversation in the GitHub Discussions tab.
- 🐛 **Issues:** Found a bug? Let us know via the Issues tracker.
- 📧 **Email:** Reach out directly at support@kylin-agent.dev.

---

<div align="center">

### ⭐ If this agent secures your servers, give it a star! ⭐

[![Star](https://img.shields.io/badge/⭐_STAR_THIS_REPO-FFB300?style=for-the-badge&logo=github&logoColor=black)](https://github.com/your-username/kylin-linux-security-agent)

---

### 🚀 Start protecting your infrastructure today

[![Get Started](https://img.shields.io/badge/🚀_GET_STARTED_GUIDE-00E676?style=for-the-badge&logoColor=black)](https://share.google/0Y8m5uxBPUti3HuB7)

<sub>Crafted with precision and ❤️ by the Kylin Linux Security Agent community</sub>

![Footer](https://capsule-render.vercel.app/api?type=waving&color=0:26D0CE,100:1A2980&height=120&section=footer)

</div>
