<div align="center" style="text-align: center;">
  <p><a href="https://parhamghafouri.github.io/EmailTools/"><strong>English</strong></a> &nbsp;|&nbsp; <a href="https://parhamghafouri.github.io/EmailTools/README.fa.html"><strong>فارسی</strong></a></p>
  <p><img src="assets/logo.png" alt="Email Tools Logo" width="128"></p>
  <h1 align="center" style="text-align: center;">Email Tools for Microsoft Outlook</h1>
  <p align="center" style="text-align: center;">
    <strong>Sub-10ms Indexed Search &bull; Automated Task Tracking &bull; Smart Seasonal Archiving &bull; GAL Name Sync</strong><br>
    <em>The high-performance, privacy-first productivity suite built natively for Microsoft Outlook.</em>
  </p>
  <p align="center" style="text-align: center;">
    <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar"><img alt="Download Installer (.rar)" src="https://img.shields.io/badge/Download-Installer%20(.rar)-0078D4?style=flat-square&logo=windows&logoColor=white"></a>&nbsp;<a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest"><img alt="Release Notes v1.1.4" src="https://img.shields.io/badge/Release%20Notes-v1.1.4-555555?style=flat-square&logo=github&logoColor=white"></a>&nbsp;<a href="https://github.com/ParhamGhafouri/EmailTools/releases"><img alt="Total Downloads" src="https://img.shields.io/github/downloads/ParhamGhafouri/EmailTools/total?label=downloads&color=0078D4&style=flat-square"></a><br><a href="#requirements"><img alt="Windows 10 / 11" src="https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?style=flat-square&logo=windows"></a>&nbsp;<a href="#requirements"><img alt="Outlook 2016-365" src="https://img.shields.io/badge/Outlook-2016--365-0072C6?style=flat-square&logo=microsoftoutlook"></a>&nbsp;<a href="#security"><img alt="Signed Authenticode" src="https://img.shields.io/badge/Signed-Authenticode-success?style=flat-square"></a>
  </p>
  <p align="center" style="text-align: center;">
    <sub><strong>Per-User Installation</strong> &bull; No administrator privileges required &bull; 100% Offline & Private &bull; Seamless background self-updates</sub>
  </p>
</div>

---

## 🚀 Overview

Outlook is the backbone of daily business communication, but large mailboxes inevitably suffer from sluggish searches, broken Windows search indexing, mailbox quota warnings, buried action items, lost attachments on replies, and stale contact display names.

**Email Tools** is a lightweight, high-performance VSTO add-in engineered to solve these core limitations without requiring third-party cloud services or enterprise IT administrative rights. Everything runs locally on your PC, yielding **sub-10ms search results**, **automated email-to-task workflow management**, **smart seasonal archiving**, **one-click attachment actions**, and **automated GAL directory synchronization**.

<p align="center">
  <img src="assets/outlook-ribbon-tab.png" alt="Email Tools Ribbon Tab in Microsoft Outlook" width="600">
</p>

---

## ✨ Key Capabilities at a Glance

| Feature | Built-in Outlook | With Email Tools |
| :--- | :--- | :--- |
| **Message Body Search** | Slow, misses unindexed or mounted PSTs | **Instant (<10ms)** local SQLite FTS5 trigram index across all stores |
| **Task & Workflow Tracking** | Manual flags easily get buried in inbox noise | **Automated Task Tracker** with custom rule triggers, Kanban cards, and auto-resolve on reply |
| **Attachment Search** | Slow metadata lookup, no extension filters | **Instant dedicated search** with wildcard extensions (`*.pdf`, `*.xlsx`, etc.) |
| **Mailbox Full / Quotas** | Annoying quota popups, manual deletion | **Smart & Emergency Archiving** into auto-rotated 45 GB seasonal PSTs |
| **Storage & Quota Health** | Buried in backstage account settings | **Fluent 2 Status Gauges** with visual quota bars and drive capacity meters |
| **Reply with Attachments** | Manually re-attach files from sent items | **1-Click Reply / Reply All with Attachments** on the Home Ribbon |
| **Forward without Files** | Manual attachment deletion per email | **1-Click Forward without Attachments** (retains inline signatures) |
| **Corporate Directory Sync** | Stale historical names persist in rules & views | **Automatic GAL Reconciliation** during idle background time |
| **Vacation Prep** | Manual folder filing | **1-Click Vacation Mode** keeps recent mail, archives the rest safely |
| **Meeting Reminders** | Overdue past meeting popups pile up | **Silent automatic dismissal** of outdated meeting reminders |
| **Privacy & Storage** | Varies by cloud configuration | **100% Local Processing**; zero cloud uploads, zero external telemetry |

---

## 🔍 Feature Tour

### 1. Advanced Search (Sub-10ms Local Index)

A dedicated, non-blocking search cockpit featuring an intuitive query bar, real-time result sorting, virtualized grid rendering (up to 100,000 items), and a fully sandboxed preview pane.

