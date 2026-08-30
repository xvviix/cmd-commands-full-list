# 📘 The Complete Windows Command-Line Master Reference

**CMD + PowerShell · every command · every subcommand · full step-by-step tutorials**

> **Expanded edition.** This reference now covers the complete built-in command set of Windows 10/11, full subcommand tables for every compound tool (`diskpart`, `netsh`, `net`, `sc`, `schtasks`, `reg`, `DISM`, `powercfg`, `wevtutil`, `certutil`, `ftp`, `nslookup`, `w32tm`, `bcdedit`, `vssadmin`, `wbadmin`, `bitsadmin`, `winget`…), a beginner course, 10 hands-on tutorials, and 7 quick-reference appendices.
>
> Conventions used throughout: `command` = type it exactly as shown · `⟨required⟩` · `[optional]` · `a|b` = choose one · ⚠ = **destructive, use with care** · † = deprecated (modern replacement given) · *Admin* = run from an elevated prompt.

---

## Table of Contents

**PART 0 — Getting Started (Beginner Course)**
0.1 CMD vs PowerShell vs Windows Terminal · 0.2 Every way to open a shell · 0.3 Running as Administrator · 0.4 Syntax, wildcards & quoting · 0.5 Operators & redirection · 0.6 Getting help anywhere · 0.7 Keyboard shortcuts · 0.8 Safe practice lab · 0.9 Your first 10 commands

**PART 1 — Command Prompt: The Complete Command Set**
1. Navigation & directory listing · 2. File & folder create/copy/move/delete · 3. Copy tools deep-dive (`copy`, `xcopy`, `robocopy` — all flags + exit codes) · 4. Viewing, searching & comparing text · 5. Attributes, permissions & ownership (`attrib`, `icacls`, `takeown`) · 6. Links, compression & cabinets (`mklink`, `compact`, `makecab`, `expand`, `tar`) · 7. System information & environment · 8. `wmic` — full alias & verb reference † · 9. Disks & file systems (`chkdsk`, `format`, `defrag`, `label`, `mountvol`, `subst`, `convert`) · 10. `diskpart` — every subcommand · 11. `fsutil` — subcommand reference · 12. Encryption & wiping (`cipher`)

13. Networking core (`ipconfig`, `ping`, `tracert`, `pathping`, `nslookup`, `netstat`, `arp`, `route`, `nbtstat`, `getmac`, `curl`, `ssh`, `telnet`) · 14. `netsh` — contexts & subcommands (wlan, advfirewall, interface, portproxy, winsock, trace, http) · 15. `net` — every subcommand (`user`, `localgroup`, `use`, `share`, `session`, `accounts`, `time`, `statistics`, `helpmsg`…)

16. Process & task management (`tasklist`, `taskkill`, `start`, `timeout`, `waitfor`, `msg`) · 17. `schtasks` — every subcommand · 18. `sc` — every subcommand · 19. Users, groups & security (`runas`, `auditpol`, `secedit`, `cmdkey`, `logoff`)

20. Registry (`reg` — every operation, `regedit`, `regini`) · 21. Maintenance & recovery (`sfc`, `DISM` all subcommands, `bcdedit`, `bcdboot`, `bootrec`, `reagentc`, `wbadmin`, `vssadmin`, `verifier`, `cleanmgr`, `gpupdate`, `gpresult`, `manage-bde`, `openfiles`) · 22. Shutdown & power (`shutdown` all switches, `powercfg` all subcommands) · 23. Event logs (`wevtutil`, `eventcreate`) · 24. Performance & logging (`logman`, `typeperf`, `relog`, `tracerpt`) · 25. Remote Desktop / Terminal Services (`qwinsta`, `quser`, `tscon`, `tsdiscon`, `tskill`, `mstsc`…) · 26. Certificates (`certutil`) · 27. Transfers (`bitsadmin`, `ftp` — all subcommands, `tftp`) · 28. Time (`w32tm`, `tzutil`) · 29. Software deployment (`msiexec`, `pnputil`, `regsvr32`, `cscript`) · 30. Console & environment (`set`, `setx`, `path`, `prompt`, `title`, `color`, `chcp`, `mode`, `doskey`, `clip`, `assoc`, `ftype`, `where`, `forfiles`, `choice`, `sort`) · 31. GUI tools launched from CMD (full `.msc`/`.cpl` table)

**PART 2 — PowerShell: The Complete Cmdlet Set**
P1. PowerShell crash course (objects, pipeline, discovery) · P2. File system cmdlets · P3. Text & data (CSV/JSON/XML/HTML) · P4. Objects, pipeline & formatting · P5. System info & hardware · P6. Processes, services & scheduled tasks · P7. Networking & firewall · P8. Storage & SMB shares · P9. Users, security & credentials · P10. Registry · P11. Remoting & background jobs · P12. Modules & packages (incl. `winget` — every subcommand) · P13. Maintenance & power · P14. Scripting tutorial — zero to advanced

**PART 3 — Hands-On Tutorials (T1–T10)**
T1 CMD basics — your first hour · T2 File-management mastery · T3 Write a real batch backup script · T4 Network troubleshooting walkthrough · T5 `diskpart` — format a USB drive & change letters · T6 Automate anything with Task Scheduler · T7 Repair a broken Windows boot · T8 PowerShell — build a system report script · T9 Security hardening in 15 commands · T10 Managing another PC remotely

**PART 4 — Appendices**
A. Master A–Z command index · B. Environment variables reference · C. Exit-code tables (`robocopy`, `xcopy`, `msiexec`, ERRORLEVEL patterns) · D. CMD ↔ PowerShell ↔ Linux equivalents · E. Keyboard shortcuts · F. Run (Win+R) launcher list · G. Common errors & quick fixes + safety checklist

---
---

# PART 0 — GETTING STARTED (Beginner Course)

## 0.1 CMD vs PowerShell vs Windows Terminal

| Shell | What it is | Best for | Scripts |
|---|---|---|---|
| **Command Prompt (cmd.exe)** | Legacy text shell inherited from MS-DOS. Commands output plain text. | Quick file ops, `net`/`netsh`/`sc` tools, legacy systems, `.bat` automation | `.bat` / `.cmd` batch files |
| **Windows PowerShell (powershell.exe, v5.1)** | Object-based shell built on .NET. Commands pass **objects**, not text. | Windows administration, automation, reporting | `.ps1` scripts |
| **PowerShell 7+ (pwsh.exe)** | Modern cross-platform successor, installed side-by-side via `winget install Microsoft.PowerShell`. | Same as above + Linux/macOS, newer language features | `.ps1` |
| **Windows Terminal (wt.exe)** | A modern *tabbed window* that hosts any of the above shells. Not a shell itself. | Comfortable day-to-day use | — |

Rules of thumb:
- Almost **every CMD command also works inside PowerShell** (it calls the real `.exe`), but PowerShell cmdlets do *not* work inside CMD unless prefixed: `powershell -Command "..."` or `pwsh -Command "..."`.
- CMD commands and PowerShell cmdlets differ the most in **copying/deleting**, where PowerShell adds `-Recurse`, `-Force`, `-WhatIf` safety.
- Learn CMD first for fundamentals (paths, wildcards, networking tools) — those habits transfer everywhere.

## 0.2 Every way to open a shell

| Method | How |
|---|---|
| Start menu | Press ⊞, type `cmd` or `powershell` or `terminal`, press ⏎ |
| Run dialog | ⊞+R → `cmd` ⏎ (or `powershell`, `wt`) |
| Power-user menu | ⊞+X → *Terminal* or *Terminal (Admin)* |
| From Explorer | Type `cmd` in the address bar of any folder ⏎ — opens CMD already inside that folder |
| Right-click | Shift+right-click in a folder → *Open in Terminal* / *Open PowerShell window here* |
| Task Manager | Ctrl+Shift+Esc → File → *Run new task* → `cmd`, tick *Create this task with administrative privileges* |
| From inside CMD | `start powershell` opens a PowerShell window; `start cmd` a new CMD one |
| One command, keep window | `cmd /k command` runs *command* then stays open; `cmd /c command` closes after |

## 0.3 Running as Administrator (elevation)

Many commands touch machine-wide state and will fail with *Access denied* unless elevated. The reliable ones to remember: `chkdsk /f`, `sfc`, `DISM`, `diskpart`, `format`, `net user /add`, `reg` writes to `HKLM`, `sc create/config`, `shutdown /m`, `route add`, `powercfg /h`, firewall changes, `defrag`, `takeown` on system files.

- Open elevated: ⊞ → type `cmd` → **Ctrl+Shift+⏎** (works in the Start menu for any app).
- From a normal prompt: `powershell -Command "Start-Process cmd -Verb RunAs"` spawns an elevated CMD.
- **Check whether your current window is elevated:**

```cmd
net session >nul 2>&1 && echo ELEVATED (Admin) || echo NOT elevated
openfiles >nul 2>&1 && echo Admin || echo Normal user
```

An elevated prompt usually shows `Administrator: ...` in its title bar.

## 0.4 Syntax, wildcards & quoting

| Concept | Example | Notes |
|---|---|---|
| Wildcards | `*.txt`, `file?.log`, `a*b.*` | `*` = any characters, `?` = exactly one. Work with most CMD file commands |
| Case | `DIR` = `dir` = `Dir` | CMD and PowerShell are case-**insensitive** for commands and paths |
| Spaces in paths | `cd "C:\Program Files"` | Always quote paths containing spaces |
| Escape character | `\|`, `^&`, `^\|`, `^>` | `^` escapes the next character in CMD |
| Percent variables | `echo %USERNAME%` | See Appendix B for the full variable list |
| Multiple commands | `cls & dir` (always both), `dir && echo OK` (2nd only if 1st succeeds), `dir \|\| echo FAILED` (2nd only if 1st fails) | `&`, `&&`, `\|\|` are CMD's command separators |
| Long paths >260 chars | `\\?\C:\very\long\path` | Prefix bypasses MAX_PATH for tools that support it |
| Current directory shorthand | `.\file.txt`, `..\..` | A single dot = here, two dots = parent |
| UNC paths | `\\server\share\folder` | CMD can't `cd` into these directly — use `pushd`, which maps a temporary drive letter automatically |

## 0.5 Operators & redirection (the complete table)

| Operator | Meaning |
|---|---|
| `>` | Redirect stdout to file, **overwrite** (`dir > list.txt`) |
| `>>` | Redirect stdout to file, **append** |
| `<` | Feed a file into a command's stdin (`sort < unsorted.txt`) |
| `2>` | Redirect only **errors** (`command 2> err.log`) |
| `2>>` | Append only errors |
| `>file 2>&1` | Capture normal output **and** errors into one file |
| `>nul 2>&1` | Throw everything away (used to test success silently) |
| `\|` | **Pipe** stdout of one command into another (`dir \| find ".txt"`) |
| `&` | Run next command regardless of previous result |
| `&&` | Run next command only if the previous **succeeded** |
| `\|\|` | Run next command only if the previous **failed** |
| `^` | Escape/continue character; `^` at end of line continues a long command on the next line |
| `%var%` | Expand a variable (at parse time) |
| `!var!` | Delayed expansion — inside loops; needs `setlocal enabledelayedexpansion` |

## 0.6 Getting help anywhere (the three help systems)

| Where | Command | Notes |
|---|---|---|
| CMD | `help` | Lists all CMD internal commands |
| CMD | `command /?` | Full syntax + every switch for *any* command — this is the single most useful habit (`robocopy /?`, `netsh /?`) |
| CMD | `help x` | Same as `x /?` for internal commands |
| PowerShell | `Get-Help Get-Process` | Help for a cmdlet |
| PowerShell | `Get-Help Get-Process -Examples` / `-Full` / `-Detailed` | Increasing depth |
| PowerShell | `Get-Help Get-Process -Online` | Opens official Microsoft docs in browser |
| PowerShell | `Update-Help` | Downloads current help files (Admin, once per session-ish) |
| Anything | Microsoft Learn → “Windows commands” reference | The official complete A–Z |

## 0.7 Keyboard shortcuts

**Command Prompt**

| Key | Action |
|---|---|
| F1 | Type the previous command one character at a time |
| F2 + char | Retype previous command up to *char* |
| F3 | Complete previous command entirely |
| F4 + char | Delete from cursor to *char* |
| F5 / F8 | Cycle back / matching-cycle through history |
| F7 | Popup list of command history |
| F9 + number | Re-run history entry *n* |
| ↑ / ↓ | Move through history |
| Ctrl+C | Abort current command / clear line |
| Ctrl+Home/End | Delete to start/end of line (Win10+) |
| Page Up/Down | Insert first/last command of the session |
| Esc | Clear current line |
| Tab | Path completion (cycles matches) |

**PowerShell (PSReadLine)**

| Key | Action |
|---|---|
| Tab / Shift+Tab | Complete parameter, path, cmdlet, value (cycles backwards with Shift) |
| Ctrl+Space | Show *all* completions in a menu |
| Ctrl+R | Reverse incremental search through history |
| ↑ / ↓ | History |
| Ctrl+Left/Right | Word-jump on the line |
| Ctrl+A / Ctrl+E | Jump to start / end of line |
| Ctrl+K / Ctrl+U | Delete to end / to start of line |
| Ctrl+W | Delete word left |
| Alt+. | Insert last token of the previous command (like bash `!$`) |
| F8 | History matching current text |
| F2 | Toggle prediction view (history-based suggestions, PSReadLine 2.1+) |

## 0.8 Safe practice lab — before you run anything destructive

1. Create a sandbox: `mkdir C:\Lab` and `cd C:\Lab`. Practice everything there first.
2. The commands that can destroy data quickly: ⚠ `del /s /q`, `rd /s /q`, `format`, `diskpart` (`clean`), `robocopy /mir` (deletes extras in the destination!), `cipher /w`, `reg delete`, `bcdedit`, `shutdown`. Never run these casually, and double-check the target path/drive letter.
3. Prefer test runs: robocopy's `/l` (list-only) flag, PowerShell's `-WhatIf` on destructive cmdlets.
4. Best practice environment: a VM (Hyper-V, VirtualBox) or Windows Sandbox (Pro: ⊞R → `windows-sandbox`) — reset with one click.
5. Before deleting/moving lots of files, run the same command with `echo` in front first to preview what it would touch.

## 0.9 Your first 10 commands (quickstart)

```cmd
:: 1. go to your Desktop
cd %USERPROFILE%\Desktop
:: 2. create a file containing one line
echo Hello > hello.txt
:: 3. see it listed
dir
:: 4. print its contents
type hello.txt
:: 5. duplicate it
copy hello.txt hello2.txt
:: 6. rename the copy
ren hello2.txt backup.txt
:: 7. create a folder
mkdir Test
:: 8. move the file into it
move backup.txt Test\
:: 9. view the structure you built
tree /f
:: 10. clean up
del Test\backup.txt
rd Test
```

Notes: `:: text` marks a comment (never inside a parenthesized block — use `rem` there). Each line above teaches one operation you'll use daily. Everything else in this book is variation on these verbs: **go, look, create, copy, rename, move, delete**.

---
---

# PART 1 — COMMAND PROMPT: THE COMPLETE COMMAND SET

## 1. Navigation & Directory Listing

### `dir` — every switch

| Form | What it does |
|---|---|
| `dir` | Lists current folder |
| `dir C:\Windows` | Lists an absolute path |
| `dir /a` | All entries **including hidden + system** |
| `dir /a:h` | Only hidden (`:d` dirs, `:s` system, `:r` read-only, `:a` ready-for-archive, `-` negates, e.g. `/a:-d` = files only) |
| `dir /b` | Bare list — names only (ideal for scripts/loops) |
| `dir /s` | Recursive through all subfolders |
| `dir /s /b *.log` | Recursive **and** bare — full paths, one per line (classic file finder) |
| `dir /o:n` | Sort by name — `/o:s` size, `/o:d` date, `/o:e` extension, `/o:g` folders-first; prefix `-` to reverse (`/o:-s` largest first) |
| `dir /t:c` | Which timestamp to use: `c` created, `a` last access, `w` last written (default) |
| `dir /w` / `dir /d` | Wide format / wide format sorted by column |
| `dir /p` | Pause after each screen |
| `dir /q` | Show **file owner** (NTFS) |
| `dir /c` / `dir /-c` | Show/hide thousand separators in sizes |
| `dir /x` | Show 8.3 short names (why `PROGRA~1` = `C:\Program Files`) |
| `dir /l` | Lowercase output |
| `dir /r` | Show NTFS alternate data streams (`file.txt:Zone.Identifier`) |
| `dir /4` | Four-digit years |
| `dir C:\ *.log /s /b` | Combine: path, mask, recursion, bare |

### `cd` / `chdir`, drives, and the directory stack

| Command | Explanation |
|---|---|
| `cd` | Print current directory |
| `cd folder` / `cd C:\path` | Change directory (quote paths with spaces) |
| `cd ..` | Up one level (repeatable: `cd ..\..`) |
| `cd \` | Jump to root of current drive |
| `cd /d D:\data` | Change **drive and directory** in one step (without `/d`, `cd` can't cross drives) |
| `D:` | Switch to drive D:, keeping its last-known directory |
| `pushd C:\deep\nested\path` | Save current dir on a stack, then move |
| `pushd \\server\share` | ⭐ CMD trick: automatically maps a temp drive letter (Z:) to a UNC path and cd's into it |
| `popd` | Return to the last `pushd`-saved location (and unmaps the temp drive) |
| `tree` | Folder tree (folders only) |
| `tree /f` | Tree **with files** |
| `tree /a` | Use ASCII characters instead of line-drawing |
| `cd -` | ✗ Not in CMD (that's PowerShell/Linux) — use `pushd`/`popd` |

## 2. File & Folder Create / Copy / Move / Delete

### Creating & writing

| Command | Explanation |
|---|---|
| `md folder` / `mkdir folder` | Create folder (both names identical) |
| `md one\two\three` | Create nested path in one shot |
| `echo text > file.txt` | Create/overwrite a file with one line |
| `echo more >> file.txt` | Append a line |
| `copy con file.txt` … Ctrl+Z ⏎ | Type a file live in the console (retro but works) |
| `type nul > empty.txt` | Create an empty file (or `break > empty.txt`) |
| `fsutil file createnew big.bin 1048576` | Create a file of an exact size in bytes (zero-filled) |

### `copy`

| Form | Explanation |
|---|---|
| `copy a.txt D:\` | Copy one file |
| `copy *.txt D:\Backup\` | Copy by wildcard |
| `copy a.txt+b.txt+c.txt all.txt` | Concatenate files |
| `copy /y` | Overwrite without prompting |
| `copy /-y` | Force prompting (useful in scripts) |
| `copy /v` | Verify after copy |
| `copy /b file` | Binary mode (prevents Ctrl+Z truncation) |
| `copy /d` | Only copy if source is newer (poor-man's sync) |
| `copy /l` | List what would be copied — no action |
| `copy file \\server\share` | Copy to network share |
| `xcopy`, `robocopy` | Use these for folders — see §3 |

### `move`, `ren`, `del`, `rd`

| Command | Explanation |
|---|---|
| `move file D:\dest\` | Move file |
| `move /y` | Move/overwrite without prompt |
| `move folder D:\dest\` | Move whole folder (same volume = instant rename) |
| `ren old.txt new.txt` | Rename (never accepts a destination path — same folder only) |
| `ren *.txt *.bak` | Bulk rename extension |
| `del file` / `erase file` | Delete file (identical twins) |
| ⚠ `del /f /s /q *.tmp` | Force + recursive + no-prompt delete of matches |
| `del /p` | Prompt per file (safe) |
| `del /a:h` | Delete by attribute (h hidden, r read-only needs `/f`, s system) |
| ⚠ `rd folder` / `rmdir folder` | Remove **empty** folder |
| ⚠ `rd /s /q folder` | Remove folder tree silently — triple-check the name |
| `tree /f > list.txt` before deleting | Good habit: snapshot what exists first |

### `type`, `more`, `print`

| Command | Explanation |
|---|---|
| `type file.txt` | Print file to screen (text only) |
| `type a.txt b.txt` | Print several files in sequence |
| `more file.txt` | Page through a file (Space = next page, Q = quit) |
| `more +100 file.txt` | Start at line 100 |
| `more /s` | Squeeze repeated blank lines |
| `print file.txt` | Send to the default LPT printer (legacy) |
| `clip < file.txt` | Put file contents on the clipboard |
| `type file.txt \| more` | Pipe long output through the pager |

### `replace` & `recover` (the forgotten two)

| Command | Explanation |
|---|---|
| `replace src.* D:\dest` | Copies src over **existing same-name files only** |
| `replace /s` | Include subfolders of destination |
| `replace /u` | Only replace if source is newer |
| `recover badfile` | Reads a file from a bad disk sector-by-sector, salvaging readable data |

## 3. Copy Tools Deep-Dive — `xcopy` & `robocopy` (all flags)

### `xcopy` — every switch

| Flag | Meaning |
|---|---|
| `/s` | Copy folders + subfolders (skip empty ones) |
| `/e` | Copy subfolders **including empty ones** |
| `/t` | Create folder tree only (no files) |
| `/u` | Copy only files that already exist at destination |
| `/i` | If destination missing, assume it's a folder (avoids the “file or directory?” prompt) |
| `/y` / `/-y` | Suppress / force overwrite prompt |
| `/c` | Continue after errors |
| `/q` | Quiet — don't echo filenames |
| `/f` | Show full source & destination paths |
| `/l` | List only — **dry run** |
| `/g` | Allow copying to destination with encrypted (EFS) support |
| `/h` | Include hidden + system files |
| `/r` | Overwrite read-only files |
| `/k` | Copy attributes (otherwise resets read-only) |
| `/o` | Copy ACL + owner info |
| `/x` | Copy audit settings (implies `/o`) |
| `/n` | Copy using short (8.3) names |
| `/a` | Copy only files with archive attribute set |
| `/m` | Like `/a` but resets the archive attribute (incremental backups) |
| `/d:[date]` | Copy only files changed on/after date (`/d:` alone = only newer than destination) |
| `/exclude:file.lst` | Skip paths containing strings listed in file.lst |
| `/w` `/p` | Prompt before starting / before each file |
| `/z` | Restartable mode for unstable networks |
| `/b` | Backup mode (uses Backup privilege — bypasses some permission issues) |
| `/j` | Unbuffered I/O — much faster for very large files |
| `/e /h /k /o /x` combined | “Full fidelity” copy |

**xcopy exit codes:** `0` OK · `1` no files found · `2` aborted by user · `4` init failure (memory/privilege) · `5` disk write error.

### `robocopy` — the professional's copy tool (all flag groups)

Exit codes: `0` nothing copied · `1` files copied · `2` extra files at destination · `3` = 1+2 · `4` mismatches · `5`–`7` combinations incl. copies · `8` **some files failed** · `16` **fatal error**. Test with `if %errorlevel% GEQ 8` → failure.

**Copy options**

| Flag | Meaning |
|---|---|
| `/s` | Subfolders (skip empty) |
| `/e` | Subfolders incl. empty |
| `/lev:n` | Only first *n* levels of the tree |
| `/z` | Restartable mode (resumes after network drop; slower) |
| `/b` | Backup mode (Admin — bypasses ACL denials) |
| `/zb` | Restartable, fall back to backup mode |
| `/j` | Unbuffered I/O (big files) |
| `/efsraw` | Copy encrypted (EFS) files in raw mode |
| `/copy:DATSOU` | What to copy: **D**ata, **A**ttributes, **T**imestamps, **S**ecurity (ACLs), **O**wner, **U**auditing. Default = DAT |
| `/dcopy:T` | Copy directory timestamps too |
| `/sec` | = `/copy:DATS` |
| `/copyall` | = `/copy:DATSOU` |
| `/nocopy` | Copy nothing (use with `/purge`/`/timfix` to fix metadata only) |
| `/secfix` | Fix security on all files, even skipped ones |
| `/timfix` | Fix timestamps on all files, even skipped |
| ⚠ `/purge` | Delete destination files/dirs that no longer exist at source |
| ⚠ `/mir` | **Mirror** = `/e` + `/purge` — destination becomes exact copy (deletes extras!) |
| `/mov` | Move: delete source files after copy |
| `/move` | Move: delete files *and dirs* after copy |
| `/a+:[RASHCNETO]` | Add attributes to copied files (e.g. `/a+:R` = mark read-only) |
| `/a-:[RASHCNETO]` | Remove attributes |
| `/create` | Create tree + zero-length files only (skeleton) |
| `/fat` | Use 8.3 FAT names |
| `/256` | Turn off long-path (>256) support |
| `/mon:n` | Re-run when ≥ n changes detected (watch mode) |
| `/mot:m` | Re-run every m minutes (monitor mode) |
| `/rh:hhmm-hhmm` | Run only in this time window |
| `/pf` | Check run-hours per file, not per copy |
| `/ipg:n` | Pace packets (n ms gap) for slow WAN links |
| `/sl` | Follow symbolic links as links (copy the link itself) |
| `/mt[:n]` | Multithreaded — default 8 threads, max 128. Huge speedup for many small files |
| `/nodcopy` | Don't copy directory info |
| `/nooffload` | Don't use Windows copy-offload mechanism |

**File-selection options**

| Flag | Meaning |
|---|---|
| `/a` | Only files with archive attribute set |
| `/xa:[attr]` | Exclude files with given attributes |
| `/xf file1 file2 *.tmp` | Exclude files/masks |
| `/xd dir1 "C:\big folder"` | Exclude directories |
| `/xc` `/xn` `/xo` | Exclude **c**hanged / **n**ewer / **o**lder files |
| `/is` | Include same files (default: skipped) |
| `/it` | Include tweaked files |
| `/max:n` `/min:n` | File size ceiling/floor in bytes |
| `/maxage:n` `/minage:n` | Max/min age: days, or `YYYYMMDD` date. `/maxage:7` = only files newer than 7 days |
| `/maxlad:date` `/minlad:date` | Same but by last-**access** date |
| `/fft` | Assume FAT timestamps (2s granularity) — fixes “everything gets re-copied” on NAS drives |
| `/fat` | Create FAT-style names |

**Retry options**

| Flag | Meaning |
|---|---|
| `/r:n` | Retries per file — **default is 1,000,000!** Set `/r:1` or `/r:3` in scripts |
| `/w:n` | Wait n seconds between retries (default 30 → set `/w:1`) |
| `/reg` | Save `/r` and `/w` as defaults in the registry |

**Logging options**

| Flag | Meaning |
|---|---|
| `/l` | **List only — dry run, copies nothing. Always preview `/mir` with this first!** |
| `/x` | Report extra files (not just copied ones) |
| `/v` | Verbose (skip lines) |
| `/ts` | Include full timestamps |
| `/fp` | Include full paths |
| `/ns` `/nc` `/nfl` `/ndl` | Suppress size / class / **file-list** / **dir-list** lines (faster logs) |
| `/np` | No progress percentage (essential when logging) |
| `/eta` | Show estimated arrival times |
| `/log:file` | Write log (overwrite) |
| `/log+:file` | Append log |
| `/unilog:file` `/unilog+:file` | Unicode log |
| `/tee` | Log **and** show on screen |
| `/njh` | No job header |
| `/njs` | No job summary |
| `/unicode` | Unicode status output |

**Job files**

| Flag | Meaning |
|---|---|
| `/job:jobname` | Run with parameters from a .rcj job file |
| `/save:jobname` | Save current parameters as a job file |

**Recipes**

```bat
robocopy C:\Data D:\Mirror /mir /mt:16 /r:1 /w:1 /log:sync.log /np /tee
robocopy C:\Data \\NAS\Backup /e /maxage:1 /r:1 /w:1        :: daily incremental
robocopy C:\Src D:\Dst /e /xf *.tmp *.log /xd node_modules   :: selective
robocopy C:\Src D:\Dst /e /l /ns /nc /njh /njs > preview.txt :: preview only
robocopy C:\Data D:\Dst /e /copyall /secfix /timfix /e /xo   :: re-sync metadata only
if %errorlevel% GEQ 8 (echo FAILED) else (echo OK)
```

## 4. Viewing, Searching & Comparing Text

### `find` (simple) vs `findstr` (regex)

| `find` | Explanation |
|---|---|
| `find "text" file.txt` | Case-sensitive search |
| `find /i "text" *.log` | Case-insensitive |
| `find /c "text" file` | Count matching **lines** |
| `find /v "text" file` | Show lines that do NOT match |
| `find /n "text" file` | Prefix line numbers |
| `dir \| find "DIR"` | Filter command output (find filters only, it cannot search recursively on its own) |

| `findstr` | Explanation |
|---|---|
| `findstr "cat dog" file` | Match lines containing cat **OR** dog |
| `findstr /c:"cat dog" file` | Match the literal phrase “cat dog” (spaces included) |
| `findstr /i /s /m "TODO" *.py` | Recursive, case-insensitive, filenames only |
| `findstr /r "^Error.*[0-9]" app.log` | Real regex: `^ $ . * ? [class] \<word \>` |
| `findstr /n /i "pattern" file` | Line numbers + case-insensitive |
| `findstr /x "exact line" file` | Match whole line exactly |
| `findstr /v "#" config.ini` | Exclude comment lines |
| `findstr /b /e "name"` | Match at beginning (`/b`) or end (`/e`) of line |
| `findstr /d:C:\code;D:\src "main" *.c` | Search multiple directories |
| `findstr /g:patterns.txt big.log` | Search patterns from a file |
| `findstr /f:filelist.txt "error"` | Search the files listed in a file |
| `findstr /a:0E /si "password" C:\*.*` | ⚠ Colorized recursive content scan (audit your own files!) |
| `tasklist \| findstr /i "chrome"` | Everyday combo |

### `sort`, `fc`, `comp`, `where`, `clip`

| Command | Explanation |
|---|---|
| `sort file.txt` | Alphabetical sort to screen |
| `sort file.txt /r` | Reverse |
| `sort file.txt /+3` | Sort starting at column 3 of each line |
| `sort file.txt /o out.txt` | Write result to file |
| `sort file.txt /l locale-id` | Locale-aware collation |
| `sort /rec 4096 file` | Max line length (default 2048) |
| `dir \| sort` | Sort piped output |
| `fc a.txt b.txt` | Compare text files, show differences |
| `fc /b a.dll b.dll` | Binary byte-by-byte compare |
| `fc /n` | Line numbers · `/i` ignore case · `/w` ignore whitespace · `/u` Unicode |
| `comp a.dat b.dat` | Byte compare with decimal offsets (`/a` show diffs as ASCII, `/l` line numbers) |
| `where notepad` | Locate executables on PATH (shows every match) |
| `where /r C:\Projects *.sln` | Recursive file search from a root — fast and script-friendly |
| `where /q file & if errorlevel 1 echo not found` | Quiet existence test |
| `command \| clip` | Anything → clipboard |

### `forfiles` — run a command per file (all variables)

| Flag | Meaning |
|---|---|
| `/p path` | Starting folder |
| `/m mask` | File mask (default `*`) |
| `/s` | Recurse subfolders |
| `/d +2024/01/01` or `/d -30` | Files changed after date / within last 30 days (`-dd` = days) |
| `/c "command"` | Command to run per file (default: `cmd /c echo @FILE`) |

Variables inside `/c`: `@file` name · `@fname` name w/o extension · `@ext` extension · `@path` full path · `@relpath` path relative to `/p` · `@isdir` TRUE/FALSE · `@fsize` bytes · `@fdate` · `@ftime`.

```bat
forfiles /s /m *.log /d -30 /c "cmd /c del @path"                 :: delete old logs
forfiles /s /d -90 /c "cmd /c if @isdir==FALSE echo @relpath"     :: list files older than 90 days
forfiles /m *.bak /c "cmd /c echo n | comp @path @path.bak"       :: per-file scripted command
```

## 5. Attributes, Permissions & Ownership

### `attrib` — full flag set

Attribute letters: `R` read-only · `H` hidden · `S` system · `A` archive · `I` not-content-indexed · `X` no-scrub.

| Command | Explanation |
|---|---|
| `attrib file` | Show attributes |
| `attrib +h file` / `attrib -h file` | Hide / unhide |
| `attrib +h +s folder` / `s`+`h` | “Super hide” — invisible even with “show hidden” enabled |
| `attrib +r file` | Read-only · `-r` removes |
| `attrib +r +s +h /s /d C:\Secret\*.*` | Apply recursively to files (`/s`) and folders (`/d`) |
| `attrib -h -r -s /s /d X:\*.*` | Classic USB-unhide recipe after malware hid everything |

### `icacls` — modern ACL tool (all verbs)

Permissions shorthand: `F` full · `M` modify · `RX` read+execute · `R` read · `W` write · `D` delete.
Inheritance flags: `(OI)` object inherit · `(CI)` container inherit · `(IO)` inherit-only · `(NP)` no-propagate · `(I)` inherited from parent.

| Command | Explanation |
|---|---|
| `icacls file` | Show ACLs |
| `icacls file /grant bob:F` | Grant full control (add to existing ACL) |
| `icacls folder /grant Users:(OI)(CI)RX` | Grant read+execute, inherited by files & subfolders |
| `icacls file /grant:r bob:F` | **Replace** all of bob's entries with this one |
| `icacls file /deny bob:W` | Explicit deny (deny always wins) |
| `icacls file /remove bob` | Remove all of bob's entries (`/remove:d` only grant, `/remove:g` only deny) |
| `icacls folder /reset /t /c` | Reset to inherited permissions, recursively, keep going on errors |
| `icacls file /setowner Administrators` | Change owner (`/t /c /q` for silent recursive) |
| `icacls file /inheritance:r` | Remove inherited ACLs (`:e` re-enable, `:d` disable+copy) |
| `icacls /findsid bob C:\Data /t` | Find every ACL mentioning user bob |
| `icacls C:\Data /save acls.txt /t` | Backup all ACLs to file |
| `icacls C:\ /restore acls.txt` | Restore them later |
| `icacls file /verify` | Find ACL canonical-order problems |

### `takeown` & legacy `cacls`

| Command | Explanation |
|---|---|
| `takeown /f file` | Become owner of a file (*Admin*) |
| `takeown /f folder /r /d y` | Recursive takeover, auto-answer “yes” to prompts |
| `takeown /f file /a` | Give ownership to *Administrators* group instead of you |
| `icacls file /grant %username%:F` | The usual follow-up after takeown |
| `cacls file /e /g bob:f` † | Legacy ACL editor — prefer `icacls` |

## 6. Links, Compression & Cabinet Files

### Links: `mklink` & `fsutil hardlink`

| Command | Explanation |
|---|---|
| `mklink link.txt target.txt` | **Symbolic link to file** — needs Admin or Developer Mode |
| `mklink /d C:\link C:\real` | Symbolic link to **directory** — same requirement |
| `mklink /h link.txt target.txt` | **Hard link** — same file, second name, same volume, no admin needed |
| `mklink /j C:\Mount C:\Users\Data` | **Junction** — directory link on local volumes, no admin needed; the classic tool (e.g. move a Steam library) |
| `fsutil hardlink create b.txt a.txt` | Hard link via fsutil |
| `rmdir C:\link` | Delete a link/junction (never removes the target's content) |
| `dir /a:l` | List links/junctions (`<SYMLINK>` `<JUNCTION>` markers) |

### Compression

| Command | Explanation |
|---|---|
| `compact` | Show compression state of folder |
| `compact /c file` / `/c /s` | Compress file / whole tree (NTFS compression) |
| `compact /u /s` | Uncompress tree |
| `compact /c /exe:lzx big.iso` | **CompactOS** — LZX-compress an executable (XPress4K/8K/16K also) |
| `compact /compactos:query` | Is OS binaries compression on? (`:always` / `:never` to set) |
| `makecab file.txt` | Create file1_.cab |
| `makecab file.txt out.cab` | Name the cabinet |
| `expand file.cab -f:* C:\out` | Extract cabinet contents |
| `extrac32 file.cab` | Alternate cabinet extractor |

### `tar` & `curl` (modern additions, Windows 10 1803+)

| Command | Explanation |
|---|---|
| `tar -czf backup.tar.gz folder/` | Create gzip tarball |
| `tar -xzf backup.tar.gz` | Extract |
| `tar -tf archive.tar.gz` | List contents |
| `tar -xzf a.zip` | bsdtar reads **zip** too |
| `tar -a -cf out.zip folder/` | Create **zip** (format from file extension) |
| `tar -xzf a.tar.gz -C C:\dest` | Extract into specific folder |
| `tar -xzf a.tar.gz path/in/archive` | Extract single member |
| `curl -L -o file.zip https://…` | Download with redirect-following |
| `curl -I https://site` | Headers only |
| `curl -F "field=@file" url` | Multipart upload |
| `curl -u user:pass -T file ftp://…` | Upload with auth |

## 7. System Information & Environment

| Command | Explanation |
|---|---|
| `systeminfo` | Everything: OS, BIOS, RAM, hotfixes, network, boot time |
| `systeminfo \| findstr /i "memory hotfix"` | Filter to what you need |
| `systeminfo /s pc01 /u domain\admin /p pw` | Query a remote machine |
| `ver` | Windows version line |
| `winver` | GUI version box |
| `hostname` | Computer name |
| `whoami` | Domain\user |
| `whoami /user` | SID |
| `whoami /groups` | Group memberships + SIDs (check elevation: look for `S-1-16-12288` High) |
| `whoami /priv` | Token privileges (SeBackupPrivilege etc.) |
| `whoami /fo list` | Formatting: `table`, `list`, `csv` |
| `msinfo32` | Full GUI system report |
| `set` | All environment variables |
| `set p` | Show only variables starting with “p” |
| `driverquery` | All drivers, `driverquery /v` verbose, `/fo csv` export, `/si` signed drivers |
| `fltmc` | Filter drivers (Admin) — `fltmc filters` |
| `qprocess` | Quick process/session list (see also §16) |

## 8. `wmic` — Full Alias & Verb Reference † (removed in Win11 24H2+)

> `wmic` is deprecated; modern Windows 11 builds no longer ship it. Everything below maps to `Get-CimInstance` in PowerShell (§P5). Still invaluable on Windows 10.

**Anatomy:** `wmic [global switches] [alias] [verb] [parameters]` — global switches: `/node:pc01` (remote), `/user:`, `/password:`, `/format:list|csv|table`, `/interactive:off`, `/failfast:on`.

**Verbs:** `get` (read properties) · `list` (default view) · `set` (change) · `call` (invoke method) · `create` · `delete` · `assoc` (related objects) · `where` (filter, e.g. `where "name like '%chrome%'"`).

**The complete alias table**

| Alias | Object | Classic query |
|---|---|---|
| `os` | Operating system | `wmic os get caption,version,osarchitecture` |
| `cpu` | Processors | `wmic cpu get name,numberofcores,maxclockspeed` |
| `computersystem` | Machine model, RAM total | `wmic computersystem get manufacturer,model,totalphysicalmemory` |
| `memorychip` | RAM sticks | `wmic memorychip get capacity,speed,manufacturer` |
| `bios` | BIOS/UEFI | `wmic bios get serialnumber,smbiosbiosversion` |
| `baseboard` | Motherboard | `wmic baseboard get manufacturer,product` |
| `diskdrive` | Physical disks | `wmic diskdrive get model,size,mediatype` |
| `logicaldisk` | Volumes | `wmic logicaldisk get caption,size,freespace` |
| `partition` | Partitions | `wmic partition get name,size,type` |
| `volume` | Volumes incl. mount points | `wmic volume get label,capacity,freespace` |
| `process` | Processes | `wmic process get name,processid,commandline` |
| `service` | Services | `wmic service get name,state,startmode` |
| `startup` | Autostart entries | `wmic startup get caption,command` |
| `product` | Installed MSI software | `wmic product get name,version` (slow) |
| `qfe` | Patches/hotfixes | `wmic qfe list` |
| `useraccount` | Local/domain users | `wmic useraccount get name,sid` |
| `group` | Groups | `wmic group get name,sid` |
| `sysaccount` | System accounts | `wmic sysaccount get name,sid` |
| `share` | Shared folders | `wmic share get name,path` |
| `printer` / `printerconfig` | Printers | `wmic printer get name,default` |
| `printjob` | Print queue | `wmic printjob list` |
| `netlogin` | Logon info | `wmic netlogin get name,lastlogon,badpasswordcount` |
| `nic` / `nicconfig` | Adapters / IP config | `wmic nicconfig where IPEnabled=TRUE get ipaddress,macaddress` |
| `netuse` | Mapped drives | `wmic netuse list` |
| `desktop` / `desktopmonitor` | Desktop & monitors | `wmic desktopmonitor get name` |
| `environment` | Env variables (registry) | `wmic environment list` |
| `pagefile` / `pagefileset` | Page file | `wmic pagefileset get initialsize,maximumsize` |
| `cdrom` | Optical drives | `wmic cdrom get name,drive` |
| `sounddev` | Audio devices | `wmic sounddev get name` |
| `idecontroller` / `scsicontroller` | Storage controllers | `wmic idecontroller get name` |
| `battery` | Battery | `wmic battery get estimatedchargeremaining` |
| `systemenclosure` | Chassis (laptop vs desktop) | `wmic systemenclosure get chassistypes` |
| `diskquota` | NTFS disk quotas | `wmic diskquota list` |
| `ntevent` | Event log (slow) | `wmic ntevent where "EventType=1" list` — prefer `wevtutil` §23 |
| `timezone` | Time zone | `wmic timezone get caption` |
| `datafile` | File ops via WMI | `wmic datafile where name="C:\\a.txt" get filesize` |
| `fsdir` | Folder ops | `wmic fsdir where name="C:\\x" list` |

**Killer `wmic` one-liners**

```bat
wmic process where "name='chrome.exe'" delete                    :: kill all chrome
wmic process call create "notepad.exe"                           :: start a process
wmic os get lastbootuptime                                      :: uptime
wmic product where "name='App 3.1'" call uninstall              :: silent uninstall (slow)
wmic /node:pc01 /user:admin /pw:x cpu get loadpercentage        :: remote CPU load
wmic logicaldisk where "drivetype=3" get deviceid,freespace     :: hard drives only
wmic path softwarelicensingservice get OA3xOriginalProductKey    :: Windows product key
wmic recoveros get debuginfoType                                :: crash-dump config
```

**Repairing WMI itself** (*Admin*): `winmgmt /verifyrepository` → `winmgmt /salvagerepository` → (last resort) `winmgmt /resetrepository`.

## 9. Disks & File Systems

### `chkdsk` — all switches

| Command | Explanation |
|---|---|
| `chkdsk C:` | Read-only scan, report only |
| `chkdsk C: /f` | **Fix** file-system errors (prompts to schedule at reboot if volume in use) |
| `chkdsk C: /r` | Fix + **locate bad sectors and recover readable data** (includes `/f`) |
| `chkdsk C: /x` | Force dismount first (implies `/f`) |
| `chkdsk C: /scan` | Online scan, no dismount (Win8+) |
| `chkdsk C: /spotfix` | Takes volume briefly offline to fix queued issues (fastest real fix) |
| `chkdsk C: /b` | Re-evaluate bad clusters (implies `/r`) — use after a disk image restore |
| `chkdsk C: /perf` | Faster (uses more resources) online scan |
| `chkdsk C: /i` `/c` | NTFS speed-ups (skip index checks / cycle check) — scan-only |
| `chkdsk C: /f /r /x` | The canonical deep repair |
| `fsutil dirty query C:` | Is the dirty bit set (repair scheduled)? |
| `chkntfs C:` | Same question interactively |
| `chkntfs /d` | Reset chkdsk schedule to default |
| `chkntfs /x C: D:` | Exclude volumes from boot-time checking |

### `format`, `label`, `vol`, `convert`, `mountvol`, `subst`, `defrag`

