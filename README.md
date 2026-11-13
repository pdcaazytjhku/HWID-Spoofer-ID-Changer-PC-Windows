# 🔥 HWID Spoofer & ID Changer — PC Windows

A hardware-ID spoofer — is a Windows desktop utility that rewrites the identifiers a machine reports about itself (SMBIOS UUID, disk and volume serials, NIC MAC, `MachineGuid`, product ID) from the client side instead of from a new motherboard. This repo documents the installer side of it rather than the button: build number and compile date, Authenticode signer, SHA-256, x64 and ARM64 packages kept in separate lanes, silent install flags, the per-user install path under `%LOCALAPPDATA%`, the serial profile under `%APPDATA%`, and the original-ID snapshot kept for rollback. Windows 10/11, no admin prompt at install, no writes into the game directory.

---

# 📥 **INSTALLER PICKUP — START HERE**

## [⬇️ **GET THE WINDOWS INSTALLER**]( )

> One tap, the package opens on its own page — no wrapper in between.

---

## 🖼️ **PREVIEW IMAGE**

<img src="" width="1280" height="720" alt= preview image">

---

### 📦 [**OPEN THE PACKAGE**]( )

---

## ✨ What's inside

🪟 **Version stamp first** — build number and compile date printed in the header before a byte moves. If a page can't tell you the build, it's a wrapper, not a source.

🔐 **Signature check** — Authenticode subject is shown and expected to match the publisher cert, driver `.sys` countersigned. An unsigned spoofer from a mirror is a guess with a file size.

🧮 **SHA-256 line** — hash published next to the build so a downloaded file can be verified with `certutil -hashfile`. Mismatch means re-download, not "probably fine".

🧱 **Arch split** — x64 and ARM64 kept separate. An ARM64 driver dropped on an x64 machine loads, runs under emulation, and fails to patch one serial out of five for reasons nobody diagnoses.

📁 **Install paths on the table** — per-user install under `%LOCALAPPDATA%\HwidSpoofer`, profile under `%APPDATA%\HwidSpoofer`, logs under `%APPDATA%\HwidSpoofer\logs`. No `Program Files` surprise, no game-folder writes.

⚙️ **Silent install flags** — `/S` for the EXE path and `Add-AppxPackage` for the MSIX path, plus the headless form `spoofer.exe --silent --profile default`, all written out, all without a GUI step.

🔌 **Profile location** — `%APPDATA%\HwidSpoofer\profile.json`, with a working skeleton listing every spoofable target so nothing gets flipped that you didn't ask for.

💾 **Backup before write** — original values are dumped to `%APPDATA%\HwidSpoofer\backup.json` before the first spoof. A spoof without a snapshot is a one-way door.

♻️ **Rollback line** — the previous build number kept in the profile, and `--restore` to put the real IDs back. An update that breaks a launch should have a way back.

---

## 🏅 How the entries read

| Tier | Meaning |
| --- | --- |
| **S** | decides whether you have the real package — signature, driver countersign, SHA-256 |
| **A** | decides whether it applies cleanly — arch split, install path, silent flags, reboot behaviour |
| **B** | useful after the fact — profile path, backup snapshot, rollback line |
| **Noise** | on every wrapper page, proves nothing — "latest version", countdown timers, "undetected forever" |

---

## 🧪 Live example — one verify, one install, one honest log

What the console prints on a real run: