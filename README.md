# My XPS 13 7390 Hackintosh
A perfect, vanilla setup of macOS Sonoma, Ventura, or Montery with Open Core for the Dell XPS 13 7390. You should be able to easily adapt this to similar Dell laptops too!

I scrupulously went through Dortiana’s guide and worked many brain cells to create this. It truly is something, thanks Dortiana, the OpenCore team, and all the Kext devs :)


### CPU:
i7 10510U (4.9Ghz & 4c+8t), power management & turbo boost work great!

### GPU:
Intel UHD Graphics 630

### RAM:
16 Gigs Laptop: XPS 13 7390 (late 2019)

### Wi-Fi+BT:
Built-in Killer Wifi+BT card (Intel-based, so OpenIntelWireless works)

### BIOS revision:
1.19.0 (the current latest)


I also added thermal pads (https://imgur.com/a/MqWwBim) inside so the CPU can use the entire aluminum backplate as a heat spreader - it now runs without the fan kicking in unless I'm doing something very intensive, a palpable improvement! You could try this on your XPS too.

The internal SK Hynix SSD needed to be replaced as macOS doesn't support it. I popped in a WD Blue SN 570 - it works perfectly as the same chipset is used in real Macs. While at it, I gave it a fresh battery too!


## What works:
### Everything!
if you want me to list everything out:
- sleep and wake work beautifully like a real Mac on lid closure and opening
- thunderbolt, CPU power management, cameras & speakers
- the touchscreen works great and I can use trackpad gestures on it too, which gives this the world's largest trackpad lmao - BEAT THAT, MacBooks :p (thanks VoodooI2C!)
- the trackpad, keyboard...
- all Apple’s iCloud services like iMessage and Find My (my nightmare is if someone buys a Mac with the serial number I used xD)

### I lied, everything except:
- The fingerprint scanner (expected)
- Handoff only works from other iDevices > this laptop, and no AirDrop (an OpenIntelWireless limitation rn)


The funny thing is that macOS runs smoother than Windows 11 on this laptop since it’s more efficient with GPU usage (Windows 11 is so bloated with 69 different UI frameworks layered atop legacy ones, that it stuttered at times on this iGPU at 4k).

OpenCore and the Kexts are also totally up to date for now, so enjoy:)
It works fine with SIP enabled, and macOS updates (including the Rapid Security Responses) work seamlessly from Settings too. Tested last on the latest version of Ventura as of now (13.4).


## ❗️PSA:
1. **Before** booting using this, [you need to disable CFG-Lock](https://github.com/dreamwhite/bios-extraction-guide/tree/master/Dell) or it won't work.
Disable it [using this specific version of `grub_setup_var`](https://github.com/XDleader555/grub_setup_var/releases/tag/v1.0-alpha).

I've already added this version of `grub_setup_var` to the EFI folder, and also found the right BIOS flag to disable it, so here you go!

| BIOS              | CFG Lock                      | Overclock Lock
| ----------------- | ------------------------------| -----------------------------
| `1.9.0`, `1.12.1`, `1.13.0`     | `setup_var CpuSetup 0x3E 0x0` | `setup_var CpuSetup 0xDA 0x0`

2. **Don't directly use this config.plist** - you must generate your own serial number, MLB, ROM, and UUID numbers and add this to my ```
```config.plist```.

Don't fret, [this tool](https://github.com/corpnewt/GenSMBIOS) wll generate it for you :)

[Here are detailed instructions.](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#using-gensmbios)

Once you generate the values, replace these bits of my ```config.plist``` with your values:

![Values to replace](https://github.com/theJayTea/XPS-13-7390-Hackintosh/blob/main/Values_to_replace.jpg)


Good luck :]
Let me know if you need any help.