| Command | Explanation |
|---|---|
| ⚠ `format E: /fs:ntfs /q /v:Backup` | Quick NTFS format with label |
| ⚠ `format E: /fs:exfat /q` | exFAT (large-compatible, for USB) |
| ⚠ `format E: /fs:fat32 /q` | FAT32 (max 32 GB on Windows format) |
| ⚠ `format E: /p:3` | Overwrite every sector 3 passes (secure erase — slow, no `/q`) |
| `format E: /v:Name /fs:ntfs /a:8192` | Allocation-unit (cluster) size choice |
| `format E: /y` | Suppress confirmation prompt |
| `label C: System` | Change volume label |
| `vol C:` | Show label + serial number |
| `convert D: /fs:ntfs` | FAT32→NTFS **without data loss** (one-way!) |
| `mountvol` | List volumes with their GUIDs |
| `mountvol C:\Mount \\?\Volume{guid}\` | Mount a volume into a folder |
| `mountvol C:\Mount /p` | Dismount + put volume offline (needs a mounted path; `/d` removes) |
| `subst X: C:\deep\path` | Map folder to drive letter X: |
| `subst X: /d` | Remove the mapping |
| `subst` | List mappings |
| `defrag C: /o` | Optimize with the right method per media (SSD trim / HDD defrag) |
| `defrag C: /a` | Analyze only |
| `defrag C: /h` | Normal priority (faster but lags system) |
| `defrag C: /u /v` | Progress + verbose stats |
| `defrag C: /x` | Consolidate free space (HDD) |
| `defrag C: /c /o` | All volumes, optimized |

## 10. `diskpart` — Every Subcommand (Admin)

`diskpart` is an **interactive** shell with its own commands (it also runs scripts: `diskpart /s script.txt`). Golden rule: **`list` → `select` → act**. Nothing applies until you've selected a focus object.

| Subcommand | Meaning |
|---|---|
| `list disk` / `list volume` / `list partition` / `list vdisk` | Survey everything |
| `select disk 1` / `select volume 3` / `select partition 2` / `select vdisk file="C:\v.vhdx"` | Set focus |
| `detail disk` / `detail volume` / `detail partition` | Deep info about focus |
| `attributes disk` / `attributes volume` | Show read-only/hidden attributes |
| `attributes disk clear readonly` | Clear read-only (fixes “write-protected” USB) |
| ⚠ `clean` | Zero the MBR/GPT sector on selected disk — wipes layout (data recoverable) |
| ⚠ `clean all` | Zero **every sector** — secure wipe, hours |
| `convert mbr` / `convert gpt` | Convert empty disk partition style |
| `convert basic` / `convert dynamic` | Between basic/dynamic (empty disk) |
| `create partition primary size=51200` | 50 GB primary (in MB; omit size = all space) |
| `create partition extended` / `create partition logical` | Legacy MBR extended/logical |
| `create partition efi size=260` / `create partition msr` | UEFI system / Microsoft-reserved |
| `create volume simple disk=1` / `span` / `stripe` / `mirror` / `raid` | Dynamic volumes |
| ⚠ `create vdisk file="C:\d.vhdx" maximum=20480 type=fixed` | 20 GB VHD/VHDX (also `type=expandable`) |
| `attach vdisk` / `detach vdisk` | Mount / unmount virtual disk |
| `compact vdisk` | Shrink a dynamic VHDX |
| `expand vdisk maximum=40960` | Grow a VHDX |
| `merge vdisk depth=1` | Merge differencing disk into parent |
| `format fs=ntfs label="Data" quick` | Format focus volume (`fs=fat32\|exfat\|ntfs\|udf`, `unit=N`, `override`) |
| `assign letter=E` | Assign drive letter (`assign` = next free) |
| `assign mount=C:\Mount` | Mount to folder instead |
| `remove letter=E` / `remove dismount` / `remove all` | Remove letter/mount |
| `active` | Mark MBR partition active (bootable) |
| `inactive` | Clear the active flag |
| `extend size=10240` | Grow volume by 10 GB into adjacent free space (omit size = all) |
| `shrink desired=5120` | Shrink volume by 5 GB (`minimum=`, `querymax`) |
| ⚠ `delete partition override` / `delete volume` / `delete disk` | Delete things (`override` needed for protected/system partitions) |
| `rescan` | Re-scan for new hardware |
| `online disk` / `offline disk` | Bring disk online/offline |
| `online volume` / `offline volume` | Same for volumes |
| `set id=ebd0a0a2-b9e5-4433-87c0-68b6b72699c7` | Change partition type GUID |
| `gpt attributes=0x8000000000000000` | GPT attribute bits (read-only etc.) |
| `uniqueid disk` / `uniqueid volume` | Show/set MBR signature or GPT GUID |
| `filesystems` | File systems supported on focus volume |
| `repair raid` | Rebuild RAID-5 member |
| `retain` | Place retained simple volume under a dynamic mirror (server migration) |
| `san policy=onlineall` | Storage-area-network attach policy |
| `import` | Import a foreign disk group |
| `break disk=1` | Break a mirror (`keep`/`no keep`) |
| `add disk=1` | Add mirror to simple volume |
| `help` / `exit` | Obvious |

**Format a USB stick (classic sequence)**

```text
diskpart
list disk                        ← identify the USB by size!
select disk 2
clean
create partition primary
format fs=exfat label="USB" quick
assign
exit
```

⚠ `clean` on the wrong disk number destroys its partitions — verify the size column twice.

## 11. `fsutil` — Subcommand Reference (Admin)

| Command | Explanation |
|---|---|
| `fsutil fsinfo drives` | All drive letters |
| `fsutil fsinfo volumeinfo C:` | Name, serial, FS, features of volume |
| `fsutil fsinfo ntfsinfo C:` | NTFS geometry details |
| `fsutil fsinfo sectorinfo C:` | Physical sector vs logical sector size |
| `fsutil fsinfo statistics C:` | FS performance counters |
| `fsutil volume diskfree C:` | Free space, allocated, total |
| `fsutil volume unmount D:` | Unmount a volume |
| `fsutil dirty query C:` | Dirty-bit status |
| `fsutil dirty set C:` | Force chkdsk at next boot |
| `fsutil file createnew C:\1mb.bin 1048576` | Exact-size file |
| `fsutil file setzerodata offset=0 length=4096 file.txt` | Zero a byte range (secure erase part of a file) |
| `fsutil file queryextents file.txt` | Extent map |
| `fsutil hardlink create b.txt a.txt` | Hard link |
| `fsutil 8dot3name query C:` | 8.3 name state per volume |
| `fsutil 8dot3name strip C:\folder` | Strip 8.3 names (speeds directories) |
| `fsutil behavior query disabledeletenotify` | TRIM enabled? (1 = disabled!) |
| `fsutil behavior set disabledeletenotify 0` | Re-enable TRIM |
| `fsutil behavior set disablelastaccess 1` | Stop updating last-access timestamps (perf) |
| `fsutil behavior set mftzone 2` | Reserve more MFT space |
| `fsutil behavior set symlinkevaluation L2L:1 L1L:1` | Enable local-to-local symlinks |
| `fsutil sparse setflag big.vhd` | Mark sparse |
| `fsutil sparse setrange file 0 1048576` | Punch a zero range (make file sparse) |
| `fsutil reparsepoint query link` | Inspect symlink/junction data |
| `fsutil quota query C:` | NTFS quotas |
| `fsutil objectid query file` | Distributed Link Tracking ID |
| `fsutil usn queryjournal C:` | USN change journal state |
| `fsutil usn readdata file.txt` | File's USN records |
| `fsutil wim enumerate C:` / `wim querypatch file` | WIM-backed files (CompactOS) |
| `fsutil transaction query` | Active NTFS transactions |

## 12. `cipher` — EFS Encryption & Free-Space Wiping (Admin)

| Command | Explanation |
|---|---|
| `cipher` | Folder encryption state (U = unencrypted, E = encrypted) |
| `cipher /e /s:C:\Secret` | Encrypt folder + subfolders |
| `cipher /d /s:C:\Secret` | Decrypt |
| `cipher /e /a file` / `/d /a file` | Encrypt/decrypt a single file (`/a`) |
| `cipher /e /s:.\ /h` | Include hidden files (`/h`), force (`/f`) |
| `cipher /c file` | Show certificate info used to encrypt |
| `cipher /k` | Create a new EFS certificate + key |
| `cipher /x:Me backup.pfx` | Export certificate+key (do this or lose data on reinstall!) |
| `cipher /y` | Display thumbprint of current EFS cert |
| `cipher /r:Me` | Generate EFS recovery cert (.cer + .pfx) |
| ⚠ `cipher /w:C:` | **Overwrite all free space** with zeros then random data — secure deletion of “deleted” files; takes hours |
| `cipher /b file` | Re-encrypt file to force bad-cluster recovery |

## 13. Networking Core Commands

### `ipconfig` — all switches

| Command | Explanation |
|---|---|
| `ipconfig` | IP, mask, gateway per adapter |
| `ipconfig /all` | + MAC, DHCP, DNS, lease times — the first command of every network audit |
| `ipconfig /release` + `/renew` | Get a fresh DHCP address (order matters) |
| `ipconfig /release6` / `renew6` | IPv6 variants |
| `ipconfig /flushdns` | Clear the DNS resolver cache (fixes “site not found” after DNS changes) |
| `ipconfig /displaydns` | Show cached DNS entries |
| `ipconfig /registerdns` | Re-register this machine's name in dynamic DNS (after changing IP) |
| `ipconfig /showclassid "Wi-Fi"` | DHCP class IDs |
| `ipconfig /setclassid "Wi-Fi" ID` | Set one |

### `ping` — all switches

| Flag | Meaning |
|---|---|
| `ping host` | 4 echoes |
| `-t` | Forever until Ctrl+C (Ctrl+Break = stats while running) |
| `-n count` | Number of echoes |
| `-l size` | Payload bytes (`ping -l 1472 -f` = MTU path test) |
| `-f` | Set Don't-Fragment flag (IPv4) |
| `-i ttl` | Set TTL |
| `-v tos` | Type of service (legacy) |
| `-r count` | Record route hops |
| `-s count` | Timestamps |
| `-j host-list` / `-k host-list` | Loose / strict source route |
| `-w timeout` | Milliseconds to wait per reply |
| `-4` / `-6` | Force IPv4/IPv6 |
| `-S srcaddr` | Pick source address on multihomed machines |
| `-a` | Resolve IP → name (reverse) |

Reading results: `Reply from… time=Xms TTL=Y` = healthy · `Destination host unreachable` = routing/LAN issue · `Request timed out` = no reply (or blocked by firewall — note that ICMP is often blocked, so a failed ping ≠ dead server) · `General failure` = no route/local stack problem.

### `tracert`, `pathping`, `nslookup`, `netstat`, `arp`, `route`, `nbtstat`, `getmac`

| Command | Explanation |
|---|---|
| `tracert host` | Hop-by-hop route with latency |
| `tracert -d host` | Skip DNS (much faster, IP-only) |
| `tracert -h 15 host` | Max hops |
| `tracert -w 1000 host` | 1 s timeout per hop |
| `tracert -j looselist` / `-4 -6` | Source-route / IP version |
| `pathping host` | traceroute + packet-loss stats **per hop** over 25 s per hop — finds the flaky router |
| `pathping -n -q 10 -p 250 host` | No DNS, 10 queries/hop, 250 ms interval |
| `nslookup domain` | Quick DNS answer |
| `nslookup domain 8.8.8.8` | Query a specific server |
| `nslookup -type=MX domain` | `-type=`: A, AAAA, MX, NS, SOA, TXT, SRV, CNAME, PTR, ANY |
| `nslookup -type=PTR 8.8.8.8` | Reverse lookup |
| `nslookup` (interactive) | Enters the shell below |
| `netstat -ano` | All connections + owning PID (`-n` numeric, `-a` all, `-o` PID) |
| `netstat -b` | Which **program** owns each connection (Admin) |
| `netstat -e` | Interface statistics (errors!) |
| `netstat -r` | Routing table (= `route print`) |
| `netstat -s` | Per-protocol statistics |
| `netstat -p tcp` | Filter to TCP (or `udp`, `ip`) |
| `netstat -q` | Listening + bound ports |
| `netstat -t` | Current offload state |
| `netstat -ano 5` | Refresh every 5 s forever |
| `netstat -ano \| findstr :443` | The everyday port-finder combo |
| `arp -a` | IP↔MAC table (all interfaces) |
| `arp -a -N 192.168.1.1` | For one interface |
| `arp -d 192.168.1.5` / `arp -d *` | Delete entry/all |
| `arp -s 192.168.1.5 00-aa-bb-cc-dd-ee` | Static entry (ping-alias trick) |
| `route print` | Full routing table (IPv4 + IPv6) |
| `route add 10.5.0.0 mask 255.255.0.0 10.5.1.1` | Temp route |
| `route add … -p` | **Persistent** route (survives reboot) |
| `route change 10.5.0.0 mask 255.255.0.0 10.5.1.2` | Modify |
| `route delete 10.5.0.0` | Remove |
| `route -f` | Flush all routes (careful — kills connectivity temporarily) |
| `route print -4` | IPv4 table only |
| `nbtstat -n` | Local NetBIOS names |
| `nbtstat -c` | Cached name→IP |
| `nbtstat -r` / `-R` | Resolved-by-broadcast count / purge cache |
| `nbtstat -a pc01` / `-A 192.168.1.10` | Remote name table (by name / by IP) |
| `nbtstat -S` | Sessions with dest IPs |
| `getmac` / `getmac /v /fo csv` | MAC addresses, verbose CSV |

**`nslookup` interactive subcommands**

| Sub | Meaning |
|---|---|
| `server 1.1.1.1` | Switch default resolver for this session |
| `lserver 1.1.1.1` | Same but via the *original* server |
| `root` | Point at the root servers |
| `set type=MX` | Query type (A, ANY, MX, NS, PTR, SOA, SRV, TXT) |
| `set debug` / `set d2` | Turn on query details / full debug |
| `set recurse` / `set norecurse` | Toggle recursion |
| `set retry=3` / `set timeout=5` | Retries / timeout |
| `set domain=x.com` / `set search` | Append domain to bare names |
| `set vc` | Use TCP instead of UDP |
| `set port=53` | Nonstandard DNS port |
| `ls -t mx domain` | Zone listing filtered (`-a` aliases, `-d` all) — usually refused by servers |
| `view file` | Page through a previous `ls` output |
| `finger user` | Finger the server |
| `exit` | Quit |

### `curl` (shipped with Windows), OpenSSH, `telnet`, `finger`

| Command | Explanation |
|---|---|
| `curl https://api.example.com` | GET, print body |
| `curl -o page.html https://site` | Save body to file (`-O` keep remote name) |
| `curl -L url` | Follow redirects |
| `curl -k https://self-signed` | Ignore cert errors |
| `curl -I url` | Headers only |
| `curl -X POST -d "a=1&b=2" url` | Form POST |
| `curl -H "Authorization: Bearer TOKEN" url` | Add header |
| `curl -T file ftp://…` / `curl -u user:pass url` | Upload / auth |
| `curl -s -o nul -w "%{http_code}" url` | Silent status-code check |
| `curl --resolve site:443:1.2.3.4 https://site` | Test IP before DNS switch |
| `ssh user@host` | OpenSSH client included in Windows |
| `ssh -p 2222 user@host` / `ssh -i key.pem user@host` | Port / identity |
| `scp file user@host:/path` / `scp user@host:/path file` | Copy over SSH |
| `sftp user@host` | Interactive file shell (get, put, ls, cd, lpwd) |
| `ssh-keygen -t ed25519 -C "me@x"` | Generate keys (`%USERPROFILE%\.ssh\id_ed25519`) |
| `type key.pub \| ssh user@host "cat >> .ssh/authorized_keys"` | Manual copy-id |
| `telnet host port` | Raw TCP test — **requires enabling**: `dism /online /enable-feature /featurename:TelnetClient` |
| inside telnet: Ctrl+] → `quit` | Escape menu (open, close, status, display, set) |
| `finger user@host` | User info (rarely served anymore) |

## 14. `netsh` — Contexts & Subcommands (the network Swiss-army knife)

`netsh` is a shell inside a shell: `netsh ⟨context⟩ ⟨subcontext⟩ ⟨command⟩`. Explore any level with `netsh ⟨context⟩ ?`. `netsh dump > backup.txt` snapshots the whole configuration; `netsh exec backup.txt` restores.

**Top-level contexts:** `advfirewall`, `branchcache`, `bridge`, `dhcp` (server role), `dns` (server role), `http`, `interface`, `ipsec`, `lan`, `mbn`, `namespace`, `netio`, `p2p`, `ras`, `rpc`, `trace`, `wfp`, `winhttp`, `winsock`, `wlan`.

### `netsh wlan` — Wi-Fi (the favorites)

| Command | Explanation |
|---|---|
| `netsh wlan show interfaces` | Current SSID, BSSID, signal %, radio state |
| `netsh wlan show profiles` | Saved networks |
| `netsh wlan show profile name="Cafe5G" key=clear` | Show saved **password** (in Key Content) |
| `netsh wlan show networks mode=bssid` | All visible networks + channels + signal |
| `netsh wlan show drivers` | Driver capabilities (hosted network? 802.11ax?) |
| `netsh wlan show hostednetwork` | Legacy soft-AP state |
| `netsh wlan export profile folder=C:\wifi key=clear` | Dump profiles as XML (with passwords) |
| `netsh wlan add profile filename="Cafe.xml" user=all` | Re-import a profile XML |
| `netsh wlan delete profile name="Cafe"` | Forget a network |
| `netsh wlan connect name="Home5G"` / `disconnect` | Join / leave |
| `netsh wlan set autoconfig enabled=yes interface="Wi-Fi"` | Re-enable Wi-Fi radio config |

### `netsh advfirewall` — firewall

| Command | Explanation |
|---|---|
| `netsh advfirewall show allprofiles` | State of domain/private/public profiles |
| `netsh advfirewall show allprofiles state` | On/off at a glance |
| `netsh advfirewall set allprofiles state off` ⚠ / `on` | Toggle firewall |
| `netsh advfirewall set allprofiles firewallpolicy blockinbound,allowoutbound` | Explicit policy |
| `netsh advfirewall firewall add rule name="Web80" dir=in action=allow protocol=TCP localport=80` | Allow inbound TCP/80 |
| `… dir=out action=block program="C:\app\app.exe"` | Block an outbound program |
| `… remoteip=192.168.1.0/24 profile=private` | Scope by IP + profile |
| `netsh advfirewall firewall show rule name=all` | List rules |
| `netsh advfirewall firewall show rule name="Web80" verbose` | One rule in detail |
| `netsh advfirewall firewall set rule name="Web80" new action=block` | Edit |
| `netsh advfirewall firewall delete rule name="Web80"` | Delete |
| `netsh advfirewall export "fw.wfw"` / `import "fw.wfw"` | Backup / restore |
| `netsh advfirewall reset` | Factory defaults |
| `netsh advfirewall monitor show currentprofile` | Live firewall view |

### `netsh interface` — IP configuration

| Command | Explanation |
|---|---|
| `netsh interface show interface` | Adapters up/down |
| `netsh interface ip show config` | Full IP config (all adapters) |
| `netsh interface ip show addresses "Wi-Fi"` | One adapter |
| `netsh interface ip show dnsservers "Wi-Fi"` | DNS servers in use |
| `netsh interface ip set address "Wi-Fi" static 192.168.1.50 255.255.255.0 192.168.1.1` | Static IP + gateway (Admin) |
| `netsh interface ip set address "Wi-Fi" dhcp` | Back to DHCP |
| `netsh interface ip set dns "Wi-Fi" static 1.1.1.1` | Primary DNS |
| `netsh interface ip add dns "Wi-Fi" 8.8.8.8 index=2` | Secondary |
| `netsh interface ip set dns "Wi-Fi" dhcp` | DNS from DHCP |
| `netsh interface ip set address "Wi-Fi" static 2001:db8::5` | IPv6 (same pattern under `ipv6`) |
| `netsh interface ip reset` | Reset the entire TCP/IP stack (reboot) |
| `netsh interface tcp show global` | TCP tuning (autotuning, CTCP…) |
| `netsh interface tcp set global autotuninglevel=normal` | Fix slow downloads |
| `netsh interface portproxy add v4tov4 listenport=8080 connectaddress=192.168.1.10 connectport=80` | Port-forward 8080→other host:80 |
| `netsh interface portproxy show all` / `delete v4tov4 listenport=8080` | Manage forwards |
| `netsh interface set interface "Wi-Fi" disable` / `enable` | Toggle adapter |

### Other netsh fixes you'll actually use

| Command | Explanation |
|---|---|
| `netsh winsock reset` | Reset Winsock catalog — the classic network-stack repair |
| `netsh int ip reset` (= above) | Reset IPv4/IPv6 to defaults |
| `netsh winhttp show proxy` / `set proxy proxy-server="http=p.proxy:80"` | System-wide HTTP proxy |
| `netsh winhttp import proxy source=ie` | Copy user proxy to machine |
| `netsh http show urlacl` | Reserved HTTP.SYS URLs |
| `netsh http add urlacl url=http://+:8080/ user=Everyone` | Reserve endpoint for a service |
| `netsh trace start capture=yes tracefile=C:\etl.etl` / `stop` | Packet/event capture |
| `netsh trace start scenario=NetConnection` | Guided diagnostic scenario |
| `netsh mbn show interfaces` | Cellular modems |
| `netsh lan show profiles` | Wired 802.1X profiles |

## 15. `net` — Every Subcommand

| Subcommand family | Key variants |
|---|---|
| `net view` | Computers on the LAN · `net view \\pc01` = its shares |
| `net use` | List mapped drives |
| `net use Z: \\server\share` | Map drive (with `/persistent:yes\|no`) |
| `net use Z: \\server\share /user:DOM\alice pw` | Map with credentials |
| `net use Z: /delete` / `net use * /delete` | Unmap one / all |
| `net use \\server\ipc$ /delete` | Kill cached session (fixes “multiple connections” error 1219) |
| `net share` | List this machine's shares |
| `net share Data=C:\Data /grant:Everyone,FULL` | Create share |
| `net share Data /users:10 /remark:"team"` | Limit + comment |
| `net share Data /delete` | Stop sharing |
| `net session` | Who is connected to us · `/delete \\pc` kick them |
| `net file` | Open files on server · `net file id /close` |
| `net start` / `net stop` | List running services / control one (`net start spooler`) |
| `net pause` / `net continue` | Pause/resume pausable services |
| `net statistics server` / `workstation` | Uptime, bytes, errors |
| `net config server` / `workstation` | Server/workstation config |
| `net config server /srvcomment:"TEXT"` | Change network description |
| `net time \\pc01` / `net time /domain` / `net time \\pc01 /set` | Check/sync time |
| `net localgroup` | List groups · `net localgroup "Grp" user /add` / `/delete` |
| `net localgroup "Backup Ops" /add` | Create a group |
| `net group` | Same for domain groups (Active Directory) |
| `net user` | Users table |
| `net user alice` | One user's full details |
| `net user alice P@ss /add` | Create with password |
| `net user alice /active:no` | Disable · `/active:yes` re-enable |
| `net user alice NewPw` | Change password |
| `net user alice *` | Prompt for new password |
| `net user alice /delete` | Delete account |
| `net user alice /passwordchg:no /passwordreq:yes` | Policy bits |
| `net user alice /times:mon-fri,09-17` | Allowed logon hours |
| `net user alice /workstations:pc01` | Restrict machines |
| `net user alice /expires:never` / `01/01/2027` | Account expiry |
| `net user alice /fullname:"Alice A" /comment:"x"` | Metadata |
| `net user alice /homedir:\\srv\home$ /scriptpath:logon.bat` | Profile fields |
| `net accounts` | Password/lockout policy display |
| `net accounts /minpwlen:10 /maxpwage:90 /minpwage:1 /uniquepw:5` | Enforce policy |
| `net accounts /lockoutthreshold:5 /lockoutduration:30 /lockoutwindow:30` | Lockout rules |
| `net accounts /forcelogoff:30` | Force logoff when hours expire |
| `net accounts /sync` | Sync with domain controller |
| `net computer \\pc05 /add` / `/del` | Machine account in domain |
| `net send` † | Gone since Vista → use `msg` (§16) |
| `net helpmsg 1219` | **Plain-English explanation of any Windows network error number** — secret weapon |

