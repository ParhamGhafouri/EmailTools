<p align="center">
  <a href="README.md"><strong>English</strong></a> &nbsp;|&nbsp;
  <a href="README.fa.md">فارسی</a>
</p>

<p align="center">
  <img src="assets/logo.png" alt="Email Tools logo" width="124">
</p>

<h1 align="center">Email Tools for Microsoft Outlook</h1>

<p align="center">
  <strong>Search deeper. Keep names current. Archive safely. Handle attachments in one click.</strong><br>
  A polished, per-user Outlook add-in for indexed body search, GAL display-name synchronization, Smart Archive, bulk mail actions, attachment workflows, reminder cleanup, and verified updates.
</p>

<p align="center">
  <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest"><img alt="Latest release" src="https://img.shields.io/github/v/release/ParhamGhafouri/EmailTools?label=version&color=2D7DD2"></a>
  <a href="https://github.com/ParhamGhafouri/EmailTools/releases"><img alt="Downloads" src="https://img.shields.io/github/downloads/ParhamGhafouri/EmailTools/total?color=2D7DD2"></a>
  <a href="#requirements"><img alt="Windows" src="https://img.shields.io/badge/platform-Windows-0078D6"></a>
  <a href="#requirements"><img alt="Outlook" src="https://img.shields.io/badge/Outlook-2016%20%7C%202019%20%7C%202021%20%7C%20365-0072C6"></a>
  <a href="LICENSE"><img alt="License" src="https://img.shields.io/badge/license-Freeware-brightgreen"></a>
</p>

<p align="center">
  <a href="https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar"><strong>Download the latest installer package</strong></a>
  <br>
  <sub>Installs for your Windows account only. No admin rights. Auto-updates after Outlook closes.</sub>
</p>

<p align="center">
  <a href="https://github.com/ParhamGhafouri/EmailTools">Star the repo</a> if Email Tools saves you time. It helps other Outlook users find it.
</p>

---

## Why It Exists

Outlook is excellent at mail, but painful at repeated mailbox work: finding old conversations across archives, repairing stale names after directory changes, replying while keeping attachments, clearing a mailbox before time away, and keeping PST archives organized. **Email Tools** adds those missing workflows directly to the Outlook ribbon without requiring administrator access or an additional server component.

<p align="center">
  <img src="assets/outlook-ribbon-tab.png" alt="Email Tools ribbon tab in Microsoft Outlook" width="520">
</p>

## Product Tour

### Advanced Search

A dedicated search window for real mailbox investigations: fields at the top, sortable results on the left, and a live Outlook-style preview on the right.

**The big reason it exists:** Outlook's built-in search can miss message bodies when Windows indexing is stale, archives are mounted late, or a mailbox has years of PST history. Email Tools builds its own local, per-user body index so searching the actual contents of messages stays fast and predictable across mailboxes and seasonal archives.

<p align="center">
  <img src="assets/advanced-search-results.png" alt="Advanced Search results with preview and context actions" width="920">
  <br>
  <sub>Search every mailbox and archive, preview messages, then act on one result or hundreds.</sub>
</p>

- Combine **From**, **To**, **Cc**, **Subject**, and **Body** filters.
- Search the **indexed message body**, not only headers or whatever Outlook's current index happens to expose.
- Keep archive search useful: seasonal PST archives remain searchable even when Outlook's native indexing lags behind.
- Search the current folder, the whole mailbox, or mounted archives.
- Narrow by attachments, date range, flagged state, or saved searches.
- Right-click results to open, reply, forward, flag, categorize, move, delete, find related messages, or export to CSV.

### GAL Display-Name Synchronization

When a person is renamed in the Global Address List (GAL), Outlook can keep the old display name inside historical messages, rules, views, and Search Folders. That leaves the same mailbox identity appearing under different names and can make name-based filters stop matching. Email Tools reconciles those recognized identities with the current GAL while protecting Outlook's visible interface.

- Updates historical **From**, **Sender**, **To**, **Cc**, and **Bcc** display names.
- Covers normal mailbox folders, shared stores, and mounted archive/PST folders.
- Matches by mailbox address and updates a name only when it maps safely to one current GAL identity.
- Leaves external, deleted, unknown, or ambiguous recipients unchanged.
- Repairs messages during idle background time; rules, views, and Exchange Search Folder criteria are handled only after Outlook closes, avoiding disruptive rule prompts or broken folder views.
- Checkpoints progress and resumes automatically after Outlook or Windows restarts.
- Runs without prompts and does not produce mailbox-content or recipient diagnostic logs.

### Attachment Actions

The Home tab gets three focused buttons that appear where people already work.

<p align="center">
  <img src="assets/attachment-actions.png" alt="Reply with attachments, Reply All with attachments, Forward without attachments, and Advanced Search buttons" width="420">
</p>

- **Reply with Attachment(s)** keeps the original files in your reply.
- **Reply All with Attachment(s)** keeps the original files for every recipient.
- **Forward without Attachment(s)** strips file attachments while preserving inline signature images.

### Smart Archive

Smart Archive keeps mailboxes lean by moving older mail into local seasonal archives such as `2026-Season1`. Mail is moved, never deleted, and protected Outlook folders stay untouched.