<p align="center">
  <img src="assets/advanced-search-results.png" alt="Advanced Search Results and Preview" width="940">
  <br>
  <em>Instant query execution across all mailboxes, mounted PST archives, and historical conversation threads.</em>
</p>

* **SQLite FTS5 Trigram Engine:** Builds an ultra-compact, contentless trigram index locally. Searches message bodies in milliseconds without reopening or downloading messages from Exchange.
* **Dedicated Attachment Filename & Wildcard Filter:** Search specifically for attached filenames or extensions (e.g. `*.pdf`, `invoice`, `*.xlsx`) with smart inline signature noise filtering.
* **Sandboxed HTML Preview:** Includes Mark-of-the-Web isolation, web beacon suppression, script execution prevention, and SSRF blocking for completely safe message inspection.
* **Match Highlighting & Stepper:** Highlights matching query terms directly in the preview pane with instantaneous **Previous / Next** match navigation.
* **Multi-Criteria Queries:** Seamlessly combine **From**, **To**, **Cc**, **Subject**, **Body**, **Attachment Name**, **Date Range**, and **Hourly Windows**.
* **Rich Context Actions:** Right-click any result to Open, Reply, Reply All, Forward, Flag, Categorize, Move, Delete, Find Conversation, or Export to CSV (with formula-injection protection).

---

### 2. Task Tracker & Workflow Automation

Never let critical commitments, pending customer requests, or follow-ups slip through the cracks. Task Tracker bridges the gap between fast-moving emails and actionable task management directly inside Outlook.

<p align="center">
  <img src="assets/task-tracker.png" alt="Task Tracker Dashboard" width="940">
  <br>
  <em>High-contrast Kanban status summary cards, real-time filtering, and full thread context inspection.</em>
</p>

* **Kanban-Style Status Summary Cards:** Instantly overview tasks categorized as **To Do**, **In Progress**, **Waiting for Reply**, **Completed**, and **Overdue** with live counters and color-coded indicators.
* **Granular Automation Rule Builder:** Create powerful automation rules matching Incoming or Outgoing mail, specific senders/recipients, subject/body keywords, file attachment extensions, and urgency categories.
* **Auto-Resolve on Reply:** When you receive a reply to an email where you were waiting on feedback, Task Tracker automatically transitions the task state, keeping your workflow synchronized without manual upkeep.
* **Full Thread Inspection:** Inspect subject, sender, all direct (`To`) and copied (`Cc`) recipients, due dates, reminder deadlines, and custom task notes in an integrated side pane.
* **Modern Windows 11 Design:** Designed with Windows 11 DWM rounded corners, anti-aliased card borders, and automatic Office theme synchronization across Light, Dark Gray, and Black.

<p align="center">
  <img src="assets/task-rule-editor.png" alt="Task Automation Rule Editor" width="800">
  <br>
  <em>Visual rule editor supporting multi-field condition logic, exclusions, priority assignment, and default due date offsets.</em>
</p>

---

### 3. Smart Archive & Capacity Management

Never receive an Exchange *"Mailbox Quota Exceeded"* warning again. Smart Archive moves aging emails from your live Exchange mailbox into neatly organized, seasonal local PST archives (e.g., `2026-Season1.pst`).

<p align="center">
  <img src="assets/smart-archive-menu.png" alt="Smart Archive Ribbon Menu" width="400">
</p>

* **Fluent 2 Status & Health Cockpit:** Visual progress gauges showing live Exchange mailbox quota usage (with dynamic green/orange/red capacity thresholds) and archive drive free/total capacity meters.
* **Dynamic Ladder Acceleration:** Automatically identifies mailbox age distribution and skips empty date brackets to archive oldest mail first under pressure.
* **Emergency Quota Safeguard:** Automatically triggers intensive archival at 90% quota capacity and returns mailbox volume below your configured safe threshold.
* **Seasonal 45 GB Auto-Rollover:** Automatically partitions archives into quarterly volumes (`YYYY-Season1` through `Season4`) with an automatic rollover boundary at 45 GB to prevent PST corruption.
* **2-Hour Safety Floor Cooldown:** Prevents continuous background disk churning once the mailbox is safe.
* **Zero-Freeze Native Dialogs:** Modern, non-blocking UI dialogues styled with Windows 11 rounded geometry and theme-reactive typography.

<p align="center">
  <img src="assets/smart-archive-status.png" alt="Smart Archive Storage Status" width="440">
  &nbsp;&nbsp;&nbsp;&nbsp;
  <img src="assets/smart-archive-settings.png" alt="Smart Archive Threshold Settings" width="440">
</p>

---

### 4. Attachment Actions on the Home Ribbon

Eliminate repetitive attachment management steps directly from Outlook's main **Home** tab.

<p align="center">
  <img src="assets/attachment-actions.png" alt="Attachment Actions in Outlook Home Tab" width="440">
