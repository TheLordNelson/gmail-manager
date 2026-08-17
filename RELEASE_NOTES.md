# Gmail Manager — Release Notes

**App URL:** https://thelordnelson.github.io/gmail-manager/gmail-manager.html  
**GitHub:** TheLordNelson/gmail-manager  

---

## v1.6 — Label Management in Reading Pane
*Current release*

### New Features
- **Label pills on open emails** — when reading an email, all current labels are shown as coloured pills below the subject line
- **📥 Inbox pill** — shows as a distinct green pill; tapping ✕ removes the email from Inbox (archives it)
- **⭐ Starred and ❗ Important** also shown as removable pills
- **＋ Add label** — dropdown to apply any user label to the open thread
- Smart confirmation warning when removing Inbox from an email with no other labels
- Label changes update instantly and refresh the thread list in the background

---

## v1.5 — Bulk Action Confirmation Modal

### New Features
- **Confirmation modal before all bulk actions** — shows a list of every affected email (sender + subject) before executing
- Actions: Mark Read, Mark Unread, Archive, Trash, Relabel
- Cancel button leaves selection intact; Confirm executes the action
- Nothing runs automatically — explicit confirmation required every time
- Relabel picker also routes through confirmation modal

---

## v1.4 — In-App Label Refresh

### New Features
- **🏷️ Run label refresh button** in sidebar footer
- Scans inbox for unlabelled emails via Gmail API
- Auto-applies all known label rules client-side instantly
- Unknown emails surface in a **review modal** — dropdown picker per email
- "Apply selected labels" commits all choices in one tap
- All known label rules embedded: News, Jobs Jenni, Bill, Finance, Shopping, Music, Family, Technology, Health, Work, Sailing, Workers Comp, Holiday Vietnam, Holiday, Pension UK - Aegon, Calendar event, TRASH rules (Carsales, AnyList, Pizza Riccardo, BlackVue, etc.)

---

## v1.3 — HTML Email Rendering & Pagination

### New Features
- **HTML emails rendered** in sandboxed iframes — images, formatting, and layout display correctly
- Iframes are fully isolated (no scripts, no same-origin access)
- Plain text fallback for text-only emails
- Auto-resize iframes to fit content (capped at 650px per message)
- **Load More button** — sticky at top of thread list, fetches next 50 threads
- Thread header shows "(more available)" when additional pages exist
- Pagination works across all views: All Inbox, Unread, label views, grouped view

### Bug Fixes
- Fixed flexbox `min-height:0` overflow causing reading pane to push past viewport
- Messages expand/collapse correctly including iframe resize on reveal

---

## v1.2 — Group Selection & Collapse Controls

### New Features
- **Group checkbox** — tick a group header to select all emails in that group at once; supports indeterminate state
- **⊟ Collapse All / ⊞ Expand All** buttons in grouped view toolbar
- Groups remember collapsed/expanded state while browsing
- Collapsed sidebar now shows a **☰ toggle button** to reopen it

### Bug Fixes
- Group checkbox `change` event used instead of `click` — fixes selection on all browsers
- Thread IDs stored on group element via `data-thread-ids` attribute — selection works even when group is collapsed
- `updateSel` reads from stored IDs rather than querying hidden DOM rows
- Action bar now appears correctly when selecting via group checkbox

---

## v1.1 — Grouped View & Reading Pane

### New Features
- **All by Label grouped view** — inbox threads grouped by their user label, each group collapsible
- **Reading pane** — click any email to open it alongside the thread list
  - Multi-message threads shown as collapsible cards (latest open by default)
  - Archive and Trash buttons directly in reading pane
  - Automatically marks thread as read on open
  - Mobile: reading pane opens full-screen with ← Back button
- **Unread view** — dedicated sidebar entry for unread inbox threads
- Label pills on thread rows in flat views
- Mark Unread added to bulk action bar

### Bug Fixes
- Collapsible sidebar with persistent toggle
- Bulk action refresh delay increased to 1.5s to allow Gmail server to update

---

## v1.0 — Initial Release

### Features
- Google OAuth sign-in (implicit flow, token stored in localStorage)
- Collapsible sidebar with all user labels + system views (Inbox, Starred, Important)
- Thread list with unread indicators, sender, subject, snippet, date
- 50 threads per view via Gmail API
- Bulk actions: Mark Read, Archive, Trash, Relabel
- Select individual threads or all threads
- Stays signed in between sessions
- Hosted on GitHub Pages — no server required

### Technical
- Single HTML file — pure HTML/CSS/JS, no build step
- Gmail API calls direct from browser using OAuth bearer token
- OAuth redirect URI: `https://thelordnelson.github.io/gmail-manager/gmail-manager.html`
- Google Cloud Project: `savvy-factor-499307-q0`

---

## Known Limitations

- Maximum 50 threads loaded per page (Gmail API limit); use Load More for additional threads
- OAuth token expires after 1 hour — app will prompt to sign in again
- Gmail API `gmail.modify` scope requires the app to be listed as "In Production" or user added as a test user in Google Cloud Console
- HTML email rendering is read-only — no scripts execute inside emails
- Reply functionality not yet implemented
