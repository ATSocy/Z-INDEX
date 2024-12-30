Thread: operations-sig-meeting-5-18-nov-2024-8pm-cest
0x3639 | 2024-11-04 19:58:39 UTC | #1

**What:** Meeting to Discuss Improving Node Operations
**When:** [18 Nov 2024 @ 8PM CEST](https://www.worldtimebuddy.com/?qm=1&lid=12,2643743,5128581,6&h=5128581&date=2024-11-18&sln=14-15&hf=1)
**Where:** [https://element.zenon.chat/#/room/#sig-operations:hc1.chat ](https://element.zenon.chat/#/room/#sig-operations:hc1.chat)
**Agenda & Notes:** [Operations SIG 26 Aug 2024 - Zenon Wiki ](https://zenon.wiki/index.php/Operations_SIG_18_Nov_2024)

Attention Participants. Please update the meeting notes before the meeting.

-------------------------

0x3639 | 2024-12-23 17:00:25 UTC | #2

# LLM Briefing Document: Operation Sig Meeting - November 19, 2024

**Date:** November 19, 2024  
**Participants:** deeznnutz, vilkris, coinselor  

**Purpose:** This document summarizes the key discussion points and action items from the Operation Sig meeting on November 19, 2024. The meeting focused on diagnosing performance issues with go-zenon, improving troubleshooting processes, and strategizing for backup and restore functionality.

---

## Key Themes and Ideas

### **go-zenon Sync Performance & Hypervisor Impact**
- **Problem:** Performance concerns with the go-zenon sync process, potentially related to the hypervisor.
- **Proposed Solution:** A two-part test proposed by deeznnutz:
  - Test 1: Sync go-zenon on a bare-metal server (Supermicro SuperServer 5018D-FN8T).
  - Test 2: Install Proxmox on the same server, allocate all resources to a VM, and repeat the sync.
- **Goal:** Determine if the hypervisor causes bottlenecks.
- **Quotes:**
  - deeznnutz: "With this we can determine if the hypervisor is causing an issue."
  - vilkris: "It's good if others can replicate the results. It's also easy for anyone to confirm by syncing the node locally."

---

### **Standardizing Sync Testing & Data Collection**
- **Problem:** Sync time is not measured consistently or with sufficient data.
- **Data Needed:** 
  - Cloud provider, VM type, system specs (CPU, RAM, storage), internet speed, ping.
- **Implementation:**
  - **Temporary Bash Script:** deeznnutz will parse logs to time syncs (e.g., height 1 to 8M blocks).
  - **Long-Term Solution:** George is developing a go-based tool to track momentum production with Grafana.
- **Quotes:**
  - vilkris: "Logs seem like the easiest approach. They are timestamped and should record when a momentum is inserted, at least on the debug level."

---

### **Troubleshooting Script & Data Output**
- **Problem:** Troubleshooting go-zenon is time-intensive, especially for users with limited Linux experience.
- **Proposed Solution:** A script to gather essential system data (e.g., disk space, specs).
- **Output Challenges:** Finding a secure and easy method for users to share script output.
  - **Ideas:**
    - **Telegram Bot:** Encrypt API keys to send data securely.
    - **API:** Explore secure data transfer methods like nostr/tor.
    - **Copy/Paste:** Use temporarily until better solutions are found.
  - **Quotes:**
    - deeznnutz: "I get a lot of screenshots, which is why I would love a file."
    - coinselor: "I’ll review and improve the script and start learning go to create a wrapper using the Bubble Tea framework."

---

### **Backup & Restore Functionality**
- **Progress:** A local backup/restore script is ready for review.
- **Future Plans:** 
  - Start with local backups and move to remote options (e.g., S3, SCP).
  - Consider connectors for cloud providers if in scope.
- **Quotes:**
  - vilkris: "If the new suggested approach is to sync the node locally, then being able to transfer the node data onto the server would be useful."
  - deeznnutz: "It’s just a .tar, scp, and untar."
  - coinselor: "There are probably tools already built we could leverage."

---

### **HQZ (High Quality Zone) Support**
- **Reusability:** Existing scripts can be easily adapted for HQZ.
- **George's Work:**
  - Complete the dashboard and auto-install functionality.
  - Develop a time-series data exporter for znnd logs.

---

## Action Items

### **deeznnutz**
- Implement sync tests (bare-metal vs. Proxmox).
- Develop the bash script for sync timing.
- Publish the troubleshooting script.
- Explore secure data transfer methods (Telegram bot, API).
- Submit the local backup/restore script for review.
- Continue HQZ script development.

### **vilkris**
- Test on Mac M1 when possible.

### **coinselor**
- Review the troubleshooting script and provide feedback.
- Begin developing a go wrapper for the troubleshooting script (Bubble Tea framework).
- Investigate parsing time-series data from znnd exporter.
- Research secure data output methods (e.g., nostr/tor).

### **All**
- Consider options for automated data transfer from troubleshooting scripts.
- Revisit backup/restore strategies, focusing on remote capabilities (SCP).
- Evaluate connectors for specific cloud providers.

---

**Next Meeting:** December 16, 2024, 8 PM UTC

This briefing document highlights the ongoing efforts to optimize go-zenon performance, streamline troubleshooting, and establish reliable backup/restore mechanisms.

---

-------------------------