<p align="center">
  <img src="assets/smart-archive-menu.png" alt="Smart Archive menu in the Outlook ribbon" width="360">
</p>

- Runs quietly after Outlook starts, once per day.
- Files older mail into dated archives in small background steps so Outlook stays responsive.
- Steps up automatically when a mailbox is close to full.
- Migrates legacy PST archives into the right seasonal archive, then removes the empty source only after verification.

<table>
  <tr>
    <td align="center" width="50%">
      <img src="assets/smart-archive-status.png" alt="Smart Archive status window" width="340"><br>
      <sub>Status shows archive health, mounted PSTs, quota, free space, last run, and search index readiness.</sub>
    </td>
    <td align="center" width="50%">
      <img src="assets/smart-archive-settings.png" alt="Smart Archive settings window" width="420"><br>
      <sub>Settings let you choose when archiving should step up as the mailbox approaches quota.</sub>
    </td>
  </tr>
</table>

### Vacation Mode

Clear the inbox before time away without losing anything. Vacation Mode keeps the newest slice of the Inbox and archives the older mail into dated archives.

<p align="center">
  <img src="assets/vacation-mode.png" alt="Vacation Mode dialog" width="460">
</p>

### Reminder Cleanup

Overdue reminders for meetings that already passed are dismissed quietly so they do not pile up every morning.

### Verified Auto-Updates

Email Tools checks GitHub Releases once a day and installs new versions silently after Outlook closes. The updater verifies the downloaded installer with SHA-256 and a pinned Authenticode certificate before it can run.

---

## Installation

1. Download `EmailTools_Setup.rar` from the [latest release](https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar).
2. Extract the archive and run `EmailTools_Setup.exe`.
3. Start Outlook. The **Email Tools** ribbon tab appears, and the attachment buttons are added to the Home tab.

Already have Email Tools installed? **Do not uninstall it first.** Run the new installer over the existing version and setup upgrades it in place. Setup installs per-user, needs no administrator rights, and closes Outlook automatically if Outlook is running. To repair or remove Email Tools later, run `EmailTools_Setup.exe` again or uninstall it from **Settings → Apps**.

> On first start, Smart Archive may do a short background tidy, the search index may begin building, and GAL name synchronization may inspect historical items. The jobs are coordinated, run in small background steps, and resume automatically so Outlook remains usable.

---

## Requirements

| | |
|---|---|
| **Operating system** | Windows 10 or Windows 11 |
| **Outlook** | Microsoft Outlook 2016, 2019, 2021, or Microsoft 365 desktop |
| **Framework** | .NET Framework 4.8 |
| **Privileges** | None. Installs per-user. |

---

## Privacy And Safety

- Mail search, archiving, indexing, and GAL reconciliation run on your PC against your configured Outlook and Exchange profile.
- No mailbox content is uploaded.
- Network access is limited to your configured Exchange/GAL services and the update check against GitHub Releases; Email Tools uses no third-party mailbox service.
- No mailbox-content, recipient, search-index, updater, or GAL diagnostic log is produced.
- Updates are accepted only when the installer hash and pinned code-signing certificate match.

---

## FAQ

**Does Smart Archive delete email?**  
No. It moves older mail into local archives. Protected folders such as Calendar, Contacts, Tasks, Notes, Drafts, Outbox, Deleted Items, and Conversation History are not archived.

**Does it need admin rights?**  
No. Email Tools installs under your own Windows account.

**Can I still search archived mail?**  
Yes. Seasonal archives remain mounted in Outlook and are searchable from Advanced Search.

**What does GAL synchronization change?**  
It updates recognized Outlook display names to the current name in your organization's Global Address List. It does not change email addresses, message bodies, attachments, or unknown recipients. Rules, views, and Search Folders are repaired only while visible Outlook is closed.

**Why does Email Tools build its own body index?**  
Because the feature was built for real support and audit work where "maybe Outlook indexed it" is not good enough. The local body index makes old messages, archived PSTs, and body-text searches behave consistently without uploading mailbox content anywhere.

**Will the first body-index build slow Outlook down?**  
No. The first build can take time on a large mailbox because it reads your existing messages and archives, but it deliberately works in short background slices. You can continue using Outlook while Email Tools builds and then maintains the index.

---

## Changelog

See the [Releases page](https://github.com/ParhamGhafouri/EmailTools/releases) for version history and release notes.

---

<h2 align="center">Enjoying Email Tools?</h2>

<p align="center">
  <a href="https://github.com/ParhamGhafouri/EmailTools"><strong>Star it on GitHub</strong></a><br>
  <sub>It is the easiest way to support the project and help more people discover it.</sub>
</p>

---

<p align="center">
  <strong>Designed and developed by Parham Ghafouri</strong><br>
  <a href="https://github.com/ParhamGhafouri"><img alt="GitHub: ParhamGhafouri" src="https://img.shields.io/badge/GitHub-ParhamGhafouri-24292e?logo=github"></a>
  <a href="https://www.linkedin.com/in/parhaam/"><img alt="LinkedIn: parhaam" src="https://img.shields.io/badge/LinkedIn-parhaam-0A66C2?logo=linkedin"></a>
  <br>
  <sub>© 2026 Parham Ghafouri. All rights reserved.</sub>
</p>
