# Privio Compass

*(by Intelliroot)*

A free, standalone desktop companion for Digital Personal Data Protection Act
(DPDPA) readiness — a Gap Assessment, Data Flow Mapping with an auto-generated
RoPA, and a 90-day compliance roadmap. Fully local: SQLite storage, no
network calls, no telemetry.

<img width="1337" height="803" alt="image" src="https://github.com/user-attachments/assets/70ff6580-9906-42a3-917f-fc16002dfe3c" />

> **⚠️ Windows Defender / SmartScreen may flag `privio-compass.exe` on first run.**
> This is a known false positive common to unsigned, freshly-built
> binaries — see **[SECURITY.md](./SECURITY.md)** for why it happens, the
> SHA-256 checksum to verify your download against, and how to clear it.
# Security & antivirus notice

## Why Windows Defender / SmartScreen may flag `privio-compass.exe`

This is a known false positive, not a real detection. It happens because the
executable is:

- **Unsigned** — we don't yet hold a code-signing certificate, so Windows has
  no publisher identity to trust.
- **New** — a freshly built binary has no download history or reputation in
  Microsoft's cloud scoring, which both Defender and SmartScreen lean on
  heavily for unsigned files.
- This app single self-contained executable.
  That packing pattern coincidentally overlaps with how some real malware is
  packaged, which trips heuristic/ML detections (commonly surfaced as
  `Trojan:Win32/Wacatac.B!ml` or a generic "behavior" detection) on binaries
  that are, on inspection, clean.

## How to verify this build yourself

Don't take our word for it — verify the exact file you downloaded:

1. **Check the hash.** Every release lists the SHA-256 of `privio-compass.exe`.
   Compare it against what you have:

   ```powershell
   Get-FileHash .\privio-compass.exe -Algorithm SHA256
   ```
   Current build:
   ```
   SHA-256: AADFF6B42D8AA9CADBB6EE7C559BA586E4005C0E02E7045964BF6CE21D77C353
   Size:    17,851,904 bytes
   Built:   2026-10-17 (trimpath + stripped debug symbols — see note below)
   ```
   If the hash doesn't match exactly, don't run the file — re-download it.

2. **Scan it independently.** Upload the exe to
   [VirusTotal](https://www.virustotal.com/) yourself and check the
   consensus across 70+ engines, rather than relying on any single vendor's
   verdict.

## If Defender blocks or quarantines the file

This is the fastest fix for local use (not a workaround for anything
malicious — it just tells Defender to stop re-scanning a file you've already
verified):

1. Open **PowerShell as Administrator**.
2. Run:

   ```powershell
   Add-MpPreference -ExclusionPath "<path to the folder containing privio-compass.exe>"
   ```

3. If Defender already removed the file: **Windows Security → Virus & threat
   protection → Protection history** → find the entry → **Restore**.

## What this app actually does with your data

Worth stating plainly, since it's the real answer to "is this safe": Privio
Compass is a **fully local, standalone** app. It stores its SQLite database
under your user profile (`%AppData%\DPDPA Tools` — the folder keeps its
original internal name from before the product was renamed, so existing
local data isn't orphaned by the rename), makes no outbound network calls
except the two explicit "Visit website" / "Watch video" buttons (which open
your system browser — they don't run inside the app), and ships no analytics
or telemetry.

## Reporting a real issue

If you believe you've found an actual security issue (not an AV false
positive), please open an issue in this repository rather than a public
disclosure, so we can look into it first.
  
