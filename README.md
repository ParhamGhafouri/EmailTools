<div align="center" style="text-align: center;">
  <p><a href="https://parhamghafouri.github.io/EmailTools/guide.html"><strong>English</strong></a> &nbsp;|&nbsp; <a href="https://parhamghafouri.github.io/EmailTools/guide.fa.html"><strong>فارسی</strong></a></p>
  <p><img src="assets/logo.png" alt="Email Tools Logo" width="128"></p>
  <h1 align="center" style="text-align: center;">Email Tools for Microsoft Outlook</h1>
  <p align="center" style="text-align: center;">
    <strong>Fast Indexed Search &bull; Automated Task Tracking &bull; Smart Seasonal Archiving &bull; GAL Name Sync</strong><br>
    <em>Find messages, follow up on work, and manage mailbox space in classic Outlook for Windows.</em>
  </p>
  <p align="center" style="text-align: center;">
    <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar"><img alt="Download Installer (.rar)" src="https://img.shields.io/badge/Download-Installer%20(.rar)-0078D4?style=flat-square&logo=windows&logoColor=white"></a>&nbsp;<a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest"><img alt="Release Notes v1.2.0" src="https://img.shields.io/badge/Release%20Notes-v1.2.0-555555?style=flat-square&logo=github&logoColor=white"></a>&nbsp;<a href="https://github.com/ParhamGhafouri/EmailTools/releases"><img alt="Total Downloads" src="https://img.shields.io/github/downloads/ParhamGhafouri/EmailTools/total?label=downloads&color=0078D4&style=flat-square"></a><br><a href="#requirements"><img alt="Windows 10 / 11" src="https://img.shields.io/badge/Windows-10%20%2F%2011-0078D6?style=flat-square&logo=windows"></a>&nbsp;<a href="#requirements"><img alt="Outlook 2016-365" src="https://img.shields.io/badge/Outlook-2016--365-0072C6?style=flat-square&logo=microsoftoutlook"></a>&nbsp;<a href="#security"><img alt="Signed Authenticode" src="https://img.shields.io/badge/Signed-Authenticode-success?style=flat-square"></a>
  </p>
  <p align="center" style="text-align: center;">
    <sub><strong>Per-User Installation</strong> &bull; No administrator privileges required &bull; Local Mail Processing &bull; GitHub update checks</sub>
  </p>
</div>

---

## Overview

Large mailboxes make it harder to find messages, track follow-ups, and manage storage. Email Tools brings these workflows together inside classic Outlook for Windows.

**Email Tools** is a per-user VSTO add-in with **local indexed search**, **email-to-task tracking**, **seasonal PST archiving**, **attachment actions**, and **GAL display-name synchronization**. Search and task databases stay on your PC; Outlook continues to handle your mail account normally.

<p align="center">
  <img src="assets/outlook-ribbon-tab.png" alt="Email Tools Ribbon Tab in Microsoft Outlook" width="219">
</p>

---

## What's new in 1.2.0

- **Choose how archiving runs:** Auto Archive, Manual Only, or Disabled (Search & Tasks Only). Returning to Auto resumes the automatic workflow without restarting Outlook.
- **More accurate search:** Better person and domain-qualified address matching, preserved long recipient lists, and header verification that retries failed reads without clearing indexed text.
- **Clearer message context:** Reply/forward history and **Find related messages** in the preview, plus consistent attachment menus and left-to-right attachment layouts.
- **More efficient index maintenance:** Fewer redundant writes and folder lookups, with improved database upgrade cleanup.

[Read the full 1.2.0 release notes](https://github.com/ParhamGhafouri/EmailTools/releases/tag/v1.2.0) · [Download 1.2.0](https://github.com/ParhamGhafouri/EmailTools/releases/tag/v1.2.0)

**Explore:** [Search](#1-advanced-search-local-index) · [Tasks](#2-task-tracker--workflow-automation) · [Archiving](#3-smart-archive--capacity-management) · [Install](#installation) · [Compatibility](#requirements) · [Privacy](#security)

## Key capabilities

| Feature | What Email Tools provides |
| :--- | :--- |
| **Advanced Search** | Local indexed body and metadata search across connected mailboxes and mounted PSTs |
| **Task Tracker** | Email-to-task conversion, automation rules, status cards, due dates, and notes |
| **Attachment Filters** | File-attachment presence, filename, and extension filters such as `*.pdf` and `*.xlsx` |
| **Smart Archive** | Seasonal PST archives, capacity monitoring, and automatic volume rollover at 45 GB |
| **Attachment Actions** | Reply / Reply All with file attachments; Forward without file attachments |
| **GAL Name Sync** | Background reconciliation of historical display names with the corporate directory |
| **Vacation Mode** | Keep a chosen percentage of recent Inbox messages and archive the rest |
| **Reminder Cleanup** | Dismiss reminders for meetings that have already ended |
| **Local Storage** | Search indexes, task databases, and archives remain on your PC |

---

## Feature tour

### 1. Advanced Search (Local Index)

A dedicated search window with combined filters, sortable results, a virtualized grid, and an integrated message preview.

<p align="center">
  <img src="assets/advanced-search-results.png" alt="Advanced Search Results and Preview" width="940">
  <br>
  <em>Search indexed messages in connected mailboxes, mounted PST archives, and conversation folders.</em>
</p>

* **Independent Local Index:** Uses SQLite FTS5 trigrams to search indexed message bodies without depending on Windows Search. Initial indexing and later synchronization run in the background; search speed depends on the query, index coverage, and PC.
* **Dedicated Attachment Filename & Wildcard Filter:** Search specifically for attached filenames or extensions (e.g. `*.pdf`, `invoice`, `*.xlsx`) with smart inline signature noise filtering.
* **Protected HTML Preview:** Uses Mark-of-the-Web isolation and blocks scripts, remote tracking images, and external preview requests.
* **Match Highlighting & Navigation:** Highlights matching body terms in the preview, with **Previous / Next** navigation.
* **Multi-Criteria Queries:** Seamlessly combine **From**, **To**, **Cc**, **Subject**, **Body**, **Attachment Name**, **Date Range**, and **Hourly Windows**.
* **Rich Context Actions:** Right-click any result to Open, Reply, Reply All, Forward, Flag, Categorize, Move, Delete, Find Conversation, or Export to CSV (with formula-injection protection).

**Search tips:** Wait for initial indexing to finish, and keep the PST archives you want to search mounted in Outlook. For an extension filter, select **Attachment → Yes** and enter `*.txt`, `*.pdf`, or `*.xlsx` in the filename field. Use **Any Hours**, **Working Hours**, or **Outside Working Hours**; work-hour filters use your Outlook calendar settings.

**After upgrading:** A one-time header recheck may show **Message headers awaiting verification**. It reads full headers in the background; **Ready** returns after required work completes. Searches involving unverified fields may be marked partial until then.

---

### 2. Task Tracker & Workflow Automation

Turn messages into tasks with due dates, priorities, notes, and status tracking. Task Tracker searches tracked tasks; Advanced Search searches indexed messages.

<p align="center">
  <img src="assets/task-tracker.png" alt="Task Tracker Dashboard" width="940">
  <br>
  <em>An email-linked task list with status, due dates, notes, and an integrated message preview.</em>
</p>

* **Status & Due-Date Tracking:** Filter tracked tasks by view, category and priority, review overdue work, and update the selected task without losing its source-message context.
* **Granular Automation Rule Builder:** Create powerful automation rules matching Incoming or Outgoing mail, specific senders/recipients, subject/body keywords, file attachment extensions, and urgency categories.
* **Auto-Resolve on Reply:** When you receive a reply to an email where you were waiting on feedback, Task Tracker automatically transitions the task state, keeping your workflow synchronized without manual upkeep.
* **Full Thread Inspection:** Inspect subject, sender, all direct (`To`) and copied (`Cc`) recipients, due dates, reminder deadlines, and custom task notes in an integrated side pane.
* **Modern Windows 11 Design:** Designed with Windows 11 DWM rounded corners, anti-aliased card borders, and automatic Office theme synchronization across Light, Dark Gray, and Black.

<p align="center">
  <img src="assets/task-rule-editor.png" alt="Task Automation Rule Editor" width="940">
  <br>
  <em>Visual rule editor supporting multi-field condition logic, exclusions, priority assignment, and default due date offsets.</em>
</p>

---

### 3. Smart Archive & Capacity Management

Smart Archive helps manage mailbox capacity by moving older messages from your mailbox to seasonal local PST files, such as `2026-Season1.pst`.

<p align="center">
  <img src="assets/smart-archive-menu.png" alt="Smart Archive Ribbon Menu" width="258">
</p>

* **Mailbox & Index Status:** Review mailbox capacity, archive drive space, managed PSTs, and search-index readiness in one dialog.
| Archive mode | Behavior |
| :--- | :--- |
| **Auto Archive** | Automatic capacity protection, scheduled archiving and Flag Recovery |
| **Manual Only** | Automatic archiving is off; use Archive Now or Vacation Mode when needed |
| **Disabled** | Archive operations and archive maintenance are off; Search and Task Tracker remain available |

* **Dynamic Ladder Acceleration:** Automatically identifies mailbox age distribution and skips empty date brackets to archive oldest mail first under pressure.
* **Quota-Based Archiving:** Uses mailbox capacity and configured thresholds to prioritize older messages when space is low.
* **Seasonal 45 GB Rollover:** Organizes archives as `YYYY-Season1` through `Season4` and starts another volume at 45 GB to leave headroom below the PST size limit.
* **2-Hour Safety Floor Cooldown:** Prevents continuous background disk churning once the mailbox is safe.
* **Theme-Aware Dialogs:** Storage, settings, and archive dialogs follow the Outlook theme.

<p align="center">
  <img src="assets/smart-archive-status.png" alt="Smart Archive Storage Status" width="440">
  &nbsp;&nbsp;&nbsp;&nbsp;
  <img src="assets/smart-archive-settings.png" alt="Smart Archive Threshold Settings" width="440">
</p>

---

### 4. Attachment & Quick Workflow Actions on the Home Ribbon

Eliminate repetitive attachment and workflow steps directly from Outlook's main **Home** tab.

<p align="center">
  <img src="assets/attachment-actions.png" alt="Attachment and Workflow Actions in Outlook Home Tab" width="413">
</p>

* **Reply with Attachment(s):** Creates a reply and copies the original message’s file attachments.
* **Reply All with Attachment(s):** Creates a reply to all participants with the original file attachments.
* **Forward without Attachment(s):** Strips bulky attached files to save bandwidth while intelligently retaining embedded company signature images.
* **Track as Task:** Instant 1-click email-to-task conversion with direct synchronization into the Task Tracker dashboard.

---

### 5. GAL Display-Name Synchronization

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

<h2 id="installation">Installation & upgrades</h2>

### Fresh Installation

1. Download **`EmailTools_Setup.rar`** from the [Latest Release](https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar).
2. Extract the archive, save your drafts, close Outlook, and run **`EmailTools_Setup.exe`**.
3. Open Microsoft Outlook. The **Email Tools** tab will be ready on your ribbon.

### Upgrading from an Earlier Version

* **Keep the previous installation.** Save drafts and close Outlook before running the new installer. Your existing settings and databases are retained and upgraded as needed.
* **Automatic Database Upgrades:** The add-in updates existing search and task databases when required. Migration and indexing time depend on the data and the changes in that release.

---

<h2 id="requirements">💻 System Requirements</h2>

| Specification | Requirement |
| :--- | :--- |
| **Operating System** | Windows 10 or Windows 11; Windows 11 requires a 64-bit system |
| **Microsoft Outlook** | Classic Outlook for Windows: 2016, 2019, 2021, or Microsoft 365; 32-bit or 64-bit Office |
| **Runtime** | Microsoft .NET Framework 4.8 or later |
| **User Privileges** | **Standard User** (Zero administrator privileges required) |

**Storage:** Keep a backup of important PST files. An archive on your PC is not a replacement for a backup. Search covers connected stores and mounted PSTs; an unmounted archive is not included.

**Compatibility:** New Outlook for Windows, Outlook on the web, and Outlook for Mac do not support this VSTO add-in. Windows, .NET, or Office prerequisites may require IT assistance on a managed PC.

---

<h2 id="security">🛡️ Privacy, Security & Architecture</h2>

Email Tools processes search, task, and archive data locally. Account synchronization and corporate directory access continue through Outlook and your organization’s services.

* **100% Local Execution:** All database queries, FTS5 full-text indexing, and archiving logic execute strictly on your local PC.
* **No External Mail Analysis:** The add-in does not upload email content to a third-party analysis service. Update checks and downloads contact GitHub.
* **Sandboxed Preview Engine:** The message preview renders with Mark-of-the-Web isolation, suppressing scripts, tracking pixels, and unauthorized external network calls.
* **Signed Releases:** Product binaries and the installer use Authenticode signatures with RFC 3161 timestamps. The publisher certificate is self-signed; Windows trust and SmartScreen prompts depend on local or organizational policy.

---

<div align="center" style="text-align: center;">
  <h2 align="center" style="text-align: center;">🌟 Support & Community</h2>

  <p align="center" style="text-align: center;">
    If Email Tools saves you time or frees up your mailbox, please consider giving the repository a star!
  </p>

  <p align="center">
    <a href="https://github.com/ParhamGhafouri/EmailTools">
      <img src="https://img.shields.io/github/stars/ParhamGhafouri/EmailTools?style=for-the-badge&label=Star%20on%20GitHub&color=yellow&logo=github" alt="Star on GitHub">
    </a>
  </p>

  <hr>

  <p align="center" style="text-align: center;">
    <strong>Architected & Developed by Parham Ghafouri</strong><br>
    <a href="https://github.com/ParhamGhafouri"><img alt="GitHub: ParhamGhafouri" src="https://img.shields.io/badge/GitHub-ParhamGhafouri-24292e?style=flat-square&logo=github"></a>&nbsp;<a href="https://www.linkedin.com/in/parhaam/"><img alt="LinkedIn: parhaam" src="https://img.shields.io/badge/LinkedIn-parhaam-0A66C2?style=flat-square&logo=linkedin"></a><br>
    <sub>&copy; Parham Ghafouri. Freeware for personal and internal business use. See the <a href="https://github.com/ParhamGhafouri/EmailTools/blob/main/LICENSE">license terms</a>.</sub>
  </p>
</div>
