---
title: "Connecting a Toper Coffee Roaster to Artisan Scope on Mac"
date: 2023-04-18
---

# Connecting a Toper Coffee Roaster to Artisan Scope on Mac

I have a 2018 Toper TKMSX-1G coffee roaster (1kg capacity). It has a USB cable attached to it, so I wanted to connect it to a laptop, so I could record and analyze my roasts. I have a MacBook Pro with the M1 (Apple Silicon) processor, running Ventura (macOS 13).

![Toper roaster type](/docs/assets/images/toper-roaster-type.jpeg)

[Artisan](https://artisan-scope.org) is an open-source software that helps coffee roasters record, analyze, and control roast profiles. It can be used on Windows, Mac, or Linux.

The Artisan software supports many different roaster machines. When you first run the app, use the `Config > Machine` menu to load the configuration for your roaster. The menu has an option for `Toper > USB...` so I thought this would be easy. However, after selecting this option, a dialog pops up, prompting you to specify your port configuration. Unfortunately, the only options to choose from was  external monitor, and my bluetooth headphones, nothing resembling my roaster.

![Artisan port config](/docs/assets/images/artisan-port-config.jpeg)

I tried using the `Config > Device` and `Config > Port` menus in Artisan, but couldn't make heads-or-tails of anything, and nothing I did would allow Artisan to connect to the roaster.

After googling whatever ideas I could think of, my next hope was finding out that some Toper roasters have an Ethernet port built-in as well as USB, and can be connected to a network, or directly to the laptop. Unfortunately, there was no such port in my roaster.

Finally I followed the USB cable inside the machine and traced it to a box that said "PhidgetTemperatureSensor" on it. Hmm... I googled "phidget" and discovered phidgets are "products for USB Sensing and Control". Furthermore, the Artisan `Config > Machine` menu had a "Phidget" option. I selected the `Phidget USB 1048 Databridge 2xTC` sub-option, mostly because it included "USB" in the description.

![Phidget temperature sensor](/docs/assets/images/phidget_temp_sensor.jpeg)

Still nothing.

However, the Phidgets.com website also had a [drivers software section](https://www.phidgets.com/docs/OS_-_macOS), with an installer for OS X 10.11+. I downloaded and installed it. Note that the driver comes as a kernel extension (kext), which, in modern Mac OSs, is no longer "recommended", and thus requires you to approve the installation from System Settings (nee System Prefs) and rebooting before it will be active. I rebooted, plugged in my roaster, fired up Artisan and... voila!

All this took me several days, and not a little frustration to work out. And so, dear future Internet traveller, I am leaving this blog post as a bread crumb for you, in hopes of saving you at least a little time. Good luck!

## Full Instructions

1. Download the [Phidget 22 installer](https://www.phidgets.com/downloads/phidget22/libraries/macos/Phidget22.dmg) from phidgets.com
2. Run the installer (Phidgets.pkg) 
    - **Note:** In macOS 11 and later, third-party kernel extensions (kexts) require the user’s approval to install, and restarting of the macOS to load the changes into the kernel (see below).
3. Run the "Phidget Control Panel" in Applications to ensure the device is visible.
4. **Close the Control Panel** app. (You cannot run Artisan and the Phidget Control Panel at the same time)
5. Run Artisan and configure using the "Config > Machine > Phidget > USB 1048 Databridge 2xTC" option

### Allow Kernel Extension Installation (macOS 11-12)

1. Open Apple System Preferences
2. Open "Security & Privacy"
3. Select the "General" tab
4. If general settings are locked:
    - Click the lock icon in the lower-left corner
    - Enter your device password
    - Click "Unlock"
5. Click "Allow" to allow the Phidgets kext to load & reboot

### Allow in macOS 13 (Ventura)

1. Open " > System Settings"
2. Open "Privacy & Security" section
3. Scroll down to the "Security" section
4. Click "Allow" to allow the Phidgets kext to load
5. Reboot after installation to activate extension
