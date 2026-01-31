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

> **Note on Raspberry Pi Imager versions**
>  
> Raspberry Pi Imager’s layout changes occasionally between releases.
> This guide uses Raspberry Pi Imager 2.x — if your buttons are in slightly
> different places, that’s okay. The *option names* are what matter.

---

### What you’ll need

- A computer (macOS, Windows, or Linux)
- A microSD card (16 GB minimum, 32 GB recommended)
- A microSD card reader
- Raspberry Pi Imager (free)

Download Raspberry Pi Imager from:
https://www.raspberrypi.com/software/

---

### Step 1: Select your Raspberry Pi device

When Imager opens, you’ll first be asked which Raspberry Pi you’re using.

Select:

- **Raspberry Pi 4**

![Raspberry Pi 4 device selection](docs/images/01-imager-device-pi4.png)

This ensures Imager shows OS options that are compatible with the Pi 4.

---

### Step 2: Choose the OS category

Next, select:

- **Raspberry Pi OS (other)**

![Raspberry Pi OS (other) category](docs/images/02-imager-os-category.png)

This is where the Lite (64-bit) images live.

---

### Step 3: Choose Raspberry Pi OS Lite (64-bit)

From the list of available OS images, select:

- **Raspberry Pi OS Lite (64-bit)**

![Raspberry Pi OS Lite (64-bit) selected](docs/images/03-imager-os-lite-64bit.png)

Why Lite + 64-bit?

- No desktop overhead
- Better performance
- Better Python support (important for indi-allsky)

---

### Step 4: Choose storage

Select your microSD card.

If you have more than one drive connected, double-check this step. 
Imager will overwrite whatever you select.

---

### Step 5: Customisation settings (important)

Imager will now walk you through several customisation screens.
These settings make a headless setup much easier.

#### Hostname

Set a clear, descriptive hostname:

- Example: `indi-allsky-pi4-ir`

![Hostname setting](docs/images/04-imager-hostname.png)

#### Username

Create a non-personal user account:

- Example: `allsky`

![Username setting](docs/images/05-imager-username.png)

#### Wi-Fi

If you plan to use Wi-Fi, enter your network details.

In screenshots, we use a placeholder network name.

![Wi-Fi configuration](docs/images/06-imager-wifi.png)

> Replace `ExampleWiFi` with the name of your own network.

#### Enable SSH

Enable SSH and choose **password authentication**.

![SSH enabled](docs/images/07-imager-ssh-enabled.png)

SSH is required to access the Pi remotely without a keyboard or monitor.

You can change all of these settings later — no reflashing required.

You may also see localisation options (time zone and keyboard layout). These are worth setting correctly, but they don’t affect the install process.

---

### Step 6: Write the card

Click **Write** and let Imager do its thing.

This usually takes a few minutes. When it’s done, safely eject the microSD card.

---

## How this guide works

We install and test things one step at a time. When screenshots are helpful, they’ll be called out explicitly 📸

If you’re following along at home:
- you’re not expected to know Linux
- copy/paste is encouraged
- curiosity > perfection

---

## First boot checklist

This section confirms that your Raspberry Pi:

- boots correctly
- is reachable over the network
- is actually 64-bit
- didn’t quietly betray you 😄

We’ll keep this short and calm.  
No camera yet. No indi-allsky yet.

---

### Step 1: Insert the SD card and power on

1. Insert the microSD card into the Raspberry Pi
2. Connect:
   - power
   - Ethernet **or** make sure Wi-Fi is in range
3. Power it on

Give it **30–60 seconds**. Headless boots take a moment.

---

### Step 2: Connect via SSH

From your computer, open a terminal and run:

~~~bash
ssh allsky@indi-allsky-pi4-ir.local
~~~

If `.local` doesn’t work, try connecting via the Pi’s IP address instead  
(check your router or use `arp -a`).

The first time you connect, you may see a message like this:

~~~
The authenticity of host 'indi-allsky-pi4-ir.local' can't be established.
Are you sure you want to continue connecting?
~~~

Type:

~~~
yes
~~~

Then enter the password you set in Raspberry Pi Imager.

If you land at a prompt like:

~~~
allsky@indi-allsky-pi4-ir:~ $
~~~

You’re in. 🎉

---

### Step 3: Confirm the OS is 64-bit

Run:

~~~bash
uname -m
~~~

You should see:

~~~
aarch64
~~~

---

### Step 4: Update the system

~~~bash
sudo apt update
sudo apt full-upgrade -y
~~~

Reboot when finished:

~~~bash
sudo reboot
~~~

Reconnect via SSH after about a minute.

---

### Step 5: Pause and celebrate

At this point:

- the Pi boots successfully
- SSH access works
- the OS is confirmed 64-bit
- naming is consistent with this guide

---

## Next step

**Camera verification (libcamera)** — up next.
