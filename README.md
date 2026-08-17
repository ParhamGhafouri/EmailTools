<p align="center" class="language-switch">
  <a href="https://parhamghafouri.github.io/EmailTools/"><strong>English</strong></a> &nbsp;|&nbsp;
  <a href="https://parhamghafouri.github.io/EmailTools/README.fa.html">فارسی</a>
</p>

<p align="center">
  <img src="assets/logo.png" alt="Email Tools logo" width="124">
</p>

<h1 align="center">Email Tools for Microsoft Outlook</h1>

<p align="center">
  <strong>Search complete message bodies. Keep names current. Archive to a clear target. Handle attachments in one click.</strong><br>
  A free, per-user Outlook add-in for local indexed search, GAL display-name synchronization, verified seasonal archiving, bulk mail actions, attachment workflows, reminder cleanup, and signed updates.
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

Outlook handles email well, but repeated mailbox work can still take too many steps: finding old conversations across archives, repairing stale names after directory changes, replying while keeping attachments, clearing a mailbox before time away, and keeping PST archives organized. **Email Tools** adds those workflows directly to the Outlook ribbon without administrator access or an additional server component.

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
- Prepare indexed results locally without making Outlook reopen every matching message.
- Keep large result sets responsive in a virtual grid that supports up to 100,000 rows without repeatedly rebinding an unchanged list.
- Highlight every rendered body-text match in the original HTML preview and move through occurrences with Previous/Next controls.
- Keep rights-managed mail searchable by sender, subject, date, folder, and other safe metadata without opening its encrypted body in the background.
- Keep archive search useful: seasonal PST archives remain searchable even when Outlook's native indexing lags behind.
- Search the current folder, the whole mailbox, or mounted archives.
- Narrow by attachments, date range, flagged state, or saved searches.
- Display result and preview timestamps in the user's local system time.
- Right-click results to open, reply, forward, flag, categorize, move, delete, find related messages, or export to CSV.

### GAL Display-Name Synchronization

When a person is renamed in the Global Address List (GAL), Outlook can keep the old display name inside historical messages, rules, views, and Search Folders. That leaves the same mailbox identity appearing under different names and can make name-based filters stop matching. Email Tools reconciles those recognized identities with the current GAL while protecting Outlook's visible interface.

- Updates historical **From**, **Sender**, **To**, **Cc**, and **Bcc** display names.
- Covers normal mailbox folders, shared stores, and mounted archive/PST folders.
- Matches by mailbox address and updates a name only when it maps safely to one current GAL identity.
- Leaves external, deleted, unknown, or ambiguous recipients unchanged.
- Repairs messages during idle background time. Rules, Views, and Exchange Search Folder criteria are handled only after Outlook closes.
- Preserves the existing rule-recipient identity and changes only a safely matched cached display label.
- Saves a rule store only after every rule and destination has been inspected successfully; an unreadable or unsafe rule leaves the store unchanged for a later retry.
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

Smart Archive keeps mailboxes lean by moving older mail into local seasonal archives such as `2026-Season1`. Ordinary mail is moved to a verified archive destination, not permanently deleted, and protected Outlook folders stay untouched.

<p align="center">
  <img src="assets/smart-archive-menu.png" alt="Smart Archive menu in the Outlook ribbon" width="360">
</p>

- Runs quietly after Outlook starts and rechecks during the day when mailbox usage crosses the percentage saved in Settings.
- Uses the verified Exchange quota and stops as soon as the configured target is reached.
- Under pressure, works through a bounded 30/20/10/8/6/4/2/1-day sequence while protecting mail from the newest 24 hours.
- Gives Emergency Archive first priority at 90% of verified quota and uses the saved Smart Archive percentage as the exit target.
- Files older mail into dated archives in bounded background steps.
- Migrates legacy PST archives into the correct account and seasonal archive, then removes the source only after recursive exact-zero verification.
- Queues rights-managed messages while Outlook is open and moves them with a signed hidden worker after Outlook closes, without launching Office Rights Management setup.

<p align="center">
  <img src="assets/smart-archive-status.png" alt="Smart Archive status window" width="520"><br>
  <sub>Status shows archive health, mounted PSTs, verified quota, measured progress, last run, and search-index readiness.</sub>
</p>

<p align="center">
  <img src="assets/smart-archive-settings.png" alt="Smart Archive settings window" width="520"><br>
  <sub>The saved percentage is the real target used by Smart Archive and Emergency Archive.</sub>
</p>

### Vacation Mode

Clear the Inbox before time away without losing ordinary mail. Vacation Mode keeps the newest selected portion of the Inbox and moves older eligible messages to verified seasonal archives using the same destination and post-move checks as Smart Archive.

<p align="center">
  <img src="assets/vacation-mode.png" alt="Vacation Mode dialog" width="460">
</p>

### Reminder Cleanup

Overdue reminders for meetings that already passed are dismissed quietly so they do not pile up every morning.

### Verified Auto-Updates

Email Tools checks GitHub Releases once a day and prepares a verified update in the background. The signed update runner validates SHA-256 and the pinned publisher, waits for Outlook to close, and retries the silent installer handoff when another maintenance worker is still finishing.

---

## Installation

1. Download `EmailTools_Setup.rar` from the [latest release](https://github.com/ParhamGhafouri/EmailTools/releases/latest/download/EmailTools_Setup.rar).
2. Extract the archive and run `EmailTools_Setup.exe`.
3. Start Outlook. The **Email Tools** ribbon tab appears, and the attachment buttons are added to the Home tab.

Already have Email Tools installed? **Do not uninstall it first.** Run the new installer over the existing version and setup upgrades it in place. Setup installs per-user, needs no administrator rights, and closes Outlook automatically if Outlook is running. To repair or remove Email Tools later, run `EmailTools_Setup.exe` again or uninstall it from **Settings → Apps**.

> On first start, Smart Archive may inspect existing archives, the local body index may begin building, and GAL synchronization may examine historical display names. These jobs share one maintenance lane, use bounded work units, and resume automatically after interruptions.

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
- Updates are accepted only when the installer hash and pinned code-signing identity match.
- Protected-message classification uses safe metadata and does not open encrypted bodies or enumerate Outlook attachments in the background.

---

## FAQ

**Does Smart Archive delete ordinary email?**
No. It moves eligible mail into an exact verified local archive destination. Protected folders such as Calendar, Contacts, Tasks, Notes, Drafts, Outbox, Deleted Items, and Conversation History are not archived. A legacy PST file is removed only after Email Tools proves recursively that no real mail remains.

**Does it need admin rights?**  
No. Email Tools installs under your own Windows account.

**Can I still search archived mail?**  
Yes. Seasonal archives remain mounted in Outlook and are searchable from Advanced Search.

**What does GAL synchronization change?**  
It updates recognized Outlook display names to the current name in your organization's Global Address List. It does not change email addresses, message bodies, attachments, or unknown recipients. Rules, views, and Search Folders are repaired only while visible Outlook is closed.

**Why does Email Tools build its own body index?**  
Because the feature was built for real support and audit work where "maybe Outlook indexed it" is not good enough. The local body index makes old messages, archived PSTs, and body-text searches behave consistently without uploading mailbox content anywhere.

**How does the first body-index build affect Outlook?**
The first build can take time on a large mailbox because it must read existing messages and archives. Email Tools performs this work in bounded background slices and yields when Outlook is active. Normal upgrades preserve a valid existing index instead of rebuilding it from zero.

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