## 16. Process & Task Management

### `tasklist` — all filters

| Form | Meaning |
|---|---|
| `tasklist` | Everything running |
| `tasklist /svc` | Include services inside each PID (find the SVCHOST owner!) |
| `tasklist /v` | Verbose: status, user, memory, window title |
| `tasklist /m` / `tasklist /m ntdll.dll` | DLL modules per process |
| `tasklist /fi "IMAGENAME eq chrome.exe"` | Filter by name |
| `tasklist /fi "PID eq 1234"` | By PID |
| `tasklist /fi "STATUS eq not responding"` | Hung windows |
| `tasklist /fi "MEMUSAGE gt 200000"` | Memory hogs (>200 MB, in KB) |
| `tasklist /fi "SESSIONNAME eq console"` | Local-session processes |
| `tasklist /fi "WINDOWTITLE eq Administrator*"` | By title (wildcard ok) |
| `tasklist /fi "SERVICES eq wuauserv"` | Hosting a service |
| `tasklist /fi "MODULES eq wininet.dll"` | Loaded-DLL filter |
| `tasklist /s pc01 /u dom\admin /p pw` | Remote |
| `tasklist /fo csv /nh > procs.csv` | Export (csv/table/list; `/nh` no header) |

Filter operators: `eq ne gt lt ge le` (strings use eq/ne only).

### `taskkill` — all flags

| Form | Meaning |
|---|---|
| `taskkill /im chrome.exe` | Graceful by name (`*` wildcard allowed) |
| ⚠ `taskkill /im chrome.exe /f` | **Force** terminate |
| `taskkill /pid 1234 /f` | By PID |
| `taskkill /pid 1234 /t /f` | Kill PID **plus its child tree** |
| `taskkill /im app.exe /fi "STATUS eq NOT RESPONDING"` | Only hung instances |
| `taskkill /s pc01 /im app.exe /f` | Remote kill (Admin) |

Alternatives: `wmic process where name='x.exe' delete` · PowerShell `Stop-Process -Name x -Force` · `tskill app` (TS-style, no `.exe`) · `pskill` (Sysinternals).

### `start` — all flags

| Form | Meaning |
|---|---|
| `start notepad` | Launch program (bare `start` opens a new CMD) |
| `start file.txt` | Open in default handler |
| `start http://example.com` | Open in browser |
| `start "" "C:\path with spaces\app.exe"` | Empty title (`""`) required before quoted paths — classic gotcha |
| `start /min app` / `start /max app` | Window state |
| `start /wait installer.exe` | Script waits until it exits (check `%errorlevel%`) |
| `start /b tool.exe` | Launch without new window |
| `start /low /belownormal /normal /abovenormal /high /realtime app` | CPU priority |
| `start /affinity F app` | Pin to CPU cores (hex mask) |
| `start /node 1 /affinity F app` | NUMA node + mask |
| `start /d C:\work app.exe` | Set working directory |

### Synchronization & messaging

| Command | Explanation |
|---|---|
| `timeout /t 5` | Wait 5 s (keypress-skippable; `/nobreak` to prevent) |
| `timeout /t 5 /nobreak` | Hard wait |
| `ping -n 6 127.0.0.1 >nul` | Legacy ~5-second wait trick |
| `waitfor go` | Blocks until another process/schedule sends signal “go” |
| `waitfor /si go` | Send that signal (works across machines on a domain!) |
| `msg alice "Restart in 5 min"` | Popup to user · `msg * "text"` everyone · `msg console "x"` this session |
| `msg alice /time:60 "text"` | Message auto-closes after 60 s |
| `logoff` | Log off current session · `logoff 2` session id · `logoff rdp-tcp#1` |

## 17. `schtasks` — Every Subcommand

| Subcommand | Meaning |
|---|---|
| `/create` | New task (flags below) |
| `/query` | List tasks — `/fo list\|table\|csv` (add `/v` for everything) |
| `/run /tn "Name"` | Start a task immediately |
| `/end /tn "Name"` | Stop a running task |
| `/change` | Edit — `/tn "Name" /tr "newcmd"` `/enable` `/disable` `/ru user /rp pw` `/sd` `/ed` `/st` |
| `/delete /tn "Name"` ⚠ | Delete (add `/f` = no confirm; `/tn \*` all — careful) |
| `/showsid /tn "Name"` | Show the task's security ID |

**`/create` switches**

