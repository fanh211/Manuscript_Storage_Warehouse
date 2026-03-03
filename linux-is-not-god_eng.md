```markdown
---
title: 'Linux Is Not a God'
date: 2025-10-15 22:00:00
tags: [Operating Systems]
published: false
hideInList: false
isTop: false
---

*(Image: Disclaimer)*

After the last video went live, the responses poured in — everything from praise to outrage. It also exposed some uncomfortable truths the Linux community prefers to ignore. This episode is mainly a follow-up, clarification, and correction. If you haven’t seen the previous one, go watch it first.

Big thanks to @BreezeArch for providing much of the outline, inspiration, and source material.

Today I’m going to walk you through — in chronological order — the avalanche of problems that almost every genuine Linux newcomer actually encounters. No fluff. Let’s dive in.

## 1. Getting Started

### 1.1 Choosing a Distribution

*(Image: The infamous Linux distribution tree)*

This monstrous tree is basically every Linux distribution that currently exists. Everyone says the first step for a new Linux user is “choose the right distro”. Sounds simple — except for actual beginners this tree is a fucking nightmare.

Hundreds of branches: source-level families like Debian and Red Hat → mainstream derivatives like Ubuntu, Fedora, Mint, Pop!_OS → extreme custom builds like Gentoo, Arch, NixOS, Linux From Scratch. Each one proudly wears completely different badges: rolling release, LTS stability, source-based compilation, corporate sponsorship, minimalist philosophy, etc.

Newbies don’t know:

- difference between apt vs dnf vs pacman
- what “rolling release freshness vs stability roulette” actually means
- how much “community vs corporate backing” matters in real life

They just follow whatever random YouTuber or forum post screams loudest.

And the single most toxic trap: the “Arch is the best for learning Linux” propaganda pushed by terminal elitists who “forget” to mention that installing Arch requires manually:

- partitioning disks
- configuring network from terminal
- installing & configuring a display server
- installing & configuring a desktop environment
- installing & configuring a display manager
- installing & configuring GPU drivers
- …all before you even see a graphical interface.

*(Image: Arch Linux live ISO boot screen — pure black terminal)*

New user downloads the ISO, boots it, sees this black screen with white text, freezes for 30 minutes, doesn’t know how to type `lsblk`, can’t mount anything, spends two days fighting black screens because no NVIDIA driver, finally rage-quits and nukes the USB.

*(Image: 2024 beginner market share pie chart)*

Reality check — 2024 data shows **Ubuntu family still holds ~68% of true beginner market share** precisely because it (and especially its derivatives like Mint) is as close to “just fucking works” as Linux gets.

*(Image: Linux Mint Cinnamon desktop + software manager)*

Mint ships with printer drivers, codecs, a Windows-like layout, a beautiful and dead-simple app store. Yet tons of beginners never even hear about Mint — they get funneled straight into Arch, Void, or Gentoo recommendation hell, hit an impenetrable wall on day one, and conclude “Linux is impossible”.

### 1.2 Picking the Right ISO

*(Image: TUNA mirror list for Ubuntu / Mint — architecture & flavor selector)*

Open any popular mirror — instantly buried under:

- amd64 / arm64 / riscv64 / ppc64el …
- Desktop / Server / Live / Minimal / Cloud …
- gnome / kde / xfce / cinnamon / mate / budgie / lxqt …

Each choice matters hugely, but zero beginner-oriented explanation is provided.

- Download arm64 thinking it’s “newer” → USB won’t boot → reflash 5 times before realizing architecture mismatch
- Pick “Live” image thinking changes persist → customize everything → reboot → everything gone → hours wasted
- Choose xfce for “lightweight” → hate how ugly it looks → switch to cinnamon → old laptop becomes a slideshow → re-download again

Every wrong choice = hours/days of frustration → strong temptation to just reinstall Windows.

### 1.3 Actually Installing It

Burning USB tools (Ventoy/Rufus) are standard — nothing special.

The real pain begins with **dual-boot** — because almost no one is ready to abandon Windows completely.

- Disable Secure Boot in BIOS (newbies can’t find the option)
- Change boot order (English menus, panic clicking)
- Partitioning — automatic partitioning often screws you later:

  - / too small → root fills up quickly
  - /home too big or too small depending on habits
  - missing /boot → GRUB rescue hell

Manual partitioning requires understanding:

- /boot (≥1GB)
- EFI system partition sharing with Windows
- swap size rules
- / vs /home split logic
- ext4 vs btrfs vs xfs trade-offs

Miss one step → black screen or GRUB failure → full reinstall.

Windows partitioning is visually intuitive with way more hand-holding tutorials. Linux still feels like a CS homework assignment.

## 2. Daily Usage Hell

### 2.1 Installing Software

Linux package managers (apt, dnf, pacman) are objectively beautiful for open-source software:

```bash
sudo apt install gimp
```

Done. Dependencies resolved, paths clean, uninstall clean.

Then you want proprietary / professional software.

DaVinci Resolve example:

- Download 3 GB .run file
- `chmod +x DaVinci_Resolve_*.run`
- `./DaVinci_Resolve_*.run`
- Immediately greeted with:

```
Missing or outdated system packages detected.
Please install: libapr1 libaprutil1 libxcb-composite0 libxcb-cursor0 ...
```

Now what? Which versions? Which repos? Conflicting versions break Chrome / Firefox / system libraries.

Dependency hell → broken system libraries → browser crashes → try Flatpak/Snap → still missing codecs → try containers → performance hit → give up.

Root cause: most proprietary vendors treat Linux as an afterthought — lazy .run files with zero dependency checking.

### 2.2 Software “Adaptation” Theater

Many Chinese companies now “support Linux” thanks to government push.

Reality: almost always castrated versions.

Tencent Meeting Linux version — missing:

- virtual background blur
- real-time subtitles & translation
- whiteboard collaboration
- annotation on shared screen
- …basically 2–3 generations behind Windows version

Same story for countless other “Linux-compatible” apps: feature-poor, buggy, abandoned.

### 2.3 Drivers — Still a Shitshow

NVIDIA finally provides decent closed drivers — great.

Everything else? Still pain.

- Random USB Wi-Fi dongles that Windows plug-and-play → Linux needs `eject sr0` magic or won’t even enumerate
- Realtek NICs with r8169 driver — half the throughput of Windows closed driver
- Printers: many (especially Chinese brands) have zero Linux driver
- PCIe devices randomly not detected → manual modprobe blacklisting → editing /etc/modprobe.d files

Community response when newbies ask for help: “Just write your own kernel module lol” or “use the source, Luke”.

### 2.4 Terminal or GTFO

Every serious problem eventually forces you into the terminal.

Examples:

- Missing .run dependencies → copy-paste 20-package install command
- NVIDIA driver install → full CLI ritual including switching to TTY, blacklisting nouveau, running .run as root
- Wi-Fi suddenly dies → `nmcli` commands
- App store empty → `sudo apt clean && sudo apt update`

Newbies are terrified of the black box. One typo → panic. One wrong sudo rm → system gone.

Mint / Deepin hide 99% of it — but the remaining 1% is always the critical breakage.

### 2.5 sudo — The Double-Edged Sword

Newbies hear “just add sudo” → copy dangerous commands from random forums.

- `sudo rm -rf /` memes become reality
- `sudo apt remove` wrong metapackage → desktop environment deleted → boot to tty only

Windows “everything runs as admin by default” is actually much safer for average users.

### 2.6 Wine / Compatibility Layer Hell

Single-boot Linux users → forced to use Wine / Proton / CrossOver.

- Games crash on window resize
- Photoshop CS6 brush lag unbearable
- Office documents render wrong / crash on save

DXVK compilation requires proxy, git, meson, ninja, vulkan-headers… pure masochism.

Performance usually 30–70% worse than native Windows — even on same hardware.

### 2.7 Dual-Boot Nightmares

- Windows Update kills GRUB → Linux invisible
- Resizing partitions → risk nuking both OSes
- NTFS ↔ ext4 file sharing → random corruption / permission issues
- Switching OSes for one missing app → 3-minute reboot tax every time

Many users eventually just give up and stay on Windows.

### 2.8 deepin / UOS — Pretty Cage

Deepin looks gorgeous —毛玻璃, animations smoother than macOS sometimes, preconfigured fcitx, WeChat/QQ one-click, NTFS read-write out of box.

But underneath? Still vanilla Debian/Ubuntu base.

- Tencent Meeting still missing features
- DaVinci Resolve still dependency hell
- Printer still no driver
- App store “Windows apps” = repackaged shitty Wine wrappers

The prettier the distro, the harder the fall when reality hits.

## 3. Conclusion

Linux in 2025 has crossed the “minimally usable for enthusiasts” line — but it is still **very far** from being suitable as a daily driver for most normal people.

The setup friction, driver roulette, software ecosystem gaps, and terminal dependency remain massive barriers.

Most people who successfully use Linux long-term already had solid Windows / computing fundamentals — they understand filesystems, bootloaders, permissions, terminals.

Average users today are even more “巨婴化” (giant baby-ized) than before — they rage when Windows 11 moves the taskbar. Expecting them to learn Linux is delusional.

## 4. Appendix: 13-trixie & Me

After the last video, this comment stood out:

> 13-trixie:  
> Windows and Android have spoiled people with蜜罐 (honey pots). Even if Linux becomes simpler, people refuse to learn.  
> I’m an Arch user. Linux isn’t that hard. But most Chinese computer noobs can’t even use Windows properly — you expect them to understand X11 vs Wayland? apt vs dnf?  
> Videos like this point out real problems, but the root cause is users are lazy.  
> I went Windows → Ubuntu → Arch following wiki step-by-step. Everything is solvable. Calling it “hard” now is beyond me.  
> **It’s the users’ fault, not the system’s.**

I agree with the first half — but learning cost is still objectively high.

We argued in comments for three days straight.

Eventually we moved to DMs, talked about FOSS philosophy, reached mutual understanding — and yes, I finally tried pure Arch thanks to his guidance.

## 5. Closing Words

Two quotes from the comment section sum it up perfectly:

> I want medicine that comes ready to swallow — not medicine where I first have to study pharmacokinetics and pharmacology before I can take it.  
> I want a house I can move into immediately — not one where I have to mix cement, lay bricks, and waterproof everything first.  
> Same with computers: I want a system that works out of the box — not one where I have to learn command lines and programming languages just to use it.  
> — @毕偏导

And from 13-trixie himself:

> Even if I master Linux completely, if I had to pick one main system — I’d still choose Windows.  
> I need something I can instantly use for work, something truly plug-and-play — not something that requires 15 minutes of debugging every morning and might collapse completely after one wrong move.  
> I need full-featured software and excellent hardware support — not constantly tinkering with devices and settling for gimped versions of apps.  
> Only Windows delivers that. macOS is close but still lacking. Linux hasn’t even reached the entry threshold.  
> — @13-trixie
```