# indi-allsky on Raspberry Pi 4 + Camera Module 3 Wide IR

This guide documents a clean, beginner-friendly setup of **indi-allsky** on a Raspberry Pi 4 using the Raspberry Pi Camera Module 3 Wide IR.

The goal is a reliable all-sky camera setup for:
- sky condition monitoring
- timelapses
- keograms
- star trails

This is written for curious hobbyists *and* technical folks. If something feels confusing at first, that’s normal. We’ll go slowly.

---

## Hardware used

- Raspberry Pi 4 Model B  
- Raspberry Pi Camera Module 3 Wide IR  
- microSD card (Raspberry Pi OS Lite, 64-bit)  
- Stable power supply  
- Outdoor enclosure (optional, later)

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