| Switch | Meaning |
|---|---|
| `/tn "Name"` | Task name (subfolders via `\`: `"MyTasks\Backup"`) |
| `/tr "C:\script.bat arg"` | Command to run (quote whole string) |
| `/sc minute\|hourly\|daily\|weekly\|monthly\|once\|onstart\|onlogon\|onidle\|onevent` | Schedule type |
| `/mo n` | Modifier: every n minutes/hours/days; `FIRST/SECOND/LAST` for monthly weeks |
| `/d MON,TUE` / `/d 15` | Day(s) of week (for weekly) or of month (monthly) |
| `/m jan,feb` | Months (monthly) |
| `/st 22:00` | Start time |
| `/sd 01/01/2026` / `/ed 12/31/2026` | Start/end dates |
| `/ri 5` | Repetition interval in minutes (minute/hourly) |
| `/du 2:00` / `/k` | Run duration / kill at end of duration |
| `/rl HIGHEST\|LIMITED` | Run elevation |
| `/ru SYSTEM` / `/ru user /rp password` | Account to run as (`/ru SYSTEM` = no password needed) |
| `/it` / `/np` | Only when user logged on / no password storage |
| `/f` | Overwrite existing same-name task silently |
| `/z` | Delete task after final run |
| `/s pc /u user /p pw` | Remote machine |
| `/xml file.xml` | Create from XML export |
| `/v1` | Legacy compatibility |

**Recipes**

```bat
schtasks /create /tn "NightlyBackup" /tr "C:\Scripts\backup.bat" /sc daily /st 22:00 /ru SYSTEM /rl HIGHEST /f
schtasks /create /tn "HourlySync" /tr "C:\s.bat" /sc hourly /mo 2            :: every 2 hours
schtasks /create /tn "Mon" /tr "C:\s.bat" /sc weekly /d MON /st 09:00
schtasks /create /tn "Login" /tr "C:\s.bat" /sc onlogon
schtasks /create /tn "FreeRAM" /tr "C:\s.bat" /sc minute /mo 30
schtasks /query /fo csv /v | findstr /i "backup"
schtasks /change /tn "NightlyBackup" /st 23:30
schtasks /run /tn "NightlyBackup"
schtasks /end   /tn "NightlyBackup"
schtasks /change /tn "NightlyBackup" /disable
schtasks /delete /tn "NightlyBackup" /f
```

`at 22:00 backup.bat` † — the pre-Vista scheduler; removed on modern Windows.

## 18. `sc` — Every Subcommand (service control)

> Syntax quirk: **a space is required after every `=`** (`start= auto`, not `start=auto`) or the command fails silently.

| Subcommand | Meaning |
|---|---|
| `sc query` | All services + state |
| `sc query type= service state= all` | Really all (incl. inactive) |
| `sc queryex winmgmt` | One service, extended info (PID!) |
| `sc qc winmgmt` | **Query config**: start type, binary path, account |
| `sc start wuauserv` / `sc stop wuauserv` | Start / stop |
| `sc pause svc` / `sc continue svc` | Pause / resume (if supported) |
| `sc config svc start= auto` | Auto start: `boot`, `system`, `auto`, `demand`, `disabled`, `delayed-auto` |
| `sc config svc binpath= "C:\app\app.exe -arg"` | Change executable |
| `sc config svc obj= LocalSystem` | Run account |
| `sc failure svc reset= 86400 actions= restart/60000/restart/60000//` | Auto-restart on crash (empty slot = no 3rd action) |
| `sc qfailure svc` / `sc qdescription svc` | Read back failure actions / description |
| `sc description svc "What it does"` | Set description |
| `sc create NewSvc binpath= "C:\app\app.exe" start= demand` | Register a service |
| `sc create … obj= "NT AUTHORITY\LocalService"` | With a service account |
| ⚠ `sc delete svc` | Unregister |
| `sc sdshow svc` / `sc sdset svc SDDL` | Security descriptor raw |
| `sc getdisplayname svc` / `sc getkeyname "Display Name"` | Name translation |
| `sc enum` | Enumerate services (legacy) |
| `sc boot ok\|bad` | Mark last boot good/bad |
| `sc lock` / `sc unlock` / `sc querylock` | Lock service DB (rare) |
| `sc control svc param` | Send custom control code |
| `sc privs svc` / `sc qprivs svc` | Required privileges |
| `net start svc` / `net stop svc` | Friendly wrappers (also `net start` lists running) |

PowerShell equivalents §P6: `Get-Service`, `Set-Service -StartupType`, `New-Service`, `Restart-Service`.

## 19. Users, Groups & Security

### Account & credential tools

| Command | Explanation |
|---|---|
| `runas /user:Administrator cmd` | Elevated/different-user shell (prompts for password) |
| `runas /user:dom\admin /env "mmc compmgmt.msc"` | Load user profile env |
| `runas /netonly /user:dom\user app` | Credentials only for remote access |
| `runas /savecred /user:admin app` ⚠ | Caches password after first use — **security risk**, avoid |
| `cmdkey /list` | Stored credentials (Windows Credential Manager) |
| `cmdkey /list:target` | Details of one |
| `cmdkey /add:server /user:dom\alice /pass:pw` | Save a credential |
| `cmdkey /generic:TERMSRV/server /user:a /pass:p` | Save for RDP |
| `cmdkey /delete:target` / `/ras` | Remove one / dial-up |
| `whoami /upn` | User principal name |
| `quser` | Logged-on users (see §25) |
| `logoff` | Log off (see §16) |

### Security policy & auditing (Admin)

| Command | Explanation |
|---|---|
| `auditpol /get /category:*` | Current audit policy |
| `auditpol /set /category:"Logon/Logoff" /success:enable /failure:enable` | Turn on logon auditing |
| `auditpol /backup /file:audit.csv` / `restore /file:audit.csv` | Save/load policy |
| `auditpol /list /subcategory:*` | Discover subcategories |
| `secedit /analyze /db db.sdb /cfg %windir%\security\templates\setup security.inf` | Compare policy to baseline |
| `secedit /export /cfg policy.cfg` | Dump local security policy to text |
| `secedit /configure /db db.sdb /cfg policy.cfg` | Apply a policy file |
| `secedit /validate file.inf` | Check a template |
| `secedit /generaterollback /cfg new.inf /rbk rollback.inf /log log.txt` | Rollback template |
| `gpresult /r` | Resultant Group Policy (see §21) |

### BitLocker (`manage-bde`, Admin)

| Command | Explanation |
|---|---|
| `manage-bde -status` | Volumes + protection state |
| `manage-bde -on C: -RecoveryPassword` | Encrypt with 48-digit recovery key |
| `manage-bde -off C:` | Decrypt |
| `manage-bde -lock D:` / `-unlock D: -RecoveryPassword 123456-…` | Lock/unlock data drive |
| `manage-bde -protectors -get C:` | List key protectors |
| `manage-bde -pause` / `-resume` | Pause/resume encryption |

## 20. Registry — `reg` (Every Operation), `regedit`, `regini`

Root keys: `HKLM` (HKEY_LOCAL_MACHINE) · `HKCU` (current user) · `HKU` (users) · `HKCR` (classes; `HKLM\SOFTWARE\Classes`) · `HKCC` (current control set). 32/64-bit registry views: append `/reg:32` or `/reg:64` (default = native).

| Operation | Syntax | Notes |
|---|---|---|
| **query** | `reg query HKLM\SOFTWARE\Vendor /v Version` | Read one value |
| | `reg query HKLM\SOFTWARE\Vendor` | All values of key |
| | `reg query HKLM\SOFTWARE\Vendor /s` | Recursive (whole subtree) |
| | `reg query HKLM /f "productkey" /s /e` | **Search** data for string; `/k` search key names, `/d` data only, `/e` exact match |
| | `reg query \\pc01\HKLM\…` | Remote |
| **add** | `reg add HKCU\Environment /v MyVar /t REG_SZ /d "Hi" /f` | `/t`: REG_SZ, REG_DWORD, REG_QWORD, REG_BINARY, REG_EXPAND_SZ, REG_MULTI_SZ · `/d` data · `/f` no-confirm |
| | `reg add … /ve /d "default"` | Set the key's *default* value |
| | `reg add … /v N /t REG_DWORD /d 1 /reg:64` | Force 64-bit view |
| **delete** ⚠ | `reg delete HKCU\… /v Name /f` | Value · `/ve` default · `/va` all values |
| | `reg delete HKCU\… /f` | Whole key tree |
| **copy** | `reg copy HKLM\Src HKLM\Dst /s /f` | Duplicate a subtree |
| **compare** | `reg compare HKCU\A HKCU\B /v Name` | Diff keys; `/oa` show all, `/os` only matches, `/od` only differences |
| **export** | `reg export HKLM\SOFTWARE\Vendor backup.reg` | Backup (text .reg) |
| **import** | `reg import backup.reg` | Restore (silent) — `regedit /s backup.reg` identical |
| **save** | `reg save HKLM\SOFTWARE hive.hiv` | Binary hive copy — the *safe* way to snapshot before edits |
| **restore** | `reg restore HKLM\SOFTWARE hive.hiv` | Put it back |
| **load** | `reg load HKLM\TempHive C:\Users\x\NTUSER.DAT` | Mount an offline user hive |
| **unload** | `reg unload HKLM\TempHive` | Unmount (always do this!) |

`regedit` switches: `regedit /e file.reg` export · `/s` silent import · `regedit` alone = GUI.
`regini file.txt` applies permission/key scripts — the scripted way to set registry ACLs.

**Rite of passage example** — read, back up, change, verify:

```bat
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Run"          :: what autostarts
reg export "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" run.bak :: backup
reg add "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v Note /t REG_SZ /d "notepad.exe" /f
reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Run" /v Note   :: verify
```

## 21. Maintenance & Recovery

### `sfc` (System File Checker, Admin)

| Command | Meaning |
|---|---|
| `sfc /scannow` | Scan + repair all system files |
| `sfc /verifyonly` | Scan, report only |
| `sfc /scanfile=C:\Windows\System32\file.dll` | Fix one file |
| `sfc /verifyfile=…` | Check one file |
| `sfc /offbootdir=C:\ /offwindir=C:\Windows` | Offline repair (recovery console) |

CBS.log: `C:\Windows\Logs\CBS\CBS.log` — filter: `findstr /c:"[SR]" CBS.log > sfcdetails.txt`.

### `DISM` — every subcommand (Admin)

Health & repair:

| Command | Meaning |
|---|---|
| `DISM /Online /Cleanup-Image /CheckHealth` | Quick flag check (seconds) |
| `DISM /Online /Cleanup-Image /ScanHealth` | Deep corruption scan (no fix) |
| `DISM /Online /Cleanup-Image /RestoreHealth` | Scan **and repair** (via Windows Update) |
| `… /RestoreHealth /Source:D:\sources\install.wim /LimitAccess` | Repair from install media (offline source) |
| `DISM /Cleanup-Mountpoints` | Fix stuck WIM mounts |

Component-store cleanup:

| Command | Meaning |
|---|---|
| `DISM /Online /Cleanup-Image /AnalyzeComponentStore` | Is WinSxS bloated? |
| `DISM /Online /Cleanup-Image /StartComponentCleanup` | Remove superseded components |
| `… /StartComponentCleanup /ResetBase` | Aggressive — afterwards updates can't be uninstalled |
| `… /SPSuperseded` | Remove old service-pack files |

Packages & features:

| Command | Meaning |
|---|---|
| `DISM /Online /Get-Packages` / `/Get-PackageInfo /PackageName:…` | List/inspect MSU packages |
| `DISM /Online /Add-Package /PackagePath:file.msu` | Install package |
| `DISM /Online /Remove-Package /PackageName:…` | Uninstall |
| `DISM /Online /Get-Features` | Optional features + state |
| `DISM /Online /Get-FeatureInfo /FeatureName:TelnetClient` | One feature |
| `DISM /Online /Enable-Feature /FeatureName:Microsoft-Windows-Subsystem-Linux /All /NoRestart` | Enable (+deps) |
| `DISM /Online /Disable-Feature /FeatureName:Printing-XPSServices-Features` | Disable |
| `DISM /Online /Get-Capabilities` · `/Add-Capability /CapabilityName:Language.Basic~en-GB~0.0.1.0` | Capabilities (FoD) |
| `DISM /Online /Export-Source /Source:D:\sources\install.wim` | Save a repair source |

Drivers:

| Command | Meaning |
|---|---|
| `DISM /Online /Get-Drivers` | All 3rd-party drivers (oemNN.inf) |
| `DISM /Online /Get-DriverInfo /Driver:oem14.inf` | Details |
| `DISM /Online /Add-Driver /Driver:C:\drv /Recurse` | Install all INFs in folder |
| `DISM /Online /Remove-Driver /Driver:oem14.inf` | Uninstall |
| `DISM /Online /Export-Driver /Destination:C:\drivers` | **Back up all 3rd-party drivers** |

Image (WIM/VHD/FFU) operations — used for deployment/repair images:

| Command | Meaning |
|---|---|
| `DISM /Get-WimInfo /WimFile:install.wim` | Editions/indexes inside WIM |
| `DISM /Mount-Image /ImageFile:install.wim /Index:1 /MountDir:C:\mnt /ReadOnly` | Mount |
| `DISM /Image:C:\mnt /Get-Packages` | Service the mounted (offline) image (same verbs + `/Image:`) |
| `DISM /Unmount-Image /MountDir:C:\mnt /Commit` / `/Discard` | Save/drop changes |
| `DISM /Remount-Image /MountDir:C:\mnt` | Recover a lost mount |
| `DISM /Apply-Image /ImageFile:install.wim /Index:1 /ApplyDir:D:\` | Apply to disk |
| `DISM /Capture-Image /ImageFile:cap.wim /CaptureDir:D:\ /Name:"Win11"` | Create WIM |
| `DISM /Capture-FFU` / `/Apply-FFU` | Full-flash images |
| `DISM /Export-Image` / `/Append-Image` / `/Split-Image /FileSize:3800` | Manage/extend WIMs (split for FAT32 USB) |

Common options for any DISM verb: `/Online` (running OS) or `/Image:path` (offline) · `/LogPath` · `/LogLevel:3` · `/ScratchDir:D:\temp`.

### Boot repair: `bcdedit`, `bcdboot`, `bootrec`

| Command | Meaning |
|---|---|
| `bcdedit` / `bcdedit /enum all` | Show boot store |
| `bcdedit /set {bootmgr} timeout 10` | Boot menu delay (s) |
| `bcdedit /default {current}` | Default OS entry |
| `bcdedit /copy {current} /d "Safe Mode Entry"` | Clone an entry |
| `bcdedit /set {guid} safeboot minimal` | Boot entry → Safe Mode (undo: `bcdedit /deletevalue {guid} safeboot`) |
| `bcdedit /set testsigning on` | Allow unsigned drivers (watermarks desktop) |
| `bcdedit /set nointegritychecks on` ⚠ | Disable signature checks |
| `bcdedit /set hypervisorlaunchtype off` | For nested VMs (VirtualBox w/ Hyper-V conflict) |
| `bcdedit /set {current} description "Windows 11 Main"` | Rename entry |
| `bcdedit /bootsequence {guid}` | One-time boot order |
| `bcdedit /export BCD.bak` / `/import BCD.bak` | Backup/restore store |
| `bcdedit /set bootmenupolicy legacy` | Classic F8 menu |
| `bcdboot C:\Windows /s S: /f UEFI` | **Rebuild boot files** on ESP S: (the UEFI fix) — `/f BIOS` for legacy |
| `bootrec /fixmbr` (recovery env) | Rewrite MBR (legacy BIOS) |
| `bootrec /fixboot` | New boot sector |
| `bootrec /scanos` | Find Windows installs not in the BCD |
| `bootrec /rebuildbcd` | Rebuild the store (add found installs) |
| `reagentc /info` / `/enable` / `/disable` | WinRE (recovery partition) state & repair |

### Restore points, backup, VSS (Admin)

| Command | Explanation |
|---|---|
| `vssadmin list shadows` | Restore points/snapshots |
| `vssadmin list shadowstorage` | Space used by VSS |
| `vssadmin list writers` | App VSS support state |
| `vssadmin list providers` | VSS providers |
| `vssadmin create shadow /for=C:` | Manual snapshot |
| ⚠ `vssadmin delete shadows /all /quiet` | Delete all snapshots (frees space) |
| `vssadmin resize shadowstorage /for=C: /on=C: /maxsize=10GB` | Cap VSS space |
| `wbadmin get versions` | Available backups |
| `wbadmin start backup -backupTarget:E: -include:C: -allCritical -quiet` | One-shot backup (Admin) |
| `wbadmin get items -version:MM/DD/YYYY-HHMM` | What's inside a backup |
| `wbadmin start recovery -version:… -itemtype:File -items:C:\Users\me\doc.txt -recoveryTarget:D:\restore` | Restore |
| `wbadmin start sysrecovery …` | Bare-metal recovery |
| `wbadmin delete catalog` | When catalog is corrupt |
| `rstrui` | GUI System Restore |
| `verifier /standard /all` | Driver Verifier on (crash-causing drivers reveal themselves) |
| `verifier /querysettings` / `/reset` | Check / turn off |
| `msconfig` | Boot/startup GUI |
| `cleanmgr /sageset:1` → `cleanmgr /sagerun:1` | Scripted Disk Cleanup presets |
| `gpupdate /target:computer /force` | Re-apply Group Policy now |
| `gpresult /r` | Applied policies summary (`/h report.html` full) |
| `openfiles query` / `openfiles disconnect /id:n` | Who has files open (*Admin*, needs `openfiles /local on` once) |

## 22. Shutdown & Power

### `shutdown` — every switch

| Command | Meaning |
|---|---|
| `shutdown /s /t 0` | Shut down now |
| `shutdown /s /t 600 /c "Upgrading in 10 min"` | Delayed with message |
| `shutdown /r /t 0` | Restart |
| `shutdown /r /o /t 0` | Restart → **Advanced startup menu** |
| `shutdown /g /t 0` | Restart + re-open registered apps |
| `shutdown /l` | Log off |
| `shutdown /h` | Hibernate |
| `shutdown /hybrid /t 0` | Hybrid shutdown (fast boot) |
| `shutdown /s /fw /t 0` | Shut down → firmware (UEFI) settings next boot |
| `shutdown /a` | **Abort** a pending shutdown |
| `shutdown /p` | Power-off without timeout/warning |
| `shutdown /e` | Document reason (event log) |
| `shutdown /s /m \\pc01 /t 0` | Remote shutdown (Admin) |
| `shutdown /r /m \\pc01 /f` | Remote restart, force apps closed |
| `shutdown /i` | GUI remote-shutdown dialog |
| `shutdown /d P:2:17` | Reason code: Planned:major:minor (list in `shutdown /?`) |
| `logoff` · `tsdiscon` | Session-level exits |

### `powercfg` — every subcommand (Admin for most)

| Command | Meaning |
|---|---|
| `powercfg /list` (`/l`) | Power schemes |
| `powercfg /getactivescheme` | Current one |
| `powercfg /setactive GUID` (`/s`) | Switch scheme |
| `powercfg /changename GUID Name` | Rename |
| `powercfg /duplicatescheme GUID` | Copy a scheme |
| `powercfg /delete GUID` (`/d`) | Remove scheme |
| `powercfg /restoredefaultschemes` | Reset all |
| `powercfg /query` (`/q`) | All settings of active scheme (subgroups: SUB_SLEEP, SUB_VIDEO…) |
| `powercfg /q SCHEME_CURRENT SUB_VIDEO VIDEOIDLE` | One setting |
| `powercfg /change monitor-timeout-ac 10` | Display off after 10 min (`standby-timeout-ac`, `disk-timeout-ac`, `hibernate-timeout-ac`; `-dc` = battery) |
| `powercfg /x monitor-timeout-dc 5` | Same thing (`/x` alias) |
| `powercfg /setacvalueindex SCHEME_CURRENT SUB_SLEEP STANDBYIDLE 1800` + `/setactive SCHEME_CURRENT` | Set raw index |
| `powercfg /setdcvalueindex …` | On battery |
| `powercfg /aliases` | All setting aliases |
| `powercfg /a` | Supported sleep states (S3? Modern Standby? Hibernate?) |
| `powercfg /h off` / `/h on` | Disable/enable hibernation (frees hiberfil.sys) |
| `powercfg /h /size 75` | Resize hiberfil (50–100%) |
| `powercfg /h /type full` | Hiberfile type — `full` or `reduced` |
| `powercfg /availablesleepstates` | Same as `/a` |
| `powercfg /lastwake` | What woke the PC |
| `powercfg /waketimers` | Scheduled wake-ups |
| `powercfg /devicequery wake_armed` | Devices allowed to wake |
| `powercfg /devicedisablewake "HID Keyboard"` | Forbid one |
| `powercfg /deviceenablewake "NIC"` | Allow one |
| `powercfg /requests` | What's **blocking** sleep right now |
| `powercfg /requestsoverride PROCESS app.exe DISPLAY` | Override blockers |
| `powercfg /batteryreport` | HTML battery health report (laptops) → `battery-report.html` |
| `powercfg /sleepstudy` | Modern-standby drain report |
| `powercfg /energy` | 60 s energy-efficiency audit → `energy-report.html` |
| `powercfg /systemsleepdiagnostics` | Sleep transition report |
| `powercfg /systempowerreport` | Power usage transitions |
| `powercfg /export scheme.pow GUID` / `/import scheme.pow` | Move schemes |

## 23. Event Logs — `wevtutil` & `eventcreate`

| Command | Meaning |
|---|---|
| `wevtutil el` | Enumerate all ~1000 logs |
| `wevtutil gli System` | Log info (size, created, last write) |
| `wevtutil qe System /c:10 /f:text /rd:true` | Last 10 System events, readable, newest first |
| `wevtutil qe System /f:text /q:"*[System[(EventID=41)]]" /c:5` | XPath filter |
| `wevtutil qe Security /q:"*[System[(EventID=4624)]]" /f:text /rd:true /c:20` | Logon events (Admin) |
| `wevtutil qe System /c:50 /rd:true /f:text \| findstr /i "error"` | Grep the log |
| `wevtutil epl System system.evtx` | Export .evtx (for sharing) |
| `wevtutil cl System` ⚠ | Clear a log (`/bu:backup.evtx` backs up first) |
| `wevtutil sl System /ms:1073741824` | Set max size 1 GB (`/e:true` enable) |
| `wevtutil ep` | Enumerate publishers |
| `wevtutil im manifest.xml` / `um` | (Un)install publisher manifest |
| `eventcreate /t error /id 999 /d "Batch job failed"` | Write a custom event to Application log |
| `eventcreate /l System /so "MyScript" /t warning /id 500 /d "x"` | Custom source+log |
| `eventvwr` | GUI |

## 24. Performance & Data Collector Sets

| Command | Explanation |
|---|---|
| `perfmon` / `perfmon /report` | GUI / 60 s diagnostic report |
| `resmon` | Resource Monitor |
| `typeperf "\Processor(_Total)\% Processor Time" -si 5 -sc 12` | Sample a counter every 5 s ×12 |
| `typeperf -qx PhysicalDisk` | **List all counters** (discover names) |
| `typeperf -cf counters.txt -si 10 -f csv -o log.csv` | Log a counter file |
| `logman query` | Existing data collector sets |
| `logman create counter Perf1 -c "\Processor(_Total)\% Processor Time" "\Memory\Available MBytes" -si 5 -o C:\log.blg -f bincirc -max 100 -v mmddhhmm` | Create collector |
| `logman start Perf1` / `logman stop Perf1` | Run/stop |
| `logman delete Perf1` | Remove |
| `logman create trace Trace1 -p "Windows Kernel Trace" -o trace.etl -nb 16 256 -bs 64` | ETW trace |
| `logman import DCS xml` / `export` | Share collector sets |
| `relog in.blg -f csv -o out.csv` | Convert binary log to CSV |
| `relog in.blg -t 5 -o decimated.blg` | Thin samples |
| `tracerpt trace.etl -o report.txt -of csv` | Turn ETW into something readable |
| `wmic path Win32_PerfFormattedData_PerfOS_Processor get PercentProcessorTime` | Sample CPU via WMI |

**Essential counters:** `\Processor(_Total)\% Processor Time` · `\Memory\Available MBytes` · `\PhysicalDisk(_Total)\% Disk Time` + `Avg. Disk Queue Length` · `\LogicalDisk(C:)\Free Megabytes` · `\Network Interface(*)\Bytes Total/sec` · `\System\Processor Queue Length`.

## 25. Remote Desktop & Terminal Services

| Command | Explanation |
|---|---|
| `mstsc` | RDP client GUI |
| `mstsc /v:pc01 /w:1600 /h:900` | Connect with size |
| `mstsc /v:pc01 /admin` | Session 0 (console) — server admin mode |
| `mstsc /public /v:pc01` | Public-network mode |
| `mstsc /span` / `/multimon` | Span monitors |
| `qwinsta` / `query session` | List sessions on this (or `/server:pc`) machine |
| `quser` / `query user` | Who's logged on where |
| `qprocess` / `query process` | Processes per session |
| `qappsrv` / `query termserver` | RDP servers on network |
| `msg %sessionname% "text"` | Message to a session |
| `logoff rdp-tcp#3` / `logoff 4` | Log off a session (local: `logoff`) |
| `tscon 2 /dest:console` | Hand session 2 to the physical console (GPU-mining/troubleshooting classic) |
| `tsdiscon` | Disconnect own session (apps keep running) |
| `tskill notepad` | Kill process in your session (`/id:4` per session) |
| `rwinsta 3` / `reset session 3` | Hard-reset a stuck session |
| `chgport` / `chglogon` / `chgusr` | COM-port map / RDP logons / TS execution mode |
| `shadow 3` (server) | View another session |

## 26. `certutil` — Certificates & More (Admin for store edits)

| Command | Meaning |
|---|---|
| `certutil -hashfile file.iso SHA256` | Checksum (MD2 MD4 MD5 SHA1 SHA256 SHA384 SHA512) |
| `certutil -hashfile file.exe MD5` | Quick MD5 |
| `certutil -encode in.bin out.b64` | File → base64 |
| `certutil -decode in.b64 out.bin` | base64 → file (poor man's attachment transport) |
| `certutil -dump cert.cer` | Inspect a certificate file |
| `certutil -store My` / `-user -store My` | Machine / user personal store |
| `certutil -store Root` | Trusted roots |
| `certutil -addstore Root newroot.cer` | Import CA cert |
| `certutil -delstore Root serial-or-name` | Remove |
| `certutil -verify cert.cer` | Chain validation |
| `certutil -verify -urlfetch cert.cer` | + check revocation URLs |
| `certutil -urlcache * delete` | Clear cached URL objects (fix weird fetch failures) |
| `certutil -pulse` | Trigger certificate autoenrollment |
| `certutil -template` | AD certificate templates |
| `certutil -ping` / `-pingadmin` | Test CA availability |
| `certutil -getkey serial` / `-recoverkey` | Key recovery |
| `certutil -setreg …` | Configure CA registry values |
| `certutil -v` | Verbose companion to any verb |
| `certreq -new request.inf cert.req` | Certificate request generation (CSR) |

## 27. Transfers — `bitsadmin`, `ftp` (all subcommands), `tftp`

### `bitsadmin` — background intelligent transfers

| Command | Meaning |
|---|---|
| `bitsadmin /transfer Job1 /download /priority normal http://host/file.zip C:\file.zip` | One-shot download |
| `bitsadmin /create Job1` | Create named job |
| `bitsadmin /addfile Job1 http://… C:\out.zip` | Add a file to job |
| `bitsadmin /resume Job1` / `/suspend Job1` | Start / pause |
| `bitsadmin /info Job1 /verbose` | Progress |
| `bitsadmin /list` / `/listallusers` | Jobs |
| `bitsadmin /complete Job1` | Finalize after transfer |
| `bitsadmin /cancel Job1` | Abandon |
| `bitsadmin /monitor` | Live refresh dashboard |
| `bitsadmin /cache /list` / `/cache /deleteurlstats` / `/cache /clear` | Cache management |
| PowerShell `Start-BitsTransfer url dest` | Friendlier wrapper (§P12) |

BITS survives disconnects and throttles itself — ideal for big/fragile downloads.

### `ftp` — every interactive subcommand

Connect: `ftp host` (or `open host` inside). Then:

| Sub | Meaning |
|---|---|
| `user name pass` | Re-login |
| `ls` / `dir` | List (short/long) |
| `cd /dir` / `cdup` | Change dir / up |
| `pwd` | Where am I |
| `lcd C:\local` | Change **local** directory |
| `type` | Show transfer mode |
| `ascii` / `binary` | Text / binary mode — **set `binary` before anything but text** |
| `get remote` / `get remote local` | Download |
| `put local` / `put local remote` | Upload |
| `rename a b` / `delete f` | Server-side ops |
| `mkdir d` / `rmdir d` | Server folders |
| `mget *.log` / `mput *.jpg` | Multi-file get/put |
| `mdelete *.tmp` | Multi delete |
| `prompt` | Toggle per-file confirmations (off for mget) |
| `hash` | Progress # marks |
| `glob` | Toggle wildcard expansion |
| `bell` | Beep per transfer |
| `verbose` | Toggle responses |
| `debug` | Command echoing |
| `sendport` | PORT vs PASV mode toggle |
| `literal CMD` / `quote CMD` | Send raw FTP protocol command (`literal PASV`) |
| `remotehelp` | Server's supported commands |
| `disconnect` / `close` | Close link, stay in ftp |
| `bye` / `quit` | Exit |
| `!command` | Run local shell command (`!dir`) |
| `?` / `help` | List commands |
| `append local remote` | Append upload |
| `recv` = get, `send` = put | Aliases |
| `mdir`/`mls remote local` | Remote listing to file |
| `status` | Session state |
| `trace` | Packet tracing |

`tftp -i host get file` — trivial FTP; optional feature, unencrypted, rarely appropriate; exists mostly for firmware updates.

## 28. Time — `w32tm` & `tzutil`

| Command | Meaning |
|---|---|
| `w32tm /query /status` | Sync state, source, offset |
| `w32tm /query /source` | Time source host |
| `w32tm /query /peers` | Peer list |
| `w32tm /query /configuration` | Full config |
| `w32tm /query /status /verbose` | Everything |
| `w32tm /resync` | Force resync now (`/nowait`, `/rediscover`) |
| `w32tm /config /manualpeerlist:"time.windows.com,0x8 pool.ntp.org,0x8" /syncfromflags:manual /reliable:yes /update` | Point at NTP servers |
| `w32tm /config /update` | Apply config |
| `net stop w32time & net start w32time` | Restart the service after config |
| `w32tm /stripchart /computer:time.google.com /samples:5 /dataonly` | Measure offset against a server |
| `w32tm /tzquery /iso8601` | Time-zone rules dump |
| `tzutil /g` | Current time-zone ID |
| `tzutil /s "W. Europe Standard Time"` | Set zone |
| `tzutil /l` | List all zones |
| `time /t` · `date /t` | Show time/date only |
| `time` · `date` | Interactive set (needs Admin) |

## 29. Software Deployment — `msiexec`, `pnputil`, `regsvr32`, `cscript`

### `msiexec` — all switch groups

| Form | Meaning |
|---|---|
| `msiexec /i app.msi` | Install |
| `msiexec /i app.msi /qn` | Silent, no UI |
| `msiexec /i app.msi /qb` | Basic UI only |
| `msiexec /i app.msi /qn INSTALLDIR="C:\App" ALLUSERS=1` | Pass public properties |
| `msiexec /x {GUID}` / `msiexec /x app.msi /qn` | Uninstall |
| `msiexec /a app.msi /qn TARGETDIR=C:\admin` | Administrative install (unpacked) |
| `msiexec /update patch.msp /qn` | Apply patch |
| `msiexec /p patch.msp /qn` | Patch standalone |
| `msiexec /f[vomusdp] {GUID}` | Repair: `v` re-run, `o` missing files, `m` machine, `u` user, `s` shortcuts, `d` defaults, `p` all |
| `msiexec /i app.msi /l*v install.log` | Verbose log (l: i/w/e/a/r/u/c/m/p/o + v/x specials) |
| `msiexec /j[u\|m] app.msi` | Advertise (per-user/machine) |
| `msiexec /qn /norestart …` | Never reboot — common codes: 0 ok, 3010 ok+reboot, 1603 fatal, 1618 another install running, 1635/1638 patch issues |

### Drivers & COM registration

| Command | Meaning |
|---|---|
| `pnputil /enum-devices /connected` | All live devices |
| `pnputil /enum-drivers` | 3rd-party driver store |
| `pnputil /add-driver C:\drv\nv.inf /install` | Install driver |
| `pnputil /add-driver C:\drv\*.inf /subdirs /install` | Whole tree |
| `pnputil /export-driver * C:\driverbackup` | Back up all drivers |
| `pnputil /delete-driver oem14.inf /uninstall /force` | Remove bad driver |
| `pnputil /scan-devices` | Rescan hardware |
| `pnputil /restart-device "USB\VID_1234&PID_5678\..."` | Restart one device |
| `pnputil /disable-device …` / `/enable-device …` | Toggle device |
| `regsvr32 shell.dll` | Register COM DLL (Admin) |
| `regsvr32 /u shell.dll` | Unregister |
| `regsvr32 /u /s tool.dll` | Silent unregister |
| `cscript //nologo script.vbs` | Run VBScript in console |
| `wscript script.vbs` | GUI host |
| `cscript //b //t:60 script.vbs` | Batch mode + 60 s timeout |

## 30. Console & Environment — full reference

| Command | Explanation |
|---|---|
| `set` | List all variables (`set p` filters) |
| `set VAR=value` | Set (session-only). **No spaces around `=`!** |
| `set VAR=` | Delete variable |
| `set /p VAR=Prompt: ` | Read input into variable |
| `set /a x=(5+3)*2` | Arithmetic: `+ - * / %%` and `& ^ << >>` bitwise, `!x` logical |
| `set /a rnd=%random% %% 100` | Random 0–99 |
| `setx VAR value` | Persist (user) — writes registry; ⚠ truncates to 1024 chars |
| `setx VAR value /m` | Persist machine-wide (Admin) |
| `path` | Show PATH |
| `path C:\tools;%path%` | Prepend for this session |
| `echo %PATH:;=&echo.%` | PATH one-per-line trick |
| `prompt $p$g` | Default prompt — codes: `$p` path `$g` > `$t` time `$d` date `$_` newline `$$` $ `$v` version |
| `title My Script` | Window title |
| `color 0a` | Colors `XY`: background/text (0-F); `color` alone resets |
| `chcp` / `chcp 65001` | Code page → UTF-8 (fixes accents) |
| `mode con cols=120 lines=40` | Window size |
| `doskey /history` | Session history |
| `doskey g=git status $*` | Macro: `g` runs git status, `$*` passes args |
| `doskey /macrofile=macros.txt` | Load macro file (persist via `AutoRun` reg key `HKCU\Software\Microsoft\Command Processor`) |
| `doskey /listsize=200` | History depth |
| `clip` | stdin → clipboard (`dir \| clip`) |
| `assoc` | Extension→filetype map |
| `assoc .txt` | One entry |
| `assoc .my=myfile` | Create |
| `ftype myfile="C:\app\app.exe" "%1"` | Which program runs a filetype |
| `where app` | Locate on PATH (§4) |
| `choice /c YN /m "Proceed"` | Wait for key → `errorlevel` 1/2 |
| `choice /c ABC /n /t 10 /d C /m "Pick"` | Hidden list, 10 s default C |
| `timeout /t 3 /nobreak` | Wait (§16) |
| `sort` (§4), `forfiles` (§4) | See deep tables above |
| `break` | Legacy — no-op (compatibility) |
| `verify on` / `verify off` | Verify disk writes flag |
| `ver` | Windows version |
| `vol C:` | Volume label + serial |
| `exit` / `exit /b N` | Close window / end script with code N |
| `cmd /v:on` | Launch child cmd with delayed expansion enabled |
| `start` | See §16 flag table |

## 31. GUI Tools Launched from CMD

**Management consoles (.msc)**

| Command | Opens |
|---|---|
| `compmgmt.msc` | Computer Management (everything in one) |
| `devmgmt.msc` | Device Manager |
| `diskmgmt.msc` | Disk Management |
| `services.msc` | Services |
| `eventvwr.msc` / `eventvwr` | Event Viewer |
| `gpedit.msc` | Group Policy Editor (Pro+) |
| `secpol.msc` | Local Security Policy (Pro+) |
| `lusrmgr.msc` | Local Users & Groups (Pro+) |
| `perfmon.msc` / `perfmon` | Performance Monitor |
| `fsmgmt.msc` | Shared Folders |
| `certmgr.msc` | Certificate Manager (user) |
| `certlm.msc` | Certificate Manager (machine) |
| `taskschd.msc` | Task Scheduler GUI |
| `wf.msc` | Firewall with Advanced Security |
| `dsa.msc` | AD Users & Computers (RSAT) |
| `azman.msc`, `tpm.msc`, `wmimgmt.msc` | Authorization Manager / TPM / WMI Control |

**Control Panel applets (.cpl) & `control` verbs**

| Command | Opens |
|---|---|
| `appwiz.cpl` | Programs & Features |
| `ncpa.cpl` | Network Connections |
| `sysdm.cpl` | System Properties |
| `inetcpl.cpl` | Internet Options |
| `powercfg.cpl` | Power Options |
| `timedate.cpl` | Date/Time |
| `intl.cpl` | Region |
| `mmsys.cpl` | Sound |
| `desk.cpl`†→`control desktop` | Display settings |
| `main.cpl` | Mouse |
| `control printers` | Devices & Printers |
| `control folders` | File Explorer options |
| `control update` / `control /name Microsoft.WindowsUpdate` | Windows Update |
| `control userpasswords2` | Advanced user accounts (autologon) |
| `control schedtasks` | Task Scheduler |
| `control admintools` | Administrative Tools |
| `control color` / `control keyboard` | Window colors / keyboard speed |
| `hdwwiz.cpl` | Hardware wizard |
| `wscui.cpl` | Security & Maintenance |
| `access.cpl`†→`control access`? use `utilman` | Accessibility |

**System dialogs & apps**

`winver` version · `msinfo32` system info · `taskmgr` Task Manager · `resmon` Resource Monitor · `regedit` registry · `cleanmgr` disk cleanup · `dfrgui` defrag GUI · `msconfig` boot config · `reliability` reliability history · `dxdiag` DirectX · `osk` on-screen keyboard · `narrator` · `magnify` · `snippingtool` · `ms-screenclip` · `calc` · `notepad` · `write` WordPad · `mspaint` Paint · `charmap` character map · `control fonts` fonts folder · `explorer` File Explorer · `desk.cpl`† · `optionalfeatures` Windows Features · `hdwwiz` · `printmanagement.msc` print mgmt · `wsreset` Store cache reset · `lpksetup` language packs · `sysprep` · `rekeywiz` EFS · `shrpubw` share wizard · `sdclt` backup · `systempropertiesadvanced` / `systempropertiesperformance` / `systempropertiesremote` direct dialogs · `powercfg.cpl` · `utilman` · `stikynot`† Sticky Notes · `wmplayer` · `ms-settings:windowsupdate` (any Settings page works via `ms-settings:`).

(*) Anything not on this list: type its executable name — if it's on PATH, it launches.

---
---

# PART 2 — POWERSHELL: THE COMPLETE CMDLET SET

## P1. PowerShell Crash Course — Objects, Pipeline, Discovery

**The core idea:** CMD commands exchange text; PowerShell commands (**cmdlets**, named `Verb-Noun`) exchange **objects**. `Get-Process` doesn't return text — it returns process objects carrying dozens of properties (CPU, memory, path…) and methods (`.Kill()`). The pipeline passes those objects whole, so you can filter, sort, and export **structured data** without parsing strings.

**Anatomy of a cmdlet:**

```powershell
Get-Process -Name chrome -ErrorAction SilentlyContinue | Sort-Object CPU -Descending
└── cmdlet   └─ parameter └ value  └ common parameter          └ pipes objects onward
```

**The discovery trio (learn these three, unlock everything):**

```powershell
Get-Command -Verb Get                    # every cmdlet with verb Get
Get-Command -Noun Service                # every cmdlet touching services
Get-Command -Module NetTCPIP             # everything in a module
Get-Help Get-Service -Examples           # usage examples
Get-Process | Get-Member                 # what properties/methods does this object have?
```

**Aliases:** `gci`=Get-ChildItem, `ls`/`dir`=Get-ChildItem, `cat`/`gc`=Get-Content, `sl`/`cd`=Set-Location, `gps`=Get-Process, `gsv`=Get-Service, `select`=Select-Object, `sort`=Sort-Object, `where`/`?`=Where-Object, `foreach`/`%`=ForEach-Object, `fl`=Format-List, `ft`=Format-Table, `iwr`=Invoke-WebRequest, `irm`=Invoke-RestMethod, `measure`=Measure-Object. Prefer full names in scripts.

**Comparison/logic operators:** `-eq -ne -gt -ge -lt -le` · strings: `-like` (wildcards) `-notlike -match` (regex) `-notmatch -in -notin -contains -notcontains` · logic: `-and`, `-or`, `-not` · case-sensitive variants prefix `c` (`-ceq`). `$null`, `$true`, `$false` built-ins.

**Pipeline variables:** `$_` (or `$PSItem`) = current object in the block.

**A worked pipeline (each stage commented):**

```powershell
Get-Process |                    # all process objects
  Where-Object CPU -gt 100 |     # keep CPU hogs
  Sort-Object CPU -Descending |  # biggest first
  Select-Object -First 5 Name, CPU, @{n='RAM(MB)';e={[int]($_.WS/1MB)}} |  # shape output + calculated property
  Format-Table -AutoSize         # pretty print
```

**Calling CMD from PowerShell** and vice versa: `ipconfig` works directly; `robocopy`, `netsh`, `sc` (→ use `sc.exe` — `sc` collides with Set-Content alias!) all run fine. From CMD: `powershell -Command "Get-Process"` or `pwsh -Command "…"`.

## P2. File System Cmdlets

| Cmdlet | Key usage |
|---|---|
| `Get-ChildItem` (`gci`) | `gci C:\ -Recurse -Filter *.log -ErrorAction SilentlyContinue` · `-Force` hidden · `-Depth 2` limits recursion · `-Include`/`-Exclude` (with `-Recurse` or `\*`) |
| `Get-Item` | One item (metadata): `(Get-Item file.txt).Length` |
| `Set-Location` (`cd`) | `cd ..` works; `cd C:\deep\path`; `cd -` returns to previous location ✨ |
| `Get-Location` (`pwd`) | Current path |
| `Push-Location` / `Pop-Location` | Directory stack (`pushd`/`popd` too) |
| `New-Item` | `-ItemType Directory\|File\|SymbolicLink\|HardLink\|Junction` + `-Name`/`-Path` + `-Value` (target for links) |
| `Copy-Item` | `Copy-Item C:\src D:\dst -Recurse -Force` |
| `Move-Item` | Move/rename |
| `Rename-Item` | `Rename-Item old.txt new.txt` (no path in new name) |
| `Remove-Item` ⚠ | `Remove-Item folder -Recurse -Force` · add `-WhatIf` to preview |
| `Invoke-Item` (`ii`) | Open in default handler (`ii report.html`) |
| `Test-Path` | Exists? True/False — supports wildcards: `Test-Path C:\data\*.zip` |
| `Resolve-Path` | Absolute path of relative |
| `Split-Path` | `Split-Path C:\a\b.txt -Leaf` → `b.txt` (`-Parent`, `-Extension`, `-Qualifier`) |
| `Join-Path` | `Join-Path C:\data "logs"` → `C:\data\logs` |
| `Convert-Path` | Resolve wildcards/PS paths to provider paths |
| `Get-Content` (`gc`) | `-TotalCount 20` first lines · `-Tail 20` last lines · `-Wait` follow (tail -f) · `-Raw` one string |
| `Set-Content` | Overwrite with text (`-Encoding UTF8`) |
| `Add-Content` | Append |
| `Clear-Content` | Empty a file, keep it |
| `Out-File` | Redirect pipeline to file: `… \| Out-File r.txt -Encoding utf8` (vs `>` which is UTF-16 in PS5.1) |
| `Tee-Object` | Show **and** save: `… \| Tee-Object log.txt` |
| `Get-ItemProperty` | File metadata (also registry values — see P10) |
| `New-Item -ItemType HardLink` | Link types without admin? hardlink/junction fine; SymbolicLink needs Admin/dev-mode |

## P3. Text & Data — CSV, JSON, XML, HTML

| Cmdlet | Key usage |
|---|---|
| `Select-String` | `Select-String -Path *.log -Pattern "ERROR" -SimpleMatch` · `-Regex` (default) · `-Context 2,3` lines around · `-List` first match per file |
| `Compare-Object` | `Compare-Object (gc a.txt) (gc b.txt)` — `<=` only-in-first, `=>` only-in-second |
| `Export-Csv` | `Get-Service \| Export-Csv services.csv -NoTypeInformation -Encoding UTF8` · `-Append` · `-Delimiter ";"` |
| `Import-Csv` | Rows become objects: `Import-Csv users.csv \| Where-Object Dept -eq IT` |
| `ConvertTo-Json` | `Get-Process -Name chrome \| ConvertTo-Json -Depth 3` |
| `ConvertFrom-Json` | `(irm api)\|ConvertFrom-Json` (irm already parses) — navigate: `$r.items[0].name` |
| `ConvertFrom-Json -AsHashtable` | pwsh 7: real hashtable |
| `ConvertTo-Html` | `Get-Service \| ConvertTo-Html -Property Name,Status > svc.html` |
| `ConvertTo-Xml` / `[xml]$x = Get-Content file.xml` | XML objects: `$x.config.setting` |
| `Import-Clixml`/`Export-Clixml` | PowerShell-native object serialization (even credentials with `-Depth`) |
| `Format-Hex` | Hex dump of file/bytes |
| `Write-Host / Write-Output / Write-Verbose / Write-Warning / Write-Error / Write-Information` | Output channels (see P14 guidance) |
| `Out-GridView` | `Get-Service \| Out-GridView -PassThru \| Restart-Service` — interactive picker! |
| `Group-Object` | `gci *.log \| Group-Object Extension \| Select Name,Count` |
| `Measure-Object` | `Import-Csv data.csv \| Measure-Object Amount -Sum -Average -Max` |

## P4. Objects, Pipeline & Formatting

| Cmdlet | Key usage |
|---|---|
| `Where-Object` | `Where-Object {$_.CPU -gt 100}` or simplified `Where-Object CPU -gt 100` |
| `ForEach-Object` | `ForEach-Object { $_.Name.ToUpper() }` · `-Begin`/`-End` · pwsh7 `-Parallel 8` |
| `Select-Object` | `-First` `-Last` `-Skip` `-Unique` `-ExpandProperty` `-Property` + calculated `@{n='…';e={…}}` |
| `Sort-Object` | `-Property A,{-property B} -Descending -Unique -Top 10` |
| `Measure-Object` | Count/sum/avg/min/max, also `-Line -Word -Character` on text |
| `Compare-Object` | Diff object sets (`-ReferenceObject`/`-DifferenceObject`, `-IncludeEqual`, `-SyncWindow`) |
| `Get-Member` (`gm`) | Inspect type/properties/methods: `gci \| gm` |
| `Format-Table` (`ft`) | `-AutoSize -Wrap` — always last in pipeline |
| `Format-List` (`fl`) | Everything vertically: `Get-Service spooler \| fl *` |
| `Format-Wide` (`fw`) | One property columns: `fw Name -Column 3` |
| `Format-Custom` | Nested structure view |
| `Out-String` | Convert formatted output back to text (`-Width 4096` to avoid truncation in logs) |
| `New-Object` | `New-Object -TypeName System.Version -ArgumentList "1.2.3"` |
| `.Where()` / `.ForEach()` | Method syntax: `(gci).Where({$_.PSIsContainer})` |
| `Select-Object -Unique` dedupe · `Sort-Object -Unique` | Removers |
| `Group-Object -NoElement` | Just the buckets |

> **Golden rule:** `Format-*` cmdlets destroy the objects for downstream use — always put them **last** (or use `Out-String` when you need text).

## P5. System Information & Hardware

| Cmdlet | Key usage |
|---|---|
| `Get-ComputerInfo` | Everything (slow first run; select: `Get-ComputerInfo os, bios`) |
| `Get-CimInstance` | **The wmic replacement.** `Get-CimInstance Win32_OperatingSystem \| fl` |
| Useful CIM classes | `Win32_OperatingSystem` (memory, install date) · `Win32_Processor` · `Win32_PhysicalMemory` · `Win32_BIOS` · `Win32_DiskDrive` · `Win32_LogicalDisk` (free space) · `Win32_NetworkAdapterConfiguration` · `Win32_Service` · `Win32_Process` (`CommandLine`!) · `Win32_Product` ⚠ slow/repair-triggering — use registry instead · `Win32_StartupCommand` · `Win32_UserAccount` · `Win32_Share` · `Win32_Printer` · `Win32_QuickFixEngineering` = `Get-HotFix` |
| `Get-HotFix` | Installed updates: `Get-HotFix \| Sort InstalledOn -Desc` |
| `Get-PSDrive` | All providers (FS, registry, env, cert…) |
| `Get-Volume` | Letters, sizes, health (`Get-Volume \| ft DriveLetter,FileSystemLabel,SizeRemaining`) |
| `Get-PhysicalDisk` | Health: `Get-PhysicalDisk \| ft FriendlyName,MediaType,HealthStatus` |
| `Get-Disk` | Disks + partition style |
| `Get-Date` | `Get-Date -Format "yyyy-MM-dd HH:mm"` · `(Get-Date).AddDays(-7)` |
| `Set-Date` | Change clock (Admin) |
| `Get-TimeZone` / `Set-TimeZone` | Time zone |
| `Get-Uptime` (pwsh7 / Win) | Since boot |
| `(Get-CimInstance Win32_OperatingSystem).LastBootUpTime` | Boot time in PS5.1 |
| `Get-WinEvent` | See P6 |
| `$env:` drive | `$env:PATH`, `$env:USERNAME` — set session: `$env:X="1"`; permanent: `[Environment]::SetEnvironmentVariable('X','1','Machine')` |
| `Get-Variable`/`Set-Variable`/`Clear-Variable` | Variable store tools |
| `Get-Command`, `Get-Help`, `Get-Member` | Discovery trio |
| `Test-Path`, `Get-Item` on env: | `Test-Path env:COMPUTERNAME` |

## P6. Processes, Services & Scheduled Tasks

| Cmdlet | Key usage |
|---|---|
| `Get-Process` (`gps`) | `gps chrome` · `gps \| Where CPU -gt 100` · include `-FileVersionInfo` for paths |
| `.Path` gotcha | `gps \| Select Path` needs access — use `Get-CimInstance Win32_Process \| Select ProcessId,CommandLine,ExecutablePath` |
| `Start-Process` | `-FilePath setup.exe -ArgumentList "/s" -Wait` · `-Verb RunAs` (elevate) · `-WindowStyle Hidden` · `-WorkingDirectory` |
| `Stop-Process` ⚠ | `-Name chrome -Force` · `-Id 1234` |
| `Wait-Process -Name installer` | Block until it exits |
| `Debug-Process -Name app` | Attach debugger |
| `Get-Service` (`gsv`) | `gsv \| Where Status -eq Stopped` · `gsv wuauserv` |
| `Start-Service` / `Stop-Service` / `Restart-Service` | `-Name spooler` · add `-PassThru` to see result |
| `Suspend-Service` / `Resume-Service` | Pausable services |
| `Set-Service` | `-Name x -StartupType Automatic\|Manual\|Disabled` · `-Description` (Admin) |
| `New-Service` | `-Name "MySvc" -BinaryPathName "C:\app\app.exe" -StartupType Auto` |
| `Remove-Service` (pwsh7+/Win10) | Delete service definition |
| `Get-ScheduledTask` | `Get-ScheduledTask \| Where State -ne Disabled` |
| `New-ScheduledTaskAction` | `-Execute "C:\script.bat"` |
| `New-ScheduledTaskTrigger` | `-Daily -At 22:00` · `-Weekly -DaysOfWeek Mon -At 9am` · `-Once -At (Get-Date).AddMinutes(10)` · `-AtLogon` · `-AtStartup` |
| `Register-ScheduledTask` ⚠ | `-TaskName "Nightly" -Action $a -Trigger $t -User SYSTEM -RunLevel Highest` |
| `Start-ScheduledTask -TaskName Nightly` | Run now |
| `Disable-/Enable-/Unregister-ScheduledTask` | Manage |
| `Get-ScheduledTaskInfo` | Last/next run results |
| `Get-WinEvent` | `Get-WinEvent -LogName System -MaxEvents 20` · `-FilterHashtable @{LogName='System';Level=2;StartTime=(Get-Date).AddDays(-1)}` · `FilterXPath` |
| `Get-EventLog` † | Legacy (Application/System/Security) |

## P7. Networking & Firewall

| Cmdlet | Key usage |
|---|---|
| `Get-NetIPConfiguration` | ipconfig's sane twin |
| `Get-NetIPAddress` | `-InterfaceAlias Wi-Fi` · `-AddressFamily IPv4` |
| `New-NetIPAddress` | `-InterfaceAlias Wi-Fi -IPAddress 192.168.1.50 -PrefixLength 24 -DefaultGateway 192.168.1.1` (Admin) |
| `Set-NetIPAddress` / `Remove-NetIPAddress` | Modify |
| `Get-NetAdapter` | Status/speed/MAC — `Get-NetAdapter \| ft Name,Status,LinkSpeed` |
| `Enable-NetAdapter` / `Disable-NetAdapter` | Toggle (Admin) |
| `Get-NetConnectionProfile` | Public vs Private network — `Set-NetConnectionProfile -InterfaceAlias Wi-Fi -NetworkCategory Private` |
| `Get-DnsClientServerAddress` | Resolvers per interface |
| `Set-DnsClientServerAddress` | `-InterfaceAlias Wi-Fi -ServerAddresses 1.1.1.1,8.8.8.8` |
| `Clear-DnsClientCache` | flushdns |
| `Resolve-DnsName` | `Resolve-DnsName x.com -Type MX` · `-Server 8.8.8.8` · `-DnsOnly` |
| `Test-Connection` | `Test-Connection 8.8.8.8 -Count 2` · `-Quiet` returns True/False |
| `Test-NetConnection` | Port+route: `Test-NetConnection host -Port 443` · `-TraceRoute` · `-InformationLevel Detailed` |
| `Get-NetTCPConnection` | `-State Listen` · `-LocalPort 8080` — combine with `Get-Process -Id $_.OwningProcess` |
| `Get-NetUDPEndpoint` | UDP table |
| `Get-NetRoute` / `New-NetRoute` / `Remove-NetRoute` | Routing table |
| `Get-NetFirewallRule` | `Get-NetFirewallRule -Enabled True -Direction Inbound` |
| `New-NetFirewallRule` | `-DisplayName "Web" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow -Profile Private` |
| `Set-NetFirewallRule` / `Disable-NetFirewallRule` / `Remove-NetFirewallRule` | Manage |
| `Get-NetFirewallProfile` / `Set-NetFirewallProfile` | `-Name Public -Enabled False` ⚠ |
| `Invoke-WebRequest` (`iwr`) | `iwr https://x/file.zip -OutFile file.zip` · `-UseBasicParsing` · `-Headers @{…}` · `-Method Post -Body $json` · `-Credential`/`-UseDefaultCredentials` |
| `Invoke-RestMethod` (`irm`) | API calls; JSON→objects automatically |
| `New-WebServiceProxy` | SOAP clients |
| `Send-MailMessage` | ⚠ legacy auth (basic SMTP) only |

## P8. Storage & SMB Shares

| Cmdlet | Key usage |
|---|---|
| `Get-Disk` / `Initialize-Disk` | `-Number 1 -PartitionStyle GPT` (Admin) |
| `New-Partition` | `-DiskNumber 1 -UseMaximumSize -DriveLetter E` |
| `Format-Volume` ⚠ | `-DriveLetter E -FileSystem NTFS -NewFileSystemLabel Data` (`exFAT`, `FAT32`) |
| `Get-Partition` / `Set-Partition` | `-DriveLetter E -NewDriveLetter F` |
| `Get-Volume` / `Repair-Volume` | `-DriveLetter C -Scan` (chkdsk) |
| `Optimize-Volume` | `-DriveLetter C -Defrag` (HDD) / `-ReTrim` (SSD) / `-Analyze` |
| `Clear-Disk` ⚠ | `-Number 1 -RemoveData` |
| `Get-PhysicalDisk` | `HealthStatus` — failing-drive early warning |
| `Get-StorageReliabilityCounter` | Temp/wear/read errors per disk: `Get-PhysicalDisk \| Get-StorageReliabilityCounter` |
| `New-VHD`/`Mount-VHD` (Hyper-V module) | Virtual disks |
| `New-SmbShare` | `-Name "Data" -Path "C:\Data" -FullAccess "Everyone"` (Admin) |
| `Get-SmbShare` / `Remove-SmbShare` | List/delete |
| `Grant-SmbShareAccess` / `Revoke-SmbShareAccess` | `-Name Data -AccountName bob -AccessRight Change` |
| `Get-SmbConnection` | Inbound share sessions |
| `Get-SmbOpenFile` / `Close-SmbOpenFile` | Who has what open |
| `Get-SmbMapping` / `New-SmbMapping` | `-LocalPath Z: -RemotePath \\srv\share` (net use) |
| `Set-SmbServerConfiguration` | Harden: `-EnableSMB1Protocol $false` |
| `Get-SmbServerConfiguration` | Current settings |

## P9. Users, Security & Credentials

| Cmdlet | Key usage |
|---|---|
| `Get-LocalUser` | All accounts |
| `New-LocalUser` | `-Name alice -Password (Read-Host -AsSecureString)` · `-FullName "Alice" -Description "x"` |
| `Set-LocalUser` | `-Name alice -Password $newpw` |
| `Disable-LocalUser` / `Enable-LocalUser` | Toggle |
| `Remove-LocalUser` | Delete |
| `Rename-LocalUser` | Rename |
| `Get-LocalGroup` / `New-LocalGroup` / `Remove-LocalGroup` | Groups |
| `Get-LocalGroupMember` | `-Group Administrators` |
| `Add-LocalGroupMember` / `Remove-LocalGroupMember` | `-Group Administrators -Member alice` |
| `Get-Acl`/`Set-Acl` | `Get-Acl C:\Data` — mutate via `.Access`, `.SetAccessRule()` |
| `New-Object System.Security.AccessControl.FileSystemAccessRule` | Build ACE: `(New-Object Security.AccessControl.FileSystemAccessRule("bob","FullControl","ContainerInherit,ObjectInherit","None","Allow"))` |
| `Get-ExecutionPolicy -List` / `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` | Script policy: Restricted→RemoteSigned (run local, signed remote)→AllSigned→Bypass |
| `Get-Credential` | `$c = Get-Credential` — prompt, secure |
| `New-Object System.Management.Automation.PSCredential` | Non-interactive: `New-Object PSCredential("u", (ConvertTo-SecureString "p" -AsPlainText -Force))` |
| `ConvertTo-SecureString` / `ConvertFrom-SecureString` | Encrypt secrets (DPAPI; `-Key` for shared) |
| `Start-Process -Verb RunAs` | Elevate from script |
| `sudo` ‡ | Real sudo ships with Windows 11 24H2+; elsewhere use RunAs/gsudo |
| `Unblock-File` | Remove Mark-of-the-Web: `Unblock-File script.ps1` |
| `Get-AuthenticodeSignature` | Verify signatures |
| `Set-ExecutionPolicy -Scope Process Bypass` | One-session unlock: `powershell -ExecutionPolicy Bypass -File script.ps1` |

## P10. Registry (PS drives)

| Cmdlet | Key usage |
|---|---|
| `cd HKLM:\SOFTWARE` | Registry as filesystem: `HKLM:` `HKCU:` `HKCR:` (mount: `New-PSDrive HKCR Registry HKEY_CLASSES_ROOT`) `HKU:` |
| `Get-Item` | One key: `Get-Item HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Run` |
| `Get-ItemProperty` | Values inside: `Get-ItemProperty HKLM:\…\Run` → `.Note` property access |
| `New-Item` / `New-ItemProperty` | `-Path HKCU:\Software\MyApp -Name Settings` / `-Path … -Name Port -Value 8080 -PropertyType DWord` (String, ExpandString, Binary, DWord, QWord, MultiString) |
| `Set-ItemProperty` | `-Path … -Name Port -Value 9090` |
| `Remove-Item` / `Remove-ItemProperty` | Delete key tree / one value |
| `Test-Path` | Key exists? |
| `reg` commands still fine | Same verbs as §20 |

## P11. Remoting & Background Jobs

| Cmdlet | Key usage |
|---|---|
| `Enable-PSRemoting -Force` | One-time setup on target (Admin) — WinRM |
| `Set-Item WSMan:\localhost\Client\TrustedHosts -Value "pc01,pc02" -Force` | Trust workgroup machines (then `Restart-Service WinRM`) |
| `Enter-PSSession -ComputerName pc01 -Credential dom\admin` | Interactive remote shell — `Exit-PSSession`/`exit` |
| `Invoke-Command -ComputerName pc01,pc02 -ScriptBlock { Get-Service }` | Fan-out one-to-many |
| `Invoke-Command … -ThrottleLimit 32 -AsJob` | Parallel background |
| `New-PSSession` | Persistent session (avoid re-auth cost): `$s = New-PSSession pc01` |
| `Invoke-Command -Session $s { … }` | Reuse it |
| `Copy-Item -ToSession $s C:\f.zip C:\dest\` / `-FromSession` | File transfer over WinRM |
| `Enter-PSSession -HostName user@pc01` (pwsh 7) | **SSH transport** — no WinRM needed |
| `Disconnect-PSSession` / `Connect-PSSession` | Survive network drops |
| `Get-PSSession` / `Remove-PSSession` | Manage |
| `Start-Job -ScriptBlock { … }` | Local background job |
| `Get-Job` / `Receive-Job -Id 3 -Keep` | Status / fetch output (`-Keep` to re-read) |
| `Wait-Job` / `Stop-Job` / `Remove-Job` | Lifecycle |
| `Start-ThreadJob` | Lightweight in-process jobs (module ThreadJob) |
| `Register-PSSessionConfiguration` | Endpoint hardening (runas, restricted) |
| `winrs -r:pc01 cmd` | Cmd-line alternative |
| `psexec \\pc01 cmd` | Sysinternals fallback |

## P12. Modules & Packages (incl. `winget` — every subcommand)

| Cmdlet | Key usage |
|---|---|
| `Get-Module -ListAvailable` | Everything installed |
| `Import-Module Name` | Load |
| `Get-Command -Module Name` | What did it give me? |
| `Find-Module` | Search PSGallery: `Find-Module -Tag vmware` |
| `Install-Module` | `-Name 7Zip4Powershell -Scope CurrentUser` (accept `-Force`) |
| `Update-Module` / `Uninstall-Module` / `Save-Module` | Lifecycle |
| `Install-PSResource` etc. (PSResourceGet, new) | `Register-PSResourceRepository`, faster gallery |
| `Publish-Module` | Share your own |
| `$PROFILE` | Your startup script path (see P14) |

**`winget` (Windows Package Manager) — full subcommand table**

| Subcommand | Purpose · key options |
|---|---|
| `winget search term` | Find packages (`-s winget\|msstore`, `--tag`, `--name`, `--id`, `--moniker`) |
| `winget show App` | Package details, versions, installer type (`App` = name or `--id`, `-e` exact) |
| `winget install App` | Install: `-e --id Git.Git` · `--version 1.2.3` · `--silent/-h` · `--interactive/-i` · `--scope user\|machine` · `--architecture x64` · `--override "ARGS"` (custom installer flags) · `--location C:\x` · `-o/--options` passthrough · `--accept-package-agreements --accept-source-agreements` |
| `winget upgrade` | List updates; `winget upgrade --all` · `--include-unknown` · `App` to update one |
| `winget list` | Installed software (all sources + Windows) — great inventory |
| `winget uninstall App` | `-e --id …` · `--version` · `--silent` |
| `winget hash file` | Installer hash for manifest authoring |
| `winget validate manifest.yaml` | Validate a manifest |
| `winget source list/add/update/reset/remove/export` | Manage repositories (`winget source add -n X -u https://… -t Rest`) |
| `winget export -o apps.json` / `winget import -i apps.json` | Machine-to-machine app sync (`--include-versions`) |
| `winget download App` | Download without installing (`--download-directory`) |
| `winget configure file.dsc.yaml` | Apply WinGet configuration (declarative machine setup) |
| `winget settings` | Editor for settings.json (progress bar, colors, telemetry) |
| `winget features` | Feature flags (e.g. `winget features enable proxy`) |
| `winget complete` | Shell completion setup |

Common flags on many verbs: `-e/--exact`, `--id`, `--name`, `--moniker`, `-s/--source`, `--versions`, `--accept-source-agreements`, `--wait`, `--logs`, `--verbose-logs`.

## P13. Maintenance & Power

| Cmdlet | Key usage |
|---|---|
| `Restart-Computer -Force` | `-ComputerName pc01` remote |
| `Stop-Computer -Force` | Shutdown |
| `shutdown.exe /s /t 0` | When you need its extra switches |
| `Clear-RecycleBin -Force` | Empty bin |
| `Checkpoint-Computer -Description "Before X"` | Restore point |
| `Enable-ComputerRestore -Drive C:\` | Turn System Restore on |
| `Get-ComputerRestorePoint` / `Restore-Computer -RestorePoint 3` | List / roll back |
| `Repair-Volume -DriveLetter C -Scan` | chkdsk |
| `Optimize-Volume -DriveLetter C -Defrag/-ReTrim` | Defrag/TRIM |
| `sfc /scannow` · `Repair-WindowsImage -Online -RestoreHealth` | System-file repair (the cmdlet is the DISM-module version; on client Windows just call `DISM.exe`) |
| `Get-WindowsUpdateLog` | Convert ETL to readable update log |
| `Enable-BitLocker -MountPoint C: -RecoveryPasswordProtector -TpmProtector` | Encrypt (Admin) · `Get-BitLockerVolume` · `Backup-BitLockerKeyProtector` (to AD) · `Suspend-BitLocker`/`Resume-BitLocker` |
| `Measure-Command { … }` | Benchmark anything |
| `Get-ComputerInfo` | Section P5 |

## P14. PowerShell Scripting — Zero to Advanced

**Variables & types:** `$n = 42` (int) · `$s = "hi"` (string) · `$d = 3.14` (double) · cast: `[int]"5"` · `[datetime]"2026-01-01"` · `"has $(2+3) interpolation"` · format: `"{0:N2}" -f 1234.5678`.

**Arrays & hashtables:** `$a = 1,2,3` or `@(1,2,3)` · `$a[0]`, `$a[-1]`, `$a[1..2]`, `$a += 4` (slow — prefer `$a = [System.Collections.Generic.List[int]]::new(); $a.Add(4)`) · `$h = @{name="bob"; age=30}` · `$h.name`, `$h["age"]`, iterate `.Keys`.

**Flow control:**

```powershell
if ($x -gt 10) { "big" } elseif ($x -gt 5) { "mid" } else { "small" }

switch ($day) { 6 {"Sat"} 7 {"Sun"} default {"Weekday: $_"} }
switch -Wildcard ($file) { "*.log" {"log"} "*.txt" {"text"} }

foreach ($p in Get-Process) { $p.Name }        # statement (faster)
Get-Process | ForEach-Object { $_.Name }        # pipeline (streaming)
1..10 | ForEach-Object { $_ * $_ }
for ($i=0; $i -lt 5; $i++) { $i }
while ($c -lt 3) { $c++ }
do { $c++ } until ($c -ge 3)
break / continue / continue label:
```

**Functions & advanced parameters:**

```powershell
function Get-FreeSpace {
    [CmdletBinding()]                               # enables -Verbose, -WhatIf, common params
    param(
        [Parameter(Mandatory, ValueFromPipeline)]   # can pipe volumes in
        [string[]]$Drive = @('C'),
        [ValidateRange(0,100)][int]$WarnBelow = 10
    )
    process {
        foreach ($d in $Drive) {
            $v = Get-Volume -DriveLetter $d
            $pct = [math]::Round($v.SizeRemaining/$v.Size*100,1)
            if ($pct -lt $WarnBelow) { Write-Warning "$d at $pct%" }
            [pscustomobject]@{Drive=$d; FreeGB=[math]::Round($v.SizeRemaining/1GB,1); Pct=$pct}
        }
    }
}
Get-FreeSpace C, D -Verbose
```

Parameter attributes to know: `[Parameter(Mandatory)]`, `ValueFromPipeline(ByPropertyName)`, `Position=0`, `HelpMessage` · validation: `[ValidateSet('a','b')]`, `[ValidateRange(1,10)]`, `[ValidateNotNullOrEmpty()]`, `[ValidateScript({Test-Path $_})]` · `[OutputType([string])]`.

**Error handling:**

```powershell
try   { Get-Content C:\maybe\missing.txt -ErrorAction Stop }
catch { Write-Warning "failed: $($_.Exception.Message)" }
finally { "always runs" }

$Error.Clear(); $Error[0]           # inspect last error
$ErrorActionPreference = 'Stop'    # session-wide strictness
trap { "caught $_"; continue }     # legacy style
```

**Files, text & regex:** `-replace 'a','b'` (regex) · `-split ','` · `-join` · `-match 'p'` sets `$matches[]` · `-like '*x*'` wildcards · verbatim strings `'$x'` vs interpolated `"$x"` · here-strings:

```powershell
@"
line one
line two
"@
```

**Comment-based help & pragmas:**

```powershell
<#
.SYNOPSIS
  One-liner.
.DESCRIPTION
  More detail.
.PARAMETER Drive
  Letters to check.
.EXAMPLE
  Get-FreeSpace C, D
#>
#Requires -Version 7
#Requires -RunAsAdministrator
```

**Script structure:** `param()` block first → `#requires` above it → functions → `main`. Call operators: `& "C:\path\script.ps1" -Arg 1` (string paths need `&`) · `. .\lib.ps1` **dot-source** functions into scope.

**pwsh 7 goodies:** ternary `$x = $a -gt 5 ? "big" : "small"` · null-coalescing `$name ?? "default"` · chain `cmd1 && cmd2` / `cmd1 || cmd2` · `ForEach-Object -Parallel` · `ConvertFrom-Json -AsHashtable` · pipeline chain operators · `??=` assign-if-null.

**Profiles:** `$PROFILE` → `notepad $PROFILE` — put aliases/functions there; `$PROFILE.CurrentUserAllHosts` applies everywhere; machine-wide: `C:\Windows\System32\WindowsPowerShell\profile.ps1` ⚠.

**Best practices checklist**
1. Full cmdlet names in scripts (no aliases).
2. `Set-StrictMode -Version Latest` at top of scripts (catch typos).
3. Prefer `-ErrorAction Stop` inside `try/catch`.
4. Never `Write-Host` data — use output objects; `Write-Host` only for direct-to-user color text.
5. Output objects, not formatted text; `Format-*` last.
6. Use `-WhatIf`/`-Confirm` support (`[CmdletBinding(SupportsShouldProcess)]`).
7. Quote variable expansions with subscripts: `"${folder}\file"`.
8. Avoid `Invoke-Expression`; use `&`.
9. Sign or review downloaded scripts: `Get-AuthenticodeSignature`, `Unblock-File`.
10. Lint with PSScriptAnalyzer (`Invoke-ScriptAnalyzer .\script.ps1`).

---
---

# PART 3 — HANDS-ON TUTORIALS

## T1. CMD Basics — Your First Hour

**Goal:** total comfort with navigating and manipulating files without Explorer.

```bat
:: 1 — Where am I? What's here?
cd                          & :: prints C:\Users\you
dir                         & :: look around
dir /a                      & :: including hidden
dir /o:-s                   & :: biggest files first

:: 2 — Build a practice tree under C:\Lab
cd \                        & :: root of C:
mkdir Lab                   & :: create
cd Lab
mkdir Docs Work Archive
cd Docs
echo Meeting notes > notes.txt
echo v1 >> notes.txt
type notes.txt              & :: verify content

:: 3 — Copy, rename, move (the daily trio)
copy notes.txt ..\Archive\notes-v1.txt
cd ..\Archive
ren notes-v1.txt 2026-01-notes.txt
move 2026-01-notes.txt ..\Work\
cd ..\Work
dir

:: 4 — Inspect like a pro
tree ..\ /f
dir ..\ /s /b               & :: every file, full paths
fc notes.txt ..\Docs\notes.txt   & :: compare copies

:: 5 — Search
findstr /i /n "v1" notes.txt
where /r C:\Lab *.txt

:: 6 — Clean up safely
cd C:\Lab
del Work\notes.txt          & :: confirm Y if prompted
rd Work                     & :: only because it's empty now
```

**Checkpoint:** you can go anywhere (`cd`, `pushd`), see anything (`dir /s /b`, `tree /f`), and reorganize safely.

## T2. File-Management Mastery

**A. Copy a whole project, excluding junk:**

```bat
robocopy C:\Projects\Site D:\Backups\Site /e /xf *.tmp *.log /xd node_modules .git /r:1 /w:1
echo Exit code: %errorlevel%   & :: 0-7 good, 8+ bad
```

**B. “Sync” two folders (mirror — destination is made identical!):**

```bat
robocopy C:\Data D:\Mirror /mir /l /np /tee      & :: PREVIEW first (/l)!
robocopy C:\Data D:\Mirror /mir /np /log+:mirror.log
```

**C. Incremental daily copy (only files changed in last 24 h):**

```bat
robocopy C:\Data \\NAS\Backup /e /maxage:1 /r:1 /w:1 /tee
```

**D. Delete all `.tmp` older than 30 days, everywhere under C:\Users:**

```bat
forfiles /p C:\Users /s /m *.tmp /d -30 /c "cmd /c echo deleting @path"
:: happy with the list? then:
forfiles /p C:\Users /s /m *.tmp /d -30 /c "cmd /c del @path"
```

**E. Find the 20 biggest files on a drive:**

```bat
dir C:\ /s /b /a:-d 2>nul ^| sort /r > allfiles_tmp.txt
for /f "delims=" %%F in (allfiles_tmp.txt) do @echo %%~zF %%F
:: or simply, sorted by size, folders only summary:
dir C:\ /s /o:-s | findstr /r /c:"^[0-9]" | more
```

**F. Verify a big copy with hashes:**

```bat
certutil -hashfile D:\Mirror\big.zip SHA256
certutil -hashfile C:\Data\big.zip SHA256
fc hash1.txt hash2.txt
```

## T3. Write a Real Batch Backup Script

Create `C:\Scripts\backup.bat` — annotated line by line:

```bat
@echo off
setlocal enabledelayedexpansion
:: =====================================================
::  backup.bat — daily mirror with 7-day rotation
::  usage: backup.bat [source] [destination]
:: =====================================================

:: --- 1. Arguments with defaults
set "SRC=%~1" & if "%SRC%"=="" set "SRC=C:\Data"
set "DST=%~2" & if "%DST%"=="" set "DST=D:\Backups"

:: --- 2. Timestamp (locale-independent-ish: use WMIC date)
for /f "tokens=2 delims==" %%I in ('wmic os get localdatetime /value ^| find "="') do set dt=%%I
set "STAMP=%dt:~0,4%-%dt:~4,2%-%dt:~6,2%_%dt:~8,2%%dt:~10,2%"
set "TODAY=%DST%\%STAMP%"

title Backup %SRC% -^> %TODAY%
echo [%time%] Starting backup of %SRC%

:: --- 3. Sanity checks
if not exist "%SRC%" (
    echo [ERROR] Source "%SRC%" not found & exit /b 2
)
net session >nul 2>&1 || echo [WARN] not elevated — OK for user folders

:: --- 4. The copy (mirror, 1 retry, log everything)
robocopy "%SRC%" "%TODAY%" /mir /mt:8 /r:1 /w:1 /np /tee /log+:"%DST%\backup.log"
set RC=%errorlevel%

:: --- 5. Interpret robocopy's code
if %RC% GEQ 16 (echo [FATAL] copy failed & exit /b 16)
if %RC% GEQ 8  (echo [ERROR] some files failed & exit /b 8)
echo [OK] copied with code %RC%

:: --- 6. Rotation: keep newest 7 folders
set /a kept=0
for /f "delims=" %%D in ('dir /b /ad /o:-n "%DST%\20*" 2^>nul') do (
    set /a kept+=1
    if !kept! GTR 7 (
        echo [ROTATE] removing %%D
        rd /s /q "%DST%\%%D"
    )
)

:: --- 7. Optional: flag success in Event Log
eventcreate /t information /id 700 /d "Backup %STAMP% OK (rc=%RC%)" >nul

echo [%time%] Done. Exit code %RC%
endlocal & exit /b %RC%
```

Schedule it (T6), then test: `backup.bat`, then `backup.bat "C:\Lab" "D:\LabBackups"`.

**What this teaches:** arguments (`%~1`), defaults, `wmic` timestamps, `if`/`for`, delayed expansion (`!kept!`), errorlevel logic, rotation, logging, event logging.

## T4. Network Troubleshooting Walkthrough

Symptom: *“My internet is slow / some sites don't load.”* Run in order — each step isolates a layer.

```bat
:: 1. Link & address ok?
ipconfig /all
::    look: adapter up? IP 192.168.x.x (not 169.254.x.x = DHCP failure!)
::    DHCP failure → ipconfig /release & ipconfig /renew

:: 2. Reach the router?
ping 192.168.1.1 -n 4
::    loss/high ms = Wi-Fi/LAN problem, not the internet

:: 3. Reach the internet by IP?
ping 8.8.8.8 -n 4
::    router ok but this fails → ISP/router WAN issue

:: 4. DNS working? (name resolution)
nslookup example.com
nslookup example.com 8.8.8.8
::    works with 8.8.8.8 but not default → your DNS server is the problem
ipconfig /flushdns

:: 5. Where does it break? (path analysis)
tracert -d example.com
pathping -n example.com          :: loss% per hop over time

:: 6. Something saturating the line / weird connections?
netstat -ano | findstr ESTABLISHED
::    map PID → program:
tasklist /fi "PID eq 4321"

:: 7. Nuclear reset (fixes most software stacks)
netsh winsock reset
netsh int ip reset
ipconfig /flushdns
shutdown /r /t 0

:: 8. Port-level checks (e.g. is my web server reachable?)
curl -I https://example.com
powershell -Command "Test-NetConnection example.com -Port 443 -InformationLevel Detailed"
```

Decision table: fails at 2 → local network · fails at 3 → ISP · fails at 4 → DNS · fails at 5 hop N → that router · slow only at 6 → bandwidth hog.

## T5. `diskpart` — Format a USB Drive & Change Letters

⚠ **Everything here is destructive. Check disk size twice.**

```bat
diskpart                    :: Admin
list disk                   :: identify USB by SIZE (say Disk 2, 32 GB)
select disk 2               :: never guess — verify!
detail disk                 :: confirm it's really the USB

:: --- path A: fresh FAT32/exFAT stick
clean
create partition primary
format fs=exfat label="USB" quick
assign
exit
```

```text
:: --- path B: USB stick stuck "write-protected"
select disk 2
attributes disk clear readonly
clean
create partition primary
format fs=fat32 quick
assign
```

**Change a drive letter (any disk):**

```text
list volume
select volume 4
assign letter=Z
:: or remove:  remove letter=E
:: or mount into a folder instead of a letter:
assign mount=C:\Mounts\Data
```

**Convert an empty disk MBR→GPT (for >2 TB or UEFI):**

```text
select disk 1
convert gpt
create partition primary
format fs=ntfs label="BigData" quick
assign letter=E
```

Scriptable version — save as `usb.txt`, run `diskpart /s usb.txt`:

```text
select disk 2
clean
create partition primary
format fs=exfat label=USB quick
assign
exit
```

## T6. Automate Anything with Task Scheduler

Take T3's backup and make it run nightly at 22:00, as SYSTEM, whether you're logged on or not:

```bat
schtasks /create ^
  /tn "NightlyBackup" ^
  /tr "C:\Scripts\backup.bat" ^
  /sc daily /st 22:00 ^
  /ru SYSTEM /rl HIGHEST /f
```

Verify and control:

```bat
schtasks /query /tn "NightlyBackup" /v /fo list
schtasks /run    /tn "NightlyBackup"        :: don't wait for 22:00
schtasks /end    /tn "NightlyBackup"
schtasks /change /tn "NightlyBackup" /st 23:00 /disable
schtasks /change /tn "NightlyBackup" /enable
schtasks /delete /tn "NightlyBackup" /f
```

Common patterns:

```bat
:: every 15 minutes
schtasks /create /tn "Sync" /tr "C:\s.bat" /sc minute /mo 15
:: at logon of any user
schtasks /create /tn "Welcome" /tr "msg * hi" /sc onlogon
:: monthly, 1st day, 09:30
schtasks /create /tn "Report" /tr "C:\r.bat" /sc monthly /d 1 /st 09:30
:: weekly Fri 17:00
schtasks /create /tn "Weekend" /tr "C:\w.bat" /sc weekly /d FRI /st 17:00
```

PowerShell variant (richer triggers):

```powershell
$a = New-ScheduledTaskAction -Execute "C:\Scripts\backup.bat"
$t = New-ScheduledTaskTrigger -Daily -At 22:00
Register-ScheduledTask -TaskName "NightlyBackup" -Action $a -Trigger $t -User SYSTEM -RunLevel Highest -Force
```

Audit what failed: `schtasks /query /fo csv /v | findstr /i "nightly"` → Last Result `0` = success, `0x1` = generic failure (script bug), `0xC0000135` = missing DLL/interpreter.

## T7. Repair a Broken Windows Boot / System Files

Do these **in order** — cheap checks first, invasive last. Each step from an **Admin** prompt (or WinRE → Troubleshoot → Command Prompt for steps marked *offline*).

```bat
:: 1 — File system health
chkdsk C: /scan                 :: online, read-only
chkdsk C: /f                    :: schedule fix at reboot → reboot
:: Y at the prompt, reboot, watch 3 stages

:: 2 — System file integrity
sfc /scannow
findstr /c:"[SR]" %windir%\Logs\CBS\CBS.log > %USERPROFILE%\Desktop\sfc.txt

:: 3 — Component store (only if sfc found unfixable corruption)
DISM /Online /Cleanup-Image /CheckHealth
DISM /Online /Cleanup-Image /ScanHealth
DISM /Online /Cleanup-Image /RestoreHealth
:: no internet? use install media:
DISM /Online /Cleanup-Image /RestoreHealth /Source:D:\sources\install.wim /LimitAccess

:: 4 — Boot files (UEFI)
bcdedit                         :: can it read the store?
mountvol S: /s                  :: mount the EFI partition as S:
bcdboot C:\Windows /s S: /f UEFI
mountvol S: /d

:: 5 — Boot record (legacy BIOS machines; from WinRE)
bootrec /fixmbr
bootrec /fixboot
bootrec /scanos
bootrec /rebuildbcd

:: 6 — Safe Mode toggle (if you can boot)
bcdedit /set {current} safeboot minimal
shutdown /r /t 0
:: after fixing:
bcdedit /deletevalue {current} safeboot

:: 7 — WinRE itself broken?
reagentc /info
reagentc /disable & reagentc /enable
```

Rule of thumb: **chkdsk** fixes disks · **sfc** fixes Windows files · **DISM** fixes the thing that fixes Windows files · **bcdboot/bootrec** fix booting. If sfc can't repair, run DISM first, then sfc again.

## T8. PowerShell — Build a System Report Script

Goal: one script that produces an HTML health report. Build it in steps at a live prompt, then save as `report.ps1`.

```powershell
# --- Step 1: explore the objects you'll use
Get-CimInstance Win32_OperatingSystem | Select Caption, Version, LastBootUpTime,
    TotalVisibleMemorySize, FreePhysicalMemory
Get-CimInstance Win32_LogicalDisk -Filter "DriveType=3"
Get-Process | Sort CPU -Descending | Select -First 5 Name, CPU, @{n='RAM_MB';e={[int]($_.WS/1MB)}}

# --- Step 2: compute derived values
$os   = Get-CimInstance Win32_OperatingSystem
$up   = (Get-Date) - $os.LastBootUpTime
$disk = Get-CimInstance Win32_LogicalDisk -Filter "DriveType=3" |
        Select DeviceID,
            @{n='FreeGB';e={[math]::Round($_.FreeSpace/1GB,1)}},
            @{n='TotalGB';e={[math]::Round($_.Size/1GB,1)}},
            @{n='Free%';e={[math]::Round($_.FreeSpace/$_.Size*100,1)}}

# --- Step 3: gather the rest
$top     = Get-Process | Sort CPU -Descending | Select -First 5 Name, CPU,
              @{n='RAM_MB';e={[int]($_.WS/1MB)}}
$stopped = Get-Service | Where {$_.StartType -eq 'Automatic' -and $_.Status -ne 'Running'}
$errors  = Get-WinEvent -FilterHashtable @{LogName='System';Level=2} -MaxEvents 10 `
              -ErrorAction SilentlyContinue |
           Select TimeCreated, Id, ProviderName, @{n='Msg';e={$_.Message.Substring(0,80)}}

# --- Step 4: assemble the HTML
$html = @"
<html><body style='font-family:Segoe UI'>
<h1>System Report - $env:COMPUTERNAME</h1>
<p>Generated $(Get-Date) &middot; Uptime $([int]$up.TotalDays)d $up.hh\:mm</p>
<h2>Disks</h2> $($disk | ConvertTo-Html -Fragment)
<h2>Top CPU</h2> $($top | ConvertTo-Html -Fragment)
<h2>Auto-services not running</h2> $($stopped | ConvertTo-Html -Fragment)
<h2>Last 10 System errors</h2> $($errors | ConvertTo-Html -Fragment)
</body></html>
"@
$html | Out-File "$env:USERPROFILE\Desktop\report.html" -Encoding utf8
Invoke-Item "$env:USERPROFILE\Desktop\report.html"
```

Run it: `powershell -ExecutionPolicy Bypass -File .\report.ps1`. Enhancements to try: `Get-NetIPAddress`, `Get-PhysicalDisk | Get-StorageReliabilityCounter`, email via `Send-MailMessage`, or a scheduled daily run (T6).

## T9. Security Hardening in 15 Commands

Run from an **Admin** prompt; read each before running.

```powershell
# 1. Firewall on, everywhere
Set-NetFirewallProfile -All -Enabled True

# 2. Set the current network to Private (blocks file sharing from public nets)
Set-NetConnectionProfile -NetworkCategory Private

# 3. Kill SMBv1 (WannaCry's door)
Set-SmbServerConfiguration -EnableSMB1Protocol $false -Force
Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol -NoRestart

# 4. Show + delete saved credentials
cmdkey /list
cmdkey /list | findstr /i "target"      # review… then:
cmdkey /delete:TERMSRV/server01

# 5. Disable the lazy autologon
control userpasswords2        # or: net user administrator /active:no

# 6. Audit failed logons
auditpol /set /subcategory:"Logon" /failure:enable

# 7. Require strong passwords locally
net accounts /minpwlen:12 /maxpwage:90 /lockoutthreshold:5 /lockoutduration:30

# 8. See who can log on remotely (RDP group)
Get-LocalGroupMember -Group "Remote Desktop Users"

# 9. Find world-writable shares and fix one
Get-SmbShare
Grant-SmbShareAccess -Name Data -AccountName Everyone -AccessRight Read   # downgrade FULL→Read

# 10. Check what's listening on the network
Get-NetTCPConnection -State Listen |
  Select LocalAddress, LocalPort, @{n='Process';e={(Get-Process -Id $_.OwningProcess).Name}} |
  Sort LocalPort

# 11. Disable the legacy Telnet client
dism /online /disable-feature /featurename:TelnetClient
Get-WindowsOptionalFeature -Online | Where State -eq Enabled | Select FeatureName   # audit

# 12. Enable BitLocker with recovery key to file
manage-bde -on C: -RecoveryPassword
manage-bde -protectors -get C: > C:\bitlocker-key.txt   # STORE THIS SAFELY

# 13. Remove stale admin accounts
Get-LocalUser | Where Enabled -eq $false
Remove-LocalUser old_temp

# 14. Scan + update Defender (release-engine independent)
powershell -Command "Get-MpComputerStatus; Update-MpSignature; Start-MpScan -ScanType QuickScan"

# 15. Verify attack surface again
Get-NetFirewallProfile | Select Name, Enabled
```

## T10. Managing Another PC Remotely

**Target setup (once, on the remote machine — Admin):**

```powershell
Enable-PSRemoting -Force
# workgroup networks: also run
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "*" -Force   # or "pc01,pc02"
Restart-Service WinRM
```

**From your desk:**

```powershell
# interactive session
Enter-PSSession -ComputerName PC01 -Credential (Get-Credential)
Exit-PSSession

# one command on many machines
Invoke-Command -ComputerName PC01,PC02,PC03 -ScriptBlock {
    Get-Volume | Select DriveLetter, SizeRemaining
} -ThrottleLimit 3 | Sort PSComputerName

# persistent session + file copy
$s = New-PSSession PC01
Invoke-Command $s { mkdir C:\Deploy -Force }
Copy-Item C:\pkg\app.msi -ToSession $s C:\Deploy\
Invoke-Command $s { msiexec /i C:\Deploy\app.msi /qn /norestart -Wait }
Receive-Job (Invoke-Command $s { Get-Service app } -AsJob)

# remote restart, then reconnect
Invoke-Command $s { Restart-Computer -Force }
Remove-PSSession $s
```

**Fallbacks:** `winrs -r:PC01 cmd` · CMD remote shutdown `shutdown /r /m \\PC01 /t 0` · RDP `mstsc /v:PC01` · Sysinternals `PsExec \\PC01 cmd` (installs a service — noisy but universal).

**pwsh 7 over SSH (no WinRM):** target needs OpenSSH + `subsystem powershell`; then `Enter-PSSession -HostName alice@pc01 -SSHTransport`.

---
---

# PART 4 — APPENDICES

## Appendix A — Master A–Z Command Index (CMD & tools)

| | Commands | | Commands |
|---|---|---|---|
| **A** | `arp` §13 · `assoc` §30 · `at` †§17 · `attrib` §5 · `auditpol` §19 | **N** | `nbtstat` §13 · `net` §15 · `netsh` §14 · `netstat` §13 · `nslookup` §13 |
| **B** | `bcdboot` §21 · `bcdedit` §21 · `bitsadmin` §27 · `bootrec` §21 · `break` §30 | **O** | `openfiles` §21 · `osk` §31 |
| **C** | `cacls` †§5 · `cd` §1 · `certreq` §26 · `certutil` §26 · `chcp` §30 · `chglogon/chgport/chgusr` §25 · `chkdsk` §9 · `chkntfs` §9 · `choice` §30 · `cipher` §12 · `cleanmgr` §21 · `clip` §4 · `cls` §0 · `cmdkey` §19 · `comp` §4 · `compact` §6 · `convert` §9 · `copy` §2 · `cscript` §29 · `curl` §6,§13 | **P** | `path` §30 · `pathping` §13 · `pause` §0 · `perfmon` §24 · `ping` §13 · `pnputil` §29 · `popd` §1 · `powercfg` §22 · `print` §2 · `prompt` §30 · `pushd` §1 |
| **D** | `date` §30 · `defrag` §9 · `del/erase` §2 · `dir` §1 · `diskpart` §10 · `dism` §21 · `doskey` §30 · `driverquery` §7 | **Q** | `qappsrv` §25 · `qprocess` §25 · `query` §25 · `quser` §25 · `qwinsta` §25 |
| **E** | `echo` §2 · `endlocal` T3 · `eventcreate` §23 · `eventvwr` §23 · `exit` §30 · `expand` §6 · `explorer` §31 · `extrac32` §6 | **R** | `rasdial` §13 · `rd/rmdir` §2 · `recover` §2 · `reg` §20 · `regedit` §20 · `regini` §20 · `regsvr32` §29 · `relog` §24 · `ren` §2 · `replace` §2 · `resmon` §24 · `reagentc` §21 · `robocopy` §3 · `route` §13 · `runas` §19 · `rwinsta` §25 |
| **F** | `fc` §4 · `find` §4 · `findstr` §4 · `finger` §13 · `fltmc` §7 · `for` §4 · `forfiles` §4 · `format` §9 · `fsutil` §11 · `ftp` §27 · `ftype` §30 | **S** | `sc` §18 · `schtasks` §17 · `secedit` §19 · `sfc` §21 · `shutdown` §22 · `sort` §4 · `start` §16 · `subst` §9 · `systeminfo` §7 |
| **G** | `getmac` §13 · `goto` T3 · `gpresult` §21 · `gpupdate` §21 | **T** | `takeown` §5 · `tar` §6 · `taskkill` §16 · `tasklist` §16 · `taskmgr` §24 · `telnet` §13 · `tftp` §27 · `time` §30 · `timeout` §16 · `title` §30 · `tracerpt` §24 · `tracert` §13 · `tree` §1 · `tscon` §25 · `tsdiscon` §25 · `tskill` §25 · `type` §2 · `typeperf` §24 · `tzutil` §28 |
| **H** | `help` §0 · `hostname` §7 | **U–V** | `ver` §7 · `verify` §30 · `vol` §9 · `vssadmin` §21 |
| **I** | `icacls` §5 · `ipconfig` §13 | **W** | `w32tm` §28 · `waitfor` §16 · `wbadmin` §21 · `wevtutil` §23 · `where` §4 · `whoami` §7 · `winmgmt` §8 · `winrm`/`winrs` §P11 · `wmic` †§8 · `wscript` §29 |
| **M** | `makecab` §6 · `manage-bde` §19 · `md/mkdir` §2 · `mode` §30 · `more` §2 · `mountvol` §9 · `move` §2 · `msg` §16 · `msiexec` §29 · `msinfo32` §7 · `mstsc` §25 | **X–Z** | `xcopy` §3 |

*(PowerShell cmdlets are indexed by module/category in Part 2; enumerate all live with `Get-Command`.)*

## Appendix B — Environment Variables Reference

| Variable | Contents |
|---|---|
| `%CD%` | Current directory |
| `%CMDCMDLINE%` | Command line that started CMD |
| `%CMDEXTVERSION%` | Command extensions version |
| `%COMPUTERNAME%` | Machine name |
| `%COMSPEC%` | Path to cmd.exe |
| `%DATE%` / `%TIME%` | Locale date / time strings |
| `%ERRORLEVEL%` | Last command's exit code |
| `%HOMEDRIVE%` `%HOMEPATH%` | User home (%HOMEDRIVE%%HOMEPATH%) |
| `%LOCALAPPDATA%` | `C:\Users\x\AppData\Local` |
| `%LOGONSERVER%` | Authenticating DC |
| `%NUMBER_OF_PROCESSORS%` | Logical CPUs |
| `%OS%` | `Windows_NT` |
| `%PATH%` `%PATHEXT%` | Search path / executable extensions |
| `%PROCESSOR_ARCHITECTURE%` · `%PROCESSOR_IDENTIFIER%` · `%PROCESSOR_LEVEL%` · `%PROCESSOR_REVISION%` | CPU info |
| `%PROGRAMDATA%` | `C:\ProgramData` |
| `%PROGRAMFILES%` `%PROGRAMFILES(X86)%` `%COMMONPROGRAMFILES%` | Install roots |
| `%PROMPT%` | Current prompt string |
| `%PSMODULEPATH%` | PowerShell module path |
| `%PUBLIC%` | `C:\Users\Public` |
| `%RANDOM%` | Random 0–32767 each expansion |
| `%SESSIONNAME%` | `Console` or `RDP-Tcp#n` |
| `%SYSTEMDRIVE%` `%SYSTEMROOT%` `%WINDIR%` | `C:` / `C:\WINDOWS` |
| `%TEMP%` `%TMP%` | User temp |
| `%USERDOMAIN%` `%USERDOMAIN_ROAMINGPROFILE%` | Domain |
| `%USERNAME%` | Login name |
| `%USERPROFILE%` | `C:\Users\x` |
| `%OneDrive%` | OneDrive root (if set) |

Set at runtime in PowerShell: `$env:NAME = "value"`; permanently: `setx`, `setx /m`, or `[Environment]::SetEnvironmentVariable(name, value, 'Machine')`.

## Appendix C — Exit-Code Tables

**robocopy** (bit flags): 1 copied · 2 extras · 4 mismatches · 8 failures · 16 fatal — test `if %errorlevel% LSS 8` = acceptable. **xcopy:** 0 ok · 1 none found · 2 ctrl-c · 4 init error · 5 disk write. **msiexec:** 0 ok · 3010 ok+reboot · 1603 fatal · 1618 busy · 1638 already installed · 1642 patch issue. **chkdsk:** 0 clean · 1 fixed · 2 cleanup/done · 3 errors remain. **diskpart script:** 0 ok, nonzero line of first error. **choice:** 1–n selected index. **robocopy in scheduled tasks:** Last Result 0 also means “nothing to copy”.

**ERRORLEVEL idioms**

```bat
some.exe
if errorlevel 1 echo failed            :: means >= 1
if %errorlevel% EQU 0 echo ok
some.exe && echo ok || echo failed
command >nul 2>&1 && echo succeeded
```

## Appendix D — CMD ↔ PowerShell ↔ Linux Equivalents

| Task | CMD | PowerShell | Linux |
|---|---|---|---|
| List files | `dir` | `Get-ChildItem` | `ls` |
| List all/hidden | `dir /a` | `gci -Force` | `ls -a` |
| Change dir | `cd` | `Set-Location` | `cd` |
| Previous dir | `pushd`/`popd` | `pushd`/`popd`, `cd -` | `cd -` |
| Print file | `type` | `Get-Content` | `cat` |
| Page file | `more` | `more` | `less` |
| Tail / follow | ✗ | `gc -Tail 20 -Wait` | `tail -f` |
| Copy | `copy`/`xcopy`/`robocopy` | `Copy-Item` | `cp` |
| Move | `move` | `Move-Item` | `mv` |
| Rename | `ren` | `Rename-Item` | `mv` |
| Delete file | `del` | `Remove-Item` | `rm` |
| Delete tree ⚠ | `rd /s /q` | `ri -Recurse -Force` | `rm -rf` |
| Create dir | `md` | `mkdir`/`New-Item` | `mkdir` |
| Create file | `echo x > f` | `New-Item`/`Set-Content` | `touch` |
| Find file | `dir /s /b` / `where /r` | `gci -Recurse -Filter` | `find` |
| Grep file | `findstr` | `Select-String` | `grep` |
| Grep output | `\| findstr` | `\| Select-String` | `\| grep` |
| Compare | `fc` | `Compare-Object` | `diff` |
| Sort | `sort` | `Sort-Object` | `sort` |
| Replace | ✗ | `-replace` | `sed` |
| Head | ✗ | `Select -First` | `head` |
| Processes | `tasklist` | `Get-Process` | `ps` |
| Kill | `taskkill /f` | `Stop-Process` | `kill` |
| Services | `sc query` / `net start` | `Get-Service` | `systemctl` |
| Disk usage | `dir /s` · `fsutil` | `Get-Volume` | `df`/`du` |
| Free/used mem | `systeminfo \| find Memory` | `Get-CimInstance Win32_OperatingSystem` | `free` |
| IP config | `ipconfig /all` | `Get-NetIPConfiguration` | `ip a` |
| Ping | `ping` | `Test-Connection` | `ping` |
| Traceroute | `tracert` | `Test-NetConnection -TraceRoute` | `traceroute` |
| Netstat | `netstat -ano` | `Get-NetTCPConnection` | `ss`/`netstat` |
| DNS lookup | `nslookup` | `Resolve-DnsName` | `dig` |
| Download | `curl -O` | `iwr -OutFile` | `wget`/`curl` |
| Shutdown | `shutdown /s` | `Stop-Computer` | `shutdown` |
| Reboot | `shutdown /r` | `Restart-Computer` | `reboot` |
| Run as admin | ⇑ + cmd | ⇑ / `-Verb RunAs` | `sudo` |
| Cron | `schtasks` | `Register-ScheduledTask` | `cron`/`systemd` |
| Env vars | `set`/`setx` | `$env:` | `export` |
| Links | `mklink` | `New-Item -ItemType SymbolicLink` | `ln -s` |
| Uptime | `systeminfo` | `Get-Uptime` | `uptime` |
| Who am I | `whoami` | `whoami` | `whoami` |
| History | `doskey /history` | `Get-History`/Ctrl+R | `history` |

## Appendix E — Keyboard Shortcuts (both shells)

CMD: F1–F9 history/editing (§0.7) · Ctrl+C abort · Esc clear line · Tab path-complete · Ctrl+Home/End line-delete · PageUp first cmd.

PowerShell (PSReadLine): Tab/Ctrl+Space completion · Ctrl+R reverse search · ↑/↓ history · Ctrl+A/E/K/U/W line edits · Ctrl+Left/Right word jump · Alt+. last arg · F2 predictions · F8 history-match · Ctrl+L clear screen · Ctrl+C cancel · Ctrl+Z undo.

Both: F11 fullscreen · Ctrl+Shift+C/V copy/paste (or just select/RightClick in CMD) · Ctrl+MouseWheel font zoom · Alt+Enter fullscreen (classic).

## Appendix F — Run (⊞+R) Launcher List

**Shells/consoles:** `cmd` · `powershell` · `pwsh` · `wt` · `bash` (WSL) · `windows-sandbox` (Pro).

**Management:** `compmgmt.msc` · `devmgmt.msc` · `diskmgmt.msc` · `services.msc` · `eventvwr` · `taskschd.msc` · `gpedit.msc` · `secpol.msc` · `lusrmgr.msc` · `certmgr.msc` · `certlm.msc` · `wf.msc` · `fsmgmt.msc` · `perfmon` · `resmon` · `taskmgr` · `msinfo32` · `regedit` · `msconfig` · `control` · `optionalfeatures` · `dccw` (calibrate) · `dxdiag` · `winver` · `sysdm.cpl` (System Properties) · `appwiz.cpl` · `ncpa.cpl` · `powercfg.cpl` · `timedate.cpl` · `intl.cpl` · `mmsys.cpl` · `inetcpl.cpl` · `wscui.cpl` · `main.cpl` · `desk.cpl`† · `hdwwiz.cpl` · `control printers` · `control folders` · `control userpasswords2` · `control update` · `control admintools` · `control color` · `control desktop` · `netcpl.cpl`†→ncpa.

**System tools:** `cleanmgr` · `dfrgui` · `chkdsk`⌘ · `defrag`⌘ · `sfc`⌘ · `diskpart`⌘ (⌘ = needs arguments/Admin console) · `recoverydrive` · `rstrui` · `sdclt` · `msdt` (Support Diagnostic) · `wsreset` · `lpksetup` · `rekeywiz` · `shrpubw` · `sysprep` · `dxdiag` · `mdsched` (memory test) · `verifier`⌘ · `perfmon /report` · `eventvwr` · `osk` · `narrator` · `magnify` · `utilman` · `charmap` · `calc` · `notepad` · `write` · `mspaint` · `snippingtool` · `explorer` · `mstsc` · `winver` · `wmplayer`.

**Power-user:** `shell:startup` (startup folder) · `shell:appdata` · `shell:programfiles` · `shell:sendto` · `shell:recyclebinfolder` · `shell:downloads` · `%temp%` · `%USERPROFILE%` · `printmanagement.msc` · `sigverif` (signed-driver check) · `iexpress` (self-extracting packager) · `eudcedit` (private character editor) · `fontview`.

## Appendix G — Common Errors & Quick Fixes + Safety Checklist

| Error message | Usual cause → fix |
|---|---|
| `'x' is not recognized as an internal or external command` | Not on PATH/typo → check spelling, `where x`, full path, or add folder to PATH (`setx PATH "%PATH%;C:\tools"`) |
| `Access is denied.` | Not elevated or ACL → Admin prompt, `takeown`+`icacls`, check read-only/`attrib` |
| `The system cannot find the path specified` | Bad path/missing drive → `cd /d` across drives, quote spaces, check with `dir` |
| `The system cannot find the file specified` | Missing file → `where /r` to hunt it |
| `The process cannot access the file because it is being used by another process` | Locked → close app, `openfiles query` (Admin), `handle.exe` (Sysinternals), or restart |
| `There are currently no logon servers available` (domain) | No DC → check VPN/network, `nltest /dsgetdc:domain` |
| `Multiple connections to a server … not allowed` (1219) | Cached session → `net use * /delete`, or different username |
| `The requested operation requires elevation` | Redo as Admin |
| A file is in use by another process | Close the owner app, `openfiles query` (Admin), or schedule a delete-at-reboot |
| Robocopy “Access denied” on your own files | Take ownership first: `takeown /f X /r /d y & icacls X /grant %username%:F` |
| PowerShell: `running scripts is disabled` | `Set-ExecutionPolicy RemoteSigned -Scope CurrentUser` or `-ExecutionPolicy Bypass` per-run |
| PowerShell: `SC` does weird things | `sc` aliases Set-Content → type `sc.exe` |
| `robocopy` copies everything every time on NAS | Add `/fft` |
| Scheduled task Last Result `0x1` | Script failed — run it manually in same context (`runas /user:SYSTEM` via psexec) |
| `Windows Resource Protection found corrupt files but was unable to fix` | Run `DISM /RestoreHealth` then `sfc /scannow` again |

**Safety checklist before any destructive command**
1. Am I elevated? Do I need to be?
2. Is the target path exactly right? (`cd` there, `dir` it first)
3. Rehearse: prefix with `echo`, or add `/l` (robocopy), `-WhatIf` (PowerShell)
4. Snapshot: `dir /s /b > before.txt` or `reg export` or `vssadmin create shadow /for=C:`
5. One command at a time — never chain `&&` with `rd /s /q format diskpart`
6. Close Explorer windows into that tree; check `openfiles query`
7. Have a bootable USB (Media Creation Tool) before touching boot/disk tools

---

## Keep Learning

- Official A–Z: **learn.microsoft.com/windows-server/administration/windows-commands/windows-commands**
- PowerShell docs: **learn.microsoft.com/powershell** (every cmdlet page has examples)
- Practice safely: `mkdir C:\Lab`, Windows Sandbox, or a VM snapshot
- 7-day path: Day 1 §0–2 · Day 2 §3–6 · Day 3 §13–15 (network) · Day 4 §16–19 · Day 5 §20–22 (repair) · Day 6 T3+T6 (automation) · Day 7 T8 (PowerShell report)
- When stuck: `command /?` first, then `Get-Help cmdlet -Online`, then this document's index (Appendix A)

*End of reference — 600+ commands, 40+ subcommand tables, 10 tutorials. Happy shelling.* 🔧
