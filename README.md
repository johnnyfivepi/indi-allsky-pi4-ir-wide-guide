# indi-allsky on Raspberry Pi 4 + Camera Module 3 Wide IR

This guide documents a clean, beginner-friendly setup of **indi-allsky** on a Raspberry Pi 4 using the Raspberry Pi Camera Module 3 Wide IR.

The goal is a reliable all-sky camera setup for:
- sky condition monitoring
- timelapses
- keograms
- star trails

This is written for curious hobbyists *and* technical folks. If something feels confusing at first, that’s normal. We’ll go slowly.

---

## What we’ll cover

- Hardware
- OS + Raspberry Pi Imager settings
- First boot checklist
- Camera verification (libcamera)
- indi-allsky installation
- Web UI + first light
- Keograms & star trails
- Storage & retention
- Troubleshooting
- Roadmap (Pi 5 variant later)

---

## Hardware used

- Raspberry Pi 4 Model B  
- Raspberry Pi Camera Module 3 Wide IR  
- microSD card (Raspberry Pi OS Lite, 64-bit)  
- Stable power supply  
- Outdoor enclosure (optional, later)

---

## OS + Raspberry Pi Imager settings

We’ll start by flashing Raspberry Pi OS Lite (64-bit) to a microSD card using **Raspberry Pi Imager**.

Even if you’ve done this before, it’s worth slowing down here — a couple of small choices make life much easier later.

---

### What you’ll need

- A computer (macOS, Windows, or Linux)
- A microSD card (16 GB minimum, 32 GB recommended)
- A microSD card reader
- Raspberry Pi Imager (free)

Download Raspberry Pi Imager from:
https://www.raspberrypi.com/software/

---

### Step 1: Choose the OS

Open Raspberry Pi Imager and select:

- **Operating System**
  - Raspberry Pi OS (other)
  - **Raspberry Pi OS Lite (64-bit)**

📸 **Screenshot moment**  
Capture: OS selection screen  
Make sure it shows: “Raspberry Pi OS Lite (64-bit)”  
Suggested filename: `01-imager-os-selection.png`

Why Lite + 64-bit?
- No desktop overhead
- Better performance
- Better Python support for indi-allsky

---

### Step 2: Choose storage

Select your microSD card.

If you have more than one drive connected, double-check this step —
Imager will overwrite whatever you select.

(No screenshot needed here unless you want one.)

---

### Step 3: Advanced settings (important)

Click the ⚙️ **gear icon** (or press `Cmd + Shift + X` / `Ctrl + Shift + X`).

Set the following:

- **Hostname**
  - Example: `allsky-pi4-ir`
- **Enable SSH**
  - Check “Enable SSH”
  - Password authentication is fine
- **Set username and password**
  - Pick something you’ll remember
- **Configure wireless LAN**
  - If using Wi-Fi, enter your network details
- **Set locale settings**
  - Time zone (important for sky data!)
  - Keyboard layout

📸 **Screenshot moment**  
Capture: Advanced settings screen  
Make sure it shows: hostname + SSH enabled  
Suggested filename: `02-imager-advanced-settings.png`

Don’t worry, you can change all of this later if needed.

---

### Step 4: Write the card

Click **Write** and let Imager do its thing.

This usually takes a few minutes.

📸 **Optional screenshot moment**  
Capture: “Writing image” or “Write complete” screen  
Suggested filename: `03-imager-write-complete.png`

When it’s done, safely eject the microSD card.

---

## OS choice

- **Raspberry Pi OS Lite (64-bit)**

Why:
- better performance
- better Python support
- fewer surprises with indi-allsky

---

## Hostname convention

To avoid confusion with other Raspberry Pis:

- **This build (Pi 4)**: `indi-allsky-pi4-ir-wide`
- **Future build (Pi 5)**: `indi-allsky-pi5-wide` (not yet covered here)

You can change hostnames later — no reflashing required.

---

## How this guide works

We install and test things one step at a time. When screenshots are helpful, they’ll be called out explicitly 📸

If you’re following along at home:
- you’re not expected to know Linux
- copy/paste is encouraged
- curiosity > perfection
