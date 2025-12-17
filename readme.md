# 🤖 AIO File Utility Bot — Zip 🗜️ / Unzip 📦 / Merge 🧩 / FTL 🔗 (Buttons-First)

An **all-in-one Telegram bot** that auto-detects what users send (archives vs normal files) and responds using a **single Session Panel** (buttons-first, minimal chat spam).

✅ 🗜️ Zip (auto-split for Telegram limits)  
✅ 📦 Unzip (single / multi-part / multiple archives)  
✅ 🧩 Merge (extract → combine → re-zip)  
✅ 🔐 Password support (extract protected archives + add/remove password on output)  
✅ 🔗 FTL (File-To-Link: direct download + stream links)

---

## ✨ Key UX: Session Panel (One Message, Always Updated)
Instead of spamming messages, the bot:

- creates **one panel message**
- **edits** it as files arrive
- finalizes when either:
  - user taps **✅ Done sending**, OR
  - an **inactivity window** (e.g. 2–3s) expires
- then shows the correct buttons based on what was detected

### Session Panel Detailed Examples for Understanding: 
<details> <summary> (Click to expand) </summary>

### 🧾 Session Panel — Textual UI Examples (Emojis)

> Below are **mock panels** showing how the bot’s **single edited Session Panel** message can look in each scenario.  
> Buttons are represented as `[🔘 Button]`.

---

### 🟦 0) Collecting phase (live updates while user is sending)

**🧾 Session Panel**
```text
📥 Receiving files…
📦 Archives: 0   📄 Files: 3
📊 Total size: 842 MB
⏳ Waiting for more… (auto-finish in 2s)
```

Buttons:  
[✅ Done sending] [🧾 List] [❌ Cancel]

---

### 📦 1) Single archive detected (1 file)

**🧾 Session Panel**
```text
📦 Archive detected: pack.zip
📊 Size: 1.6 GB   |   🔒 Password: Unknown

What do you want to do?
```

Buttons:  
[📂 Unzip] [🧾 List contents] [🎯 Extract selected]  
[🔐 Password] [⚙️ Settings] [❌ Cancel]

---

### 🔒 2) Protected archive → bot asks for password

**🧾 Session Panel**
```text
🔒 Protected archive detected: protected.zip
❗ Password required to extract.

Send the password now (as a message), or cancel.
```

Buttons:  
[🔐 Enter password] [❌ Cancel]

✅ After user sends password:

**🧾 Session Panel**
```text
🔐 Password received (session only)
📦 Extracting… 37%
```

Buttons:  
[❌ Cancel]

---

### 🔓 3) After extracting protected archive → remove/add password & send

**🧾 Session Panel**
```text
✅ Extracted successfully: protected.zip
🔐 Password used: Yes (session)

What next?
```

Buttons:  
[✅ Send extracted files]  
[🔓 Remove password & send] [🔐 Add password & send]  
[❌ Cancel]

---

### 📦📦 4) Multiple archives detected → choose handling mode

**🧾 Session Panel**
```text
📦 4 archives detected
📊 Total size: 5.8 GB

🧠 Detected pattern: 🧩 Parts of one archive (High confidence)
Choose how to proceed:
```

Buttons:  
[🧩 Parts Mode Unzip] [📦 Separate Unzip]  
[🧩 Merge → Rezip] [🧾 List] [❌ Cancel]

---

### 🧩 5) Parts Mode chosen → missing part check

✅ All parts present:

**🧾 Session Panel**
```text
🧩 Parts Mode selected
🔎 Checking parts…

✅ Found: 12/12 parts
Proceed to extract?
```

Buttons:  
[📂 Unzip now] [🧾 List contents] [❌ Cancel]

⚠️ Missing parts detected:

**🧾 Session Panel**
```text
🧩 Parts Mode selected
🔎 Checking parts…

⚠️ Missing parts detected
Found: 10/12 parts

Continue anyway (may fail) or cancel?
```

Buttons:  
[⚠️ Force unzip] [❌ Cancel]

---

### 📄 6) Non-archives detected → choose FTL or Zip

**🧾 Session Panel**
```text
📄 7 files detected (non-archive)
📊 Total size: 1.2 GB

Choose a mode:
```

Buttons:  
[🔗 Get Links (FTL)] [🗜 Make Archive]  
[🧾 List] [❌ Cancel]

---

### 🔗 7) FTL chosen → pick link type + paging

**🧾 Session Panel**
```text
🔗 FTL mode selected
📄 Files: 7

Choose link type:
```

Buttons:  
[🎬 Stream links] [⬇️ Direct links] [📋 Copy all] [❌ Cancel]

After generating (paged):

**🧾 Session Panel**
```text
✅ Links ready (Page 1/2)
1) file1.mp4   🎬 Stream | ⬇️ Direct
2) file2.mp4   🎬 Stream | ⬇️ Direct
3) file3.mp4   🎬 Stream | ⬇️ Direct
```

Buttons:  
[⏭ Next page] [📋 Copy all] [❌ Cancel]

---

### 🗜 8) Zip chosen → choose format, part size, password

**🧾 Session Panel**
```text
🗜 Zip mode selected
📄 Files: 12
📊 Total size: 6.4 GB

Choose archive format:
```

Buttons:  
[🗜 ZIP] [🧊 7Z] [⬅️ Back] [❌ Cancel]

Next:

**🧾 Session Panel**
```text
📦 Choose part size (Telegram-safe):
```

Buttons:  
[1900MiB ✅ Recommended] [1024MiB] [Custom ✍️] [⬅️ Back] [❌ Cancel]

Optional password:

**🧾 Session Panel**
```text
🔐 Add password to output archive?
(If you skip, archive will be unprotected.)
```

Buttons:  
[🔐 Add password] [🔓 Skip] [⬅️ Back] [❌ Cancel]

After starting:

**🧾 Session Panel**
```text
🗜 Creating archive… 41%
📦 Output will be split into parts if needed.
```

Buttons:  
[❌ Cancel]

</details>

---

## 🧠 Smart Detection (Auto + Override)
The bot classifies the batch into:

- 📦 **Archives only**
- 📄 **Non-archives only**
- 🧩 **Mixed** (archives + non-archives)

If multiple archives exist, it also tries to detect:

- 🧩 **Parts Mode** (split archive parts like `.001`, `.part1.rar`, `.z01`, etc.)
- 📦 **Separate Archives** (independent archives)

If detection is unsure, user can override via buttons:
- **Treat as Parts**
- **Treat as Separate**
- **Mixed options**

---

## 🧰 Features

### 🗜️ Zip
- ✅ Collect many files into one archive
- ✅ Auto-split output into multiple parts (Telegram-safe)
- ✅ Choose output: **ZIP / 7Z** (optional)
- ✅ Choose part size: **1900MiB / 1024MiB / Custom**
- ✅ Rename output via buttons or `/zipname`
- ✅ Optional: 🔐 **Add password** to output archive
- ✅ Cleanup after completion

### 📦 Unzip
- ✅ Unzip a single archive
- ✅ Unzip multi-part / split archives (**Parts Mode**)
- ✅ Unzip many independent archives (**Separate Mode**)
- ✅ List contents before extract 🧾
- ✅ Extract selected files 🎯

### 🔐 Password Support (Extraction + Output)
- ✅ **Protected archive detection**
- ✅ If protected, bot prompts: 🔐 “Send password”
- ✅ Password remembered **per session only**
- ✅ After extraction, user can optionally:
  - 🔓 **Remove password & send** (rezip unencrypted)
  - 🔐 **Add password & send** (rezip encrypted, if desired)

### 🧩 Merge / Re-Zip
For multiple archives in a batch:
- ✅ extract all → combine → re-zip into one archive
- ✅ choose output format + part size
- ✅ optional password on final output

### 🔗 FTL (File-To-Link)
- ✅ Generate **direct download** + **stream** links for sent files
- ✅ Paging for many files (avoids FloodWait spam)
- ✅ 📋 Copy all links

### 🧼 Reliability / Quality
- ✅ One active job per user (prevents collisions)
- ✅ Cancel anytime ❌
- ✅ Session TTL auto-expire (e.g. 30–60 min)
- ✅ Optional: disk-space guard, missing-part checks

---

## 📌 Commands (Minimal — Buttons First)
Most users can operate fully via buttons. Commands are just entry points.

### 🧾 General
- `/start` — show help + current session panel
- `/help` — quick usage
- `/commands` — list all commands
- `/cancel` — cancel current job/session

### 🗜️ Zip
- `/add` — start collecting files for zipping
- `/zip <name>` — create archive now (optional if using buttons)
- `/zipname <name>` — set default archive name for session
- `/zipclear` — clear collected files

### 📦 Unzip / 🔗 FTL (Optional entry points)
- `/unzip` — show unzip actions for current batch
- `/ftl` — show link generation actions

### 🖼️ Extras (Optional)
- `/addthumb` — set thumbnail (reply to a photo)
- `/delthumb` — remove thumbnail
- `/mode` — upload mode (Document / Video etc.)
- `/stats` — usage/admin stats

---

## 🧭 Workflows (Buttons-Only)

### 1) 📦 User sends **1 archive**
Bot shows:
- 📂 Unzip
- 🧾 List contents
- 🎯 Extract selected
- 🔐 Password (add/remove / prompt)
- ⚙️ Settings
- ❌ Cancel

### 2) 📦 User sends **multiple archives**
Bot asks:
- 🧩 Parts Mode Unzip (treat as one split archive)
- 📦 Separate Unzip (each archive independently)
- 🧩 Merge → Rezip
- 🧾 List
- ❌ Cancel

### 3) 📄 User sends **non-archive files**
Bot asks:
- 🔗 Get Links (FTL)
- 🗜️ Make Archive
- 🧾 Show list
- ❌ Cancel

### 4) 🧩 User sends **mixed files**
Bot asks:
- 📦 Archive actions
- 🔗 Links for non-archives
- 🗜️ Zip everything together
- 🧾 Show list
- ❌ Cancel

---

## 🗺️ Mermaid — Full Flow Diagram 

> ✅ Note: This flowchart explains the flow for easy understanding.
> - quoted node labels

```mermaid
flowchart TD
  A["👤 User starts sending files"] --> B["🧾 Session Panel created/updated"]
  B --> C{"⏳ Inactivity window<br/>or ✅ Done sending?"}
  C -->|"✅ Done / Timer ends"| D["🔎 Analyze batch"]

  D --> E{"📦 Archives only?"}
  D --> F{"📄 Non-archives only?"}
  D --> G{"🧩 Mixed batch?"}

  %% Archives only
  E --> H{"📦 How many archives?"}
  H -->|"1️⃣ One"| I["📦 Single Archive Menu<br/>📂 Unzip · 🧾 List · 🎯 Extract selected<br/>🔐 Password · ⚙️ Settings · ❌ Cancel"]
  H -->|"2️⃣+ Many"| J["📦 Multi-Archive Menu<br/>🧩 Parts Mode · 📦 Separate Unzip<br/>🧩 Merge → Rezip · 🧾 List · ❌ Cancel"]

  %% Non-archives only
  F --> K["📄 Non-Archive Menu<br/>🔗 Get Links (FTL) · 🗜 Make Archive<br/>🧾 List · ❌ Cancel"]

  %% Mixed
  G --> L["🧩 Mixed Menu<br/>📦 Archive actions · 🔗 Links for non-archives<br/>🗜 Zip everything · 🧾 List · ❌ Cancel"]

  %% Password extraction flow
  I --> M{"🔒 Protected archive?"}
  J --> M
  M -->|"Yes 🔐"| N["🔐 Ask user for password<br/>Store per session only"]
  N --> O["📦 Retry extraction"]
  M -->|"No ✅"| P["📤 Upload extracted files"]

  %% Remove password & send (optional step after successful extraction)
  P --> W{"🔓 Remove password & send?"}
  W -->|"Yes"| X["🗜 Rezip without password<br/>Send new archive (split if needed)"]
  W -->|"No"| Y["✅ Done"]

  %% Zip flow (split uploads)
  K --> Q{"🗜 Make Archive chosen?"}
  L --> Q
  Q --> R["⚙️ Choose format + part size<br/>ZIP/7Z · 1900MiB/Custom"]
  R --> S["🗜 Create archive"]
  S --> T["📤 Send parts<br/>part001 · part002 · ... ✅"]

  %% Add password to output archive (optional during zip settings)
  R --> Z{"🔐 Add password to archive?"}
  Z -->|"Yes"| ZA["🔐 Ask password input<br/>Encrypt output archive"]
  Z -->|"No"| ZB["🔓 No encryption"]

  %% FTL flow
  K --> U{"🔗 FTL chosen?"}
  L --> U
  U --> V["🔗 Generate Stream + Direct links<br/>📋 Copy All / Paging"]