</p>

* **Reply with Attachment(s):** Composes a reply while automatically cloning and preserving all original files.
* **Reply All with Attachment(s):** Keeps all original attachments intact while replying to all original participants.
* **Forward without Attachment(s):** Strips bulky attached files to save bandwidth while intelligently retaining embedded company signature images.

---

### 5. Zero-Disruption GAL Display-Name Synchronization

When colleagues change roles, departments, or surnames in the corporate Active Directory / Exchange Global Address List (GAL), Outlook often preserves obsolete names in historical emails, rules, views, and search folders.

* **Safe Address Mapping:** Resolves recipient addresses against the corporate GAL and updates historical display labels only when a 1:1 unambiguous match is verified.
* **Out-of-Process Rule & View Repair:** Updates Outlook Rules, Views, and Exchange Search Folders safely after Outlook closes to avoid UI thread deadlocks.
* **Safe Checkpointing:** Checkpoints progress incrementally and resumes seamlessly across restarts without generating invasive mailbox diagnostic logs.

---

### 6. Vacation Mode & Overdue Reminder Cleanup

<p align="center">
  <img src="assets/vacation-mode.png" alt="Vacation Mode Dialog" width="440">
</p>

* **Vacation Mode:** Lighten your Inbox before heading out on leave. Retains the newest percentage of your Inbox (e.g., top 10%) and safely archives the rest into seasonal storage.
* **Overdue Reminder Dismissal:** Automatically and silently dismisses calendar reminder popups for meetings that have already concluded, preventing notification clutter each morning.

---

## 📦 Installation & Upgrades

### Fresh Installation
1. Download **`EmailTools_Setup.rar`** from the [Latest Release](https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar).
2. Extract the archive and launch **`EmailTools_Setup.exe`**.
3. Open Microsoft Outlook. The **Email Tools** tab will be ready on your ribbon.

### Upgrading from an Earlier Version
* **Do NOT uninstall the previous version.** Simply run the new installer; it automatically closes Outlook, updates all binaries, and preserves your existing database and settings.
* **Self-Healing Database Migrations:** Upgrades seamlessly migrate existing search indexes and task tracking schemas in under 15 milliseconds without requiring a slow re-index.

---

<h2 id="requirements">💻 System Requirements</h2>

| Specification | Requirement |
| :--- | :--- |
| **Operating System** | Windows 10 or Windows 11 (64-bit / 32-bit) |
| **Microsoft Outlook** | Outlook 2016, 2019, 2021, or Microsoft 365 Desktop Client |
| **Runtime** | Microsoft .NET Framework 4.8 or later |
| **User Privileges** | **Standard User** (Zero administrator privileges required) |

---

<h2 id="security">🛡️ Privacy, Security & Architecture</h2>

Email Tools was engineered with an uncompromising commitment to enterprise data sovereignty and privacy:

* **100% Local Execution:** All database queries, FTS5 full-text indexing, and archiving logic execute strictly on your local PC.
* **Zero Cloud Leakage:** No email bodies, metadata, or analytics are ever transmitted to external servers.
* **Sandboxed Preview Engine:** The message preview renders with Mark-of-the-Web isolation, suppressing scripts, tracking pixels, and unauthorized external network calls.
* **Authenticode Code-Signed:** All binaries (`EmailTools.dll`, `EmailTools.NameRepairWorker.exe`, `EmailTools.UpdateRunner.exe`, `EmailTools_Setup.exe`) are digitally signed with an Authenticode certificate (`42536C317058B3308A75D89E19F849B0B08BD39A`) and include RFC 3161 timestamps.

---

<div align="center" style="text-align: center;">
  <h2 align="center" style="text-align: center;">🌟 Support & Community</h2>

  <p align="center" style="text-align: center;">
    If Email Tools saves you time or frees up your mailbox, please consider giving the repository a star!
  </p>

  <p align="center">
    <a href="https://github.com/ParhamGhafouri">
      <img src="https://img.shields.io/github/stars/ParhamGhafouri/EmailTools?style=for-the-badge&label=Star%20on%20GitHub&color=yellow&logo=github" alt="Star on GitHub">
    </a>
  </p>

  <hr>

  <p align="center" style="text-align: center;">
    <strong>Architected & Developed by Parham Ghafouri</strong><br>
    <a href="https://github.com/ParhamGhafouri"><img alt="GitHub: ParhamGhafouri" src="https://img.shields.io/badge/GitHub-ParhamGhafouri-24292e?style=flat-square&logo=github"></a>&nbsp;<a href="https://www.linkedin.com/in/parhaam/"><img alt="LinkedIn: parhaam" src="https://img.shields.io/badge/LinkedIn-parhaam-0A66C2?style=flat-square&logo=linkedin"></a><br>
    <sub>&copy; Parham Ghafouri. Released as Freeware under the MIT-compatible open software license.</sub>
  </p>
</div>
