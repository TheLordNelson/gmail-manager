# Claude Prompt — Gmail Manager Project

## Project Overview

I am building and maintaining a standalone Gmail management web app hosted on GitHub Pages. Claude has direct Gmail access via MCP and helps with both inbox labelling (via MCP) and iterative development of the app (via code generation).

---

## App Details

- **Live URL:** `https://thelordnelson.github.io/gmail-manager/gmail-manager.html`
- **GitHub:** `TheLordNelson/gmail-manager`
- **Google Cloud Project:** `savvy-factor-499307-q0`
- **OAuth Client ID:** `1090553100312-ls5st7kedh3h07l1tofbcn3b7epec2h4.apps.googleusercontent.com`
- **OAuth Redirect URI:** `https://thelordnelson.github.io/gmail-manager/gmail-manager.html`
- **Gmail account:** `2ian.nelson@gmail.com`
- **Test Gmail account:** `2emaleme@gmail.com`

---

## Gmail Label System

| Label Name | Label ID |
|---|---|
| News | Label_2463225475707470174 |
| Jobs Jenni | Label_805230922777097013 |
| Holiday Vietnam | Label_791703868379029115 |
| Holiday | Label_5422643364044618323 |
| Shopping | Label_1063679665430947125 |
| Music | Label_7378421052090047179 |
| Family | Label_1996254530682183484 |
| Bill | Label_6035990152513784074 |
| Finance | Label_35 |
| Technology | Label_3069034851973135286 |
| Health | Label_7323047852552588863 |
| Work | Label_9047548254714955279 |
| Sailing | Label_14 |
| Workers Comp | Label_5307757318324514926 |
| Pension UK - Aegon | Label_585759915115591443 |
| Calendar event | Label_7861096440641771906 |
| Friends | Label_3638975555762862381 |
| House Hunting | Label_377076489294141763 |

---

## Label Rules (Auto-apply via MCP or in-app refresh)

| Sender / Pattern | Label |
|---|---|
| googlenews-noreply@google.com | News |
| newsletter.afr.com | News |
| Beyond the Gantt / Substack | News |
| theguardian.com | News |
| seek.com.au / jobmail@s.seek | Jobs Jenni |
| immigration.gov.vn / vnpay | Holiday Vietnam |
| thredbo / covermore / qantas.com.au / americanairlines / airbnb | Holiday |
| amazon.com.au / woolworths / eufy / anker / ebay / chemistwarehouse | Shopping |
| Moonpig (non-family reminders e.g. Betty Briant) | Shopping |
| Moonpig (family e.g. Charlotte, Jenni) | Family |
| bandsintown / tegdainty / boneym / deep purple / farnham / trucksales | Music |
| charlottenelson | Family |
| optus / latitude / linkt / service.nsw / transport.nsw / revenue.nsw | Bill |
| nab@ / clearscore / macquarie / lloyds / smartmonday / quinn | Finance |
| walkerlawgroup | Workers Comp |
| claude.ai / anthropic / openai / surfshark / iphonelife / nrl.com / seapeopleapp / no-reply@accounts.google.com | Technology |
| health.nsw / specsavers / hotdoc / psychiatr | Health |
| planview | Work |
| making waves / orc sail | Sailing |
| aegon | Pension UK - Aegon |
| calendar-notification@google.com | Calendar event |
| carsales / blackvue / joblistify / anylist / pizzariccardo | TRASH |
| AnyList newsletters | TRASH |
| Pizza Riccardo promos | TRASH |

---

## Key Behaviours & Preferences

### Label Refresh (MCP)
- Scan inbox with `in:inbox has:nouserlabels`
- Auto-apply all known rules immediately
- For unknowns: present options as buttons (one per thread) — never auto-apply guesses
- Always show Yes / Later option at end of each batch
- Add unknown rule decisions to memory for future sessions

### Bulk Actions (App)
- **Always show a confirmation modal** listing affected emails before executing any bulk action
- Never execute bulk actions automatically — user must explicitly confirm
- After bulk action, wait 1.5 seconds before refreshing to allow Gmail server to update

### App Development
- When modifying the app, always ask the user to upload the current working `gmail-manager.html` first
- Make surgical changes only — never rewrite auth code or OAuth redirect URI
- OAuth redirect URI is permanently: `https://thelordnelson.github.io/gmail-manager/gmail-manager.html`
- Test users in Google Cloud Console: `2ian.nelson@gmail.com`, `2emaleme@gmail.com`
- After changes, provide the file for download and remind user to upload to GitHub

### Code Safety Rules
- Never change the `REDIRECT_URI` constant or the `href` on the sign-in anchor tag
- Never change `window.onload` token parsing logic unless specifically asked
- Always copy the uploaded working file before making changes — never modify from memory
- Present changes as a numbered list of exactly what was modified

---

## MCP Gmail Search Patterns

```
in:inbox has:nouserlabels          → unlabelled inbox threads
in:inbox label:LabelName           → threads with a specific label
in:inbox is:unread                 → unread inbox threads
```

- Label operations require label IDs (not names)
- Trashing via MCP: pass `['TRASH']` as labelIds to `Gmail:label_thread`
- Bulk label applications across 40–50 threads work reliably in parallel
- Post-action refresh delay: ~1–1.5 seconds

---

## App Feature Set (Current)

1. Sign in with Google (OAuth implicit flow, stored in localStorage)
2. Sidebar with collapsible navigation — views + all user labels
3. Views: All Inbox, All by Label (grouped), Unread
4. Grouped view: collapsible label groups, group checkbox selection, collapse/expand all
5. Thread list with unread indicators, sender, subject, snippet, date
6. Pagination via Load More button (sticky, top of list)
7. Reading pane: renders HTML emails in sandboxed iframes, collapsible message cards
8. Label pills on open email: add or remove any label including 📥 Inbox
9. Bulk actions with confirmation modal: Mark Read, Mark Unread, Archive, Trash, Relabel
10. In-app Label Refresh: scans for unlabelled emails, auto-applies rules, review modal for unknowns
11. Refresh labels sidebar button
12. Sign out

---

## Deployment

- Hosted on GitHub Pages (free, permanent)
- Upload `gmail-manager.html` to `https://github.com/TheLordNelson/gmail-manager`
- Changes go live within ~60 seconds of commit
- No build step — pure HTML/CSS/JS single file
