---
title: 'Linux is Not a God'
date: 2025-10-15 22:00:00
tags: [Operating Systems]
published: false
hideInList: false
isTop: false
---
(Image: Disclaimer)
After the release of my last video, I got all kinds of responses from you all, and also noticed some problems that the Linux community has to face head-on. This video is mainly a supplement and correction to the last one – those who are interested can go check it out.

Besides, the outline of this video was inspired by @BreezeArch, who also provided some of the materials.

In this video, I’ll walk through all the problems beginners run into when using Linux in a complete timeline. Let’s cut to the chase without further ado.

## 1. Getting Started
### 1.1 Distributions
(Image: Linux Distribution Tree)
This massive tree represents all existing Linux distributions. As we all know, the first step to getting started with Linux is to pick a suitable distribution in advance, but for beginners, choosing the right one from this huge tree is like finding a needle in a haystack. This leafy "distribution tree" hides hundreds of Linux variants – from "source-level" distributions like Debian and RedHat, to derivative branches such as Ubuntu and CentOS, and even niche custom versions like Gentoo and LFS. Each comes with entirely different labels: "Rolling Release", "Long-Term Support (LTS)", "Source Code Compilation", "Commercial Maintenance".

For beginners, this is not "freedom of choice", but "information overload". They neither understand the difference between apt and rpm package management, nor can they tell apart "the novelty of rolling updates and the risks to stability", let alone know how "community-driven development vs commercial support" impacts daily use. They can only fumble around blindly among messy recommendations.

The worst part is the "recommendation trap under the geek filter": many so-called "Friendly Geeks Online" will sing the praises of ArchLinux for its "high customizability", yet never mention that it requires manual configuration of the network, disk partitions and driver compilation – you even have to install the desktop environment by yourself. If someone buys into this rhetoric

(Image: ArchLinux live-cd interface)
they’ll download the image, stare blankly at the all-English black terminal interface of the Live-CD for half an hour, not knowing even the basic command to "mount a partition". After struggling for two days, they end up with a black screen on boot because they didn’t install the graphics card driver, and finally delete the image in frustration and give up.

(Image: Statistics)
In fact, according to 2024 statistics, the Ubuntu family accounts for 68% of the beginner market, and the core reason is its "out-of-the-box usability".

(Image: Linux Mint's interface and features)
Linux Mint, for example, comes with printer drivers pre-installed, is compatible with Windows operating logic, and even its software store is as intuitive as a mobile app market. But beginners often don’t know about these "nanny-level" options, and instead get led astray by recommendations for "niche and high-end" distributions, hitting an insurmountable wall right at the start.

### 1.2 Image Selection
(Image: Ubuntu and Linux Mint TUNA Source Lists)
Open the TUNA download page, and beginners will be instantly overwhelmed by a string of unfamiliar labels: instruction set suffixes like amd64, armv8l and riscv; image types such as LiveDVD, Server and Desktop; plus desktop environment options like xfce, mate and cinnamon. Each one is like an unsolved puzzle. These terms hide key differences that directly affect usage, yet there’s no "beginner guidance" whatsoever – beginners have to piece together the answers by looking up each term one by one.

First, instruction sets: amd64 is for most laptops and desktops with Intel/AMD architectures, but how would a beginner understand the concept of "x86 architecture"? If they mistakenly download the armv8l version, burn it to a USB drive but fail to boot, they’ll check the USB drive repeatedly and re-burn the image several times before realising they chose the wrong architecture.

Then, image types: LiveDVD is marked as "Experience Directly", and beginners think "I can save my settings after the experience", only to find that all modified preferences disappear after a restart. After looking it up, they finally learn it’s just a "temporary test environment" – to install the system, you have to click a dedicated installation program.

The choice of desktop environment hides even more "hidden pitfalls".
(Image: Screenshots of various desktop environments)
Xfce is lightweight but lacking in features, suitable for old computers but unable to meet aesthetic needs; Cinnamon has an exquisite interface but uses a lot of resources, leading to lag on low-end machines after installation; Mate strikes a balance but lacks distinctive features. Beginners often choose blindly based on names – for example, picking xfce and then complaining the "interface is too outdated", switching to Cinnamon only to find the "computer is too laggy to use", and having to re-download the image and start over.

This is extremely draining for a newcomer’s patience. This sense of torment only highlights how out-of-the-box Windows is, which is why some newcomers end up reinstalling Windows.

### 1.3 System Installation
I won’t elaborate on the choice of burning software – it’s a necessary step for installing all non-preinstalled systems. The biggest difference from installing Windows is switching from WinPE to burning software like Ventoy/Rufus.

(Image: Logos of Ventoy and Rufus)
The key point lies in a characteristic of Linux – most users can’t rely entirely on a Linux environment and need to install a dual-boot system.

(Image: Linux logo and Windows logo side by side)
This is already a big challenge, but the real difficulty is "dual-boot installation". Most people are unwilling to give up Windows, yet have no clue about "cross-system coordination".

First is BIOS settings: you have to disable Secure Boot (otherwise Linux may fail to load) and adjust the boot order. Beginners stare at the English interface, unable to find the corresponding options, and after messing around with the settings, they might even be unable to boot into Windows.

As for partitioning, the LiveCD environment of some Linux distributions offers an automatic partitioning feature. But in reality, automatic partitioning uses a "one-size-fits-all formula" to calculate the "optimal" partitions, which doesn’t align with everyone’s usage habits.

(Image: Virtual machine record, Deepin automatic partitioning program)
Some people are used to installing a lot of software, but automatic partitioning often sets the /home partition to be the largest and the / partition to be small – this can cause unnecessary trouble when you need to install a large number of software later. At other times, someone might store a ton of files in the /home partition, only to find it’s too small. You can manually drag a slider to allocate space, but if storage is limited, why have an unnecessary /home partition in the first place?

Therefore, manual partitioning is a more reliable option, but it means beginners have to first understand a bunch of new concepts: how big the /boot partition should be (at least 1GB, for storing boot files), how to share the /boot partition with Windows, the ratio of swap partition to memory (it’s recommended to set it equal to the memory size if RAM is over 4GB), the logic of space allocation between /home and /, and choosing the right file system (ext4 and btrfs each have their pros and cons).

Sometimes, if you forget to create the /boot partition, the system gets stuck at the GRUB interface on boot, and the only option is to reinstall the system. These seemingly "basic" pieces of knowledge take a complete novice half a day just to look up. While Windows also requires learning, its partitioning logic is simpler, tools are more intuitive, and there are far more "nanny-level" tutorials available.

## 2. Usage
### 2.1 Software Installation
(Image: Discover Store and the command pacman -Qs vlc)
Linux’s software installation mechanism indeed has a certain "geeky elegance". Compared to the scattered .exe installers and hidden registry residues in Windows, Linux’s package managers (APT, DNF) and sandbox tools (Flatpak, Snap) are a dream for clean freaks: open-source software can be installed with just a single command or a click in the store, which automatically resolves dependencies and standardises installation paths. When uninstalling, even configuration files can be cleared with one click, leaving the system as clean as if the software was never installed.

For example, to install the GIMP image editing software on Ubuntu, you just enter `sudo apt install gimp` – the system will automatically download all the required library files. No need to choose an installation path, no need to worry about bundled plugins. This "one-stop experience" is indeed more hassle-free than Windows. But this elegance falls apart completely when it comes to proprietary software.

(Image: DaVinci Resolve Official Website)
Professional tools like DaVinci Resolve only provide .run format installers on their official websites – on the surface, it’s like double-clicking a Windows .exe to run it, but in reality, it hides a series of pitfalls: first, you have to enter `chmod +x DaVinci_Resolve_18.6.3_Linux.run` in the terminal to grant execution permission; after finally launching the installer and opening it with excitement, you’re greeted with this:
```
Missing or outdated system packages detected.
Please install the following missing packages:
libapr1 libaprutil1 libxcb-composite0 libxcb-cursor0 libxcb-damage0 libxcb-xinput0
```
Not to mention how intimidating this wall of English is for users, how exactly do you install these lib-prefixed packages? What version and architecture should you install? What alternatives do you use if you can’t find them?

This is just the "appetiser" – the real nightmare is "Dependency Hell". Even with modern Linux distributions in 2025 and intelligent package managers, proprietary software’s stubbornness can still cause problems. To install DaVinci Resolve, users have to manually install outdated dependency libraries, only to find that the system’s built-in Chrome browser crashes (because Chrome relies on newer libraries); if you try to uninstall the old libraries to fix Chrome, DaVinci Resolve crashes as well. This catch-22 dilemma can stump even geeks who have used Linux for 5 years, let alone beginners.

In the end, you either compromise by using containers (Docker/AppImage/Flatpak) – and container packaging is another skill to learn – or you give up on DaVinci Resolve, or put up with a non-functional Chrome.

The root of these problems is proprietary software vendors’ perfunctory adaptation to the Linux ecosystem. They neither want to comply with package management norms (such as packaging software into .deb/.rpm/.flatpak formats) nor bother with dependency detection, passing the burden of "fixing the environment" entirely to users.

When users find that "installing an input method requires reading 5 tutorials, and using a video editing software requires modifying system libraries", they naturally think: "I just want a simple tool – why do I have to go through all this trouble?" This sense of powerlessness is more effective at driving beginners away than any other flaw.

### 2.2 Software Adaptation
With the gradual growth of Linux desktop users in recent years and the continuous advancement of domestic information innovation policies

(Image: Logos of UOS and Deepin)
many proprietary software vendors have finally abandoned their "ignore Linux" attitude and announced that they have "completed adaptation". But when you open these software with the expectation of "seamless switching", you’ll find that the so-called "adaptation" is more like a carefully packaged "feature cut show" – most are incomplete versions lagging 1 or 2 major releases behind the Windows version, only retaining the most basic "usable" features, with all more complex needs off-limits. The consequences of this perfunctory adaptation ultimately fall entirely on users.

(Image: Comparison of Tencent Meeting interfaces on Linux and Windows) (Image: Tencent Meeting Official Website)
Take Tencent Meeting as an example: the current Windows version has been updated to ($version number), supporting features like virtual background blurring, real-time subtitle translation, multi-person interactive annotation and whiteboard collaboration; while the Linux version is still stuck at ($version number), missing annotation, subtitles and a host of other features.

These vendors are not incapable of proper adaptation – Tencent can keep meeting features consistent across mobile, tablet and Windows platforms, and NetEase Cloud Music maintains full functionality on macOS. They just think the Linux user base is still too small to justify investing resources in in-depth adaptation, and only offer a "basic version" to meet the bare minimum requirements.

For beginners, this "half-baked adaptation" is more frustrating than "no adaptation at all". You might choose Linux because "it has no ads", only to find that your favourite songs won’t sync, the annotation feature you need for meetings is missing, and your office software crashes constantly. After spending two hours looking up tutorials, all you get are workaround answers like "Try using Wine" or "Wait for the next update".

What’s more frustrating is that as a beginner, you have almost no ability to solve these problems on your own, and can only beg vendors for updates in issue feedback. When essential software fails repeatedly, and "tinkering" becomes a daily routine, beginners’ patience will eventually run out, and they’ll end up going back to the familiar Windows – after all, people use computers to solve problems, not to endure them.

### 2.3 Driver Issues
Driver problems on Linux have never been a "new pain point", but a long-standing historical legacy that runs through the system’s development. Although NVIDIA finally softened its stance in recent years (Video: NVIDIA Fxxk You), resolving the core graphics card adaptation conflict with official closed-source drivers – no longer forcing users to choose between the 30% lower performance of the open-source Nouveau driver and manually disabling kernel modules to install the closed-source driver – this only pulled out the thickest thorn. Countless peripheral adaptation loopholes still prick beginners’ user experience like fine needles.

(Video: 13-trixie's real-life USB network card issue)
13-trixie’s experience with a USB wireless network card is the perfect example of this daily frustration. This network card works plug-and-play on Windows, but is completely unrecognisable on Linux: plug it into a USB port, and the system does nothing. After days of trial and error, a solution was found – you actually have to enter `eject sr0` in the terminal to eject the network card, which is disguised as an optical drive, before the system can recognise it.

What’s even more torturous is its stability: it might disconnect suddenly within 30 minutes, or pop up a "Limited Network Connection" prompt after 3 hours. Either way, you have to repeat the process of "unplug the device → enter a command in the terminal → plug the network card back in". Beginners can’t even understand "why a network card is disguised as an optical drive" – the mere fear of typing commands in the terminal is enough to make them give up entirely. And the current zen kernel even chooses to ignore such devices by default.

This gap – "works fine on Windows, but only functions with weird workarounds on Linux" – is the first straw that breaks the camel’s back for beginners.

More common than instability are performance degradation and feature incompleteness. Drivers maintained by the open-source community can make devices "work", but they often fail to reach the hardware’s actual capabilities: for example, a Realtek Gigabit network card using the system’s default open-source r8169 driver can’t reach the full throughput of the closed-source driver, doubling latency during large file transfers; the open-source Mesa driver supports basic display output but is incompatible with GPU rendering acceleration in some software, leading to a several-fold increase in rendering time.

Essential peripherals like printers are even worse off: some domestic printers have no native Linux drivers at all.
(Image: CUPS Web Interface)
Even if you configure them through the CUPS printing system, you have to select the driver model in CUPS’ web interface. Beginners don’t even know what CUPS is, let alone troubleshoot issues like "print job upload failed" or "double-sided printing greyed out".

Even PCIe devices built into motherboards can cause problems: various PCIe devices may not be recognised, and after installing vendor or third-party open-source drivers, you still have to edit configuration files under /etc/modprobe.d/. Just finding this directory is enough to stump a beginner for hours.

The most desperate situation is having no drivers available at all, leaving beginners begging vendors for mercy. In reality, a large number of professional devices have no Linux drivers whatsoever. Beginners can neither compile third-party community drivers nor write their own kernel modules. Yet when many beginners seek help, some people respond with an arrogant attitude: "If there’s no driver, make it yourself." If I had the ability to do that, why would I be asking for help in the first place? This is nothing less than the Linux community’s version of "Let them eat cake".

### 2.4 Shell First
(Image: Konsole Interface)
Linux’s Shell (terminal) has always been a star tool in the geek circle – geeks can type a few commands in the black window to batch rename files, deploy services with one click, troubleshoot system faults quickly, and even think that "using a mouse to click a graphical interface is a waste of time". But this "efficiency" is an entirely different experience for beginners: faced with a blank command prompt, they can only stare blankly; if the terminal suddenly spits out an error, even a minor one like "No such file or directory", they panic instantly – "Did I type something wrong? Will the system crash?"

(Image: A simple error, such as "No such command")
More importantly, resolving most "hardcore problems" in Linux is impossible without the Shell. For example, the missing DaVinci Resolve dependencies mentioned earlier – beginners have to type `sudo apt install libapr1 libaprutil1 libxcb-composite0` word for word in the terminal. Miss a single space or misspell a package name, and it’ll prompt "Unable to locate package". To install a .run format file, you have to first enter `chmod +x filename.run` to grant execution permission, then `./filename.run` to launch the installer – beginners neither understand that `chmod +x` means "grant permission", nor know that `./` refers to the "current directory". If double-clicking the .run file does nothing, they’ll just think the software is broken, and never even consider opening the terminal.

Even more complex software installations are no better.
(Image: Manual NVIDIA driver installation steps)
The entire process requires a complete set of terminal operations. Take manual configuration of NVIDIA graphics card drivers as an example:
```
# Preparation
# Confirm graphics card model:
lspci | grep -i nvidia

# Disable Nouveau driver (to avoid conflicts):
sudo bash -c 'echo -e "blacklist nouveau\noptions nouveau modeset=0" > /etc/modprobe.d/blacklist-nouveau.conf'
sudo update-initramfs -u # Ubuntu/Debian
sudo dracut --force # CentOS/RHEL

# Download NVIDIA driver
# Go to the NVIDIA official website and download the corresponding .run file for your graphics card model.

# Install the driver
# Enter pure command-line mode:
sudo systemctl set-default multi-user.target
sudo reboot

# Stop the display manager:
sudo systemctl stop gdm # GNOME desktop environment
sudo systemctl stop lightdm # LightDM desktop environment

# Grant execution permission and run the installer:
chmod +x NVIDIA-Linux-*.run
sudo ./NVIDIA-Linux-*.run
# Installation options: Register DKMS: It is recommended to select Yes. Install 32-bit compatibility libraries: Select based on your needs.

# Restore graphical interface:
sudo systemctl set-default graphical.target
sudo reboot

# Verify installation

# Load the driver module:
sudo modprobe nvidia

# Check driver status:
nvidia-smi
```
Every single term here is new knowledge for beginners, not to mention running into "missing header files" midway, with the terminal spitting out a screen full of "not found libfoo.so" errors. Even geeks have to look up documentation for this, so beginners will simply give up.

At this point, someone always retorts: "Aren’t Mint and Deepin optimised for the graphical interface, solving 99% of problems?" But it’s precisely the remaining 1% that becomes a fatal threshold for beginners – this 1% is not a "dispensable minor feature", but a "must-solve essential problem". For example, if WiFi suddenly disconnects in Mint, clicking "Connect" repeatedly in the graphical interface does nothing; in the end, you still have to open the terminal and enter `nmcli dev status` to check the device status, then `nmcli con up "WiFi Name"` to reconnect. If Deepin’s app store shows no content and restarting doesn’t help, you have to enter `sudo apt clean && sudo apt update` to clear the cache and update the package list.

For beginners, this 1% of Shell scenarios is essentially a 100% obstacle. They choose Linux possibly just to "use the computer in peace", not to "learn command-line syntax"; (A calm sea doesn’t make a skilled sailor, but I’m a damn passenger!) they expect to "solve all problems with a mouse click", not to "guess the cause of errors while staring at a black box".

When the Shell changes from a geek’s efficiency tool to an unavoidable mandatory test for beginners, that sense of powerlessness – "I wanted to save time, but ended up having to work twice as hard" – is more effective at driving them away than any other flaw. After all, no one wants to learn an entire command-line language just to "use a piece of software once" or "fix WiFi once".

### 2.5 User Administrator Principles
Sudo privileges are a double-edged sword. Geeks know that sudo is for "temporarily obtaining administrator privileges" and will type every command carefully; but beginners may hear that "you need to add sudo to solve problems" and mindlessly copy commands from the internet – for example, being misled into entering `sudo rm -rf /` (which deletes the entire system root directory) to clean the system, causing an immediate crash. Even if it’s not that extreme, they may delete the wrong software with `sudo apt remove`, along with the dependent desktop environment, leaving only a command-line interface after restarting. Beginners will just be dumbfounded: "Where did my desktop go? Is the system broken?"

They won’t reflect on the fact that they "typed the wrong command", but instead think that "Linux is too unstable, and you can’t make a single mistake". In fact, most system crashes are indeed caused by improper operations.

Windows’ fool-proof principle is far more suitable for computer newbies than Linux’s administrator principle. So instead of being cautious and prudent at all times, they prefer a system where they can mess around without breaking anything.

(Image: A ridiculous example of Debian’s automatic update breaking the system)

### 2.6 Windows Compatibility Layer (for single-system users)
(Image: WineHQ Website)
If a beginner chooses to use Linux as their only system, they’re basically forcing themselves to rely on Wine to survive – after all, too many essential software (such as office tools and single-player games) have no native Linux versions, so they have to pin their hopes on Wine, the Windows compatibility layer. But Wine has never been a "universal tool"; it’s a "precision instrument" – and at its core is the Shell, which beginners fear the most.

(Video: 13-trixie’s game crash video)
13-trixie’s experience is typical: he tried to play Senren * Banka, spent half an hour setting up a Wine prefix and installing the DXVK runtime, and finally got into the game – only for it to crash the moment he resized the window. When he restarted the game, he found that part of his progress was lost. If a beginner encounters this, they’ll just curse the terrible compatibility.

It’s not just games – daily software is just as unreliable.
(Image: Office compatibility on WineHQ)
Obviously, even the installers have mostly poor compatibility, let alone the software itself. This "seemingly usable but constantly limited" experience is more torturous than being "completely unusable".

If you want to improve performance, manually compiling DXVK will drive beginners to the brink of madness. DXVK is a plugin that optimises Wine by supporting DirectX to Vulkan rendering, which can significantly boost game frame rates – but compiling it is like reading an Advanced Linux Tutorial.

(Image: DXVK Official Website)
As a complete newbie, 13-trixie was completely confused when he first saw DXVK – where do you even download it? He chose to compile and install it. After struggling for a long time, he realised that just the download step requires learning how to use a proxy first; otherwise, GitHub’s glacial download speeds in China will make you give up entirely. It adds extra learning costs before you even start.

After finally downloading it, you have to manually copy and paste the files to the correct Wine prefix directory. Even if you get that right, the system might hit you with a "Graphics card does not support Vulkan" error – and that’s it, your hardware just gave you a death sentence, and all your hard work was for nothing.

If you give up DXVK and use Wine’s native solution instead? The performance is even worse (since it uses OpenGL), with constant graphical glitches that make the game unplayable. How bad is the performance loss? Again, take Senren * Banka as an example: on Windows 10 with an old i5 integrated graphics card, it runs a steady 60fps at maximum settings; on Linux with native Wine, the frame rate drops to a dozen fps, turning into a slideshow when the scene gets complex, with characters moving like stop-motion animation. Turn on even a single advanced rendering option, and the game crashes immediately.

Not to mention more demanding games – Cities: Skylines already uses a lot of memory, and it just crashes on launch on Linux. Daily software is no better – Photoshop CS6 has terrible brush lag, saving files is a gamble, and it throws random errors for no reason.

After going through all this, two thoughts cross your mind: either scram back to Windows, or compromise and install a dual-boot system. But dual-boot brings its own set of problems – boot conflicts, partition troubles – another huge pitfall waiting for you.

(Can insert LinuxTechTips Linux review)
Some people will definitely say: "What about Crossover and Lutris?" Bro, anyone who says that is almost certainly an overseas user with access to the international internet. Installing dependencies with Lutris in China’s internet environment (thanks to the Great Firewall) means download speeds slower than a truck hauling a hard drive. As for Crossover? As I said in the last video – the price alone is enough to drive away ordinary users.

### 2.7 Dual-Boot Problems
Dual-boot sounds like the perfect solution for exploring Linux while keeping Windows for essential use, but in practice, it hides a series of insurmountable hurdles for beginners.

First and foremost is boot conflicts. When installing a dual-boot system, Linux usually relies on the GRUB bootloader to manage boot options, but Windows system updates often arrogantly overwrite the boot record, causing the Linux option to disappear after a restart. Faced with a black screen or booting directly into Windows, beginners are completely helpless – they have no idea what "repair GRUB" means, let alone how to use Arch-LiveCD tools to execute the relevant commands.

Second is the vicious cycle of partition space. Even if you carefully allocate partitions during installation, you’ll often run into low disk space on one side during use: for example, Windows’ C drive gets full from cache bloat, or Linux’s root partition runs out of space from too many software installations. Resizing partitions is a high-risk operation for beginners – one wrong move can corrupt the entire disk partition table, leading to data loss on both systems.

Cross-system file sharing is also a headache. Linux’s read and write support for the NTFS format has improved, but permission errors and file corruption still happen occasionally; Windows has no native support for Linux file systems like ext4, so beginners who want to transfer files between the two systems have to install third-party tools – and configuring these tools requires the command line, pushing beginners back into the clutches of Shell fear.

A more hidden issue is the knock-on effect on hardware adaptation. For example, switchable dual graphics cards on a laptop may work barely on a single system, but in a dual-boot environment, the discrete graphics driver may fail on Linux, or the integrated graphics may have abnormal performance on Windows, leaving beginners stuck with "two systems that both work poorly".

Finally, there’s the hidden cost of switching between systems. Want to edit a document in Linux and then polish it with professional Windows software? You have to save the file, restart the computer, and wait for the system to load – the whole process takes far longer than expected. Imagine an emergency: you boot into Windows hoping to solve a problem stably, only to be met with frequent blue screens and insecure HTTPS connections caused by clock desync – you’ll panic immediately.

All these problems add up, turning dual-boot from a "solution" into a "source of new troubles". In the end, many beginners give up after repeated tinkering and go back to a single Windows system.

### 2.8 Deepin/UOS Linux Ver.?
Many people gush when recommending Deepin or UOS: "Look at this frosted glass effect! The animations are smoother than macOS! The input method is pre-installed, QQ and WeChat can be installed with one click, and even Wine is configured for you – unlike other distributions where you have to tinker with everything yourself!" (Can insert Primitive UI demo @GeekLoverOnlyColumbina)

It’s true – the Deepin team has spared no effort to make it "out-of-the-box": the input method is pre-installed, an app store is built-in, even ntfs-3g is configured, so it can recognise NTFS partitions right after boot. For newbies just getting into Linux, it’s like jumping straight from "surviving in the wild" into a "well-decorated apartment".

But the problem is, this apartment only looks good as a show home – when you actually move in, you’ll find the water pipes still leak and the wiring is still outdated. At its core, Deepin/UOS is still Linux – it just does the dirty work for you upfront, like installing the input method and configuring Wine, but when it comes to underlying ecosystem problems, it’s just as helpless as any other distribution.

Tencent Meeting’s Linux version has no annotation feature? Deepin users can only stare blankly too. Can’t find a driver for an old printer? You’ll still end up opening the terminal and entering `sudo apt install` to find an alternative package. Want to use DaVinci Resolve for video editing? You’ll still be greeted with a screen full of missing dependency errors, and you’ll have to install those missing lib libraries manually.

What’s more ironic is that the "one-click install" Windows software in Deepin’s app store is essentially running on a Crossover-like mechanism under the hood. The hassle of configuring the free version of Wine is hidden, but the compatibility issues are almost all still there.

The biggest problem is that Deepin’s "friendliness" can actually become a stumbling block for beginners looking to advance. Because everything is too easy at first, they never get the chance to learn concepts like partitioning, boot loaders and dependencies. Then one day, the system breaks after an update (Deepin’s update frequency is slow, but problems still happen), or they want to install software not available in the app store (like the latest version of Blender) – and they’re suddenly faced with the terminal they’ve never seen before.

This puts them in an even more awkward position than Ubuntu beginners: Ubuntu users know from day one that they have to learn some command line, but Deepin users are spoiled by the "pride of domestic software" and think Linux is now as fool-proof as Windows – so when they hit a real problem, they fall apart completely, and end up sighing that "domestic software is still no good".

## 3. Conclusion
In summary, my conclusion is this: Linux is still not suitable for most individual users to use as their main system, even though it has crossed half the threshold of user-friendliness. But at the very least, it won’t go mainstream in the next few years – its less than user-friendly operation guidance and the relatively difficult initial setup are more than enough to drive away people who can’t even use Windows properly.

Most people who become Linux users have a solid foundation in basic computer theory (or put simply, they’re pretty good at using Windows), can understand basic computer concepts like operating systems, partitioning, boot loaders and the command line, and know how to use them. Because the number of people who actually take the time to learn the basics of computers is still small – especially with the current trend of users being overly coddled. People even complain about the UI changes in Windows 11, let alone Linux’s high learning curve.

## 4. Addendum: 13-trixie and Me
After the release of my last video, I noticed a comment in the comment section:
>13-trixie:
>Windows and Android have spoiled people rotten. Even if Linux gets simpler, they still won’t want to learn it.
>Also, I’m an Arch user myself. Linux isn’t actually that hard, but there are tons of computer newbies in China. People who can’t even use Windows properly aren’t going to tinker with X11 or Wayland, are they? Or learn apt or dnf?
>I don’t deny Linux has problems with these videos, but the root cause is that users are too lazy to learn. How simple the system is is secondary.
>I also switched from Windows to Ubuntu, then to Arch. Things that can be solved mindlessly by following the documentation are now considered difficult – I can’t wrap my head around that.
>**It’s the users’ problem, I don’t think we should bash the system for being hard to use.**

I agree with the first half of his first sentence, but I still think Linux’s learning curve is quite steep. We argued in the comment section for about three days, exchanging dozens of comments about learning costs, software adaptation and dependency issues.

Talking to him made me suddenly realise why most Linux users rave about the system so much: not a single one of them ever looks at it from a complete newbie’s perspective, and almost no one evaluates it objectively – if you do, you’ll be labelled as "disrespecting the open-source community".

(Image montage: Arrogance?)
Some unscrupulous "Contributors" act recklessly in the community, talking down to users who are desperate for help, and spouting extreme opinions in the comment section. They’re just a bad apple that spoils the whole barrel.

(Image: Toxic comments?)
Sorry, I got off track.

As you all know, the argument ended with 13-trixie conceding. (Image: n private messages) We reached an agreement in private messages, talked a lot about our thoughts on free and open-source software, and finally decided to make this video. And with his guidance, I finally got to try the legendary Arch Linux.

## 5. Epilogue
At the end of the video, I’ll leave you with a comment from the comment section:
>I need to take medicine. I need a blister pack that I can open and take right away – not medicine where I have to learn its pharmacokinetics and pharmacology first before I can take it.
>I want to buy a house. I want a house that I can move into immediately – not one where I have to mix concrete, lay bricks and do waterproofing first before I can live in it.
>Likewise, when I buy a computer or a phone, I want a device that’s ready to use out of the box – not one where I have to learn the command line and various programming languages first before I can use it.
>——@Bi Piandao

And 13-trixie also said:
>Even if I master Linux completely, I’d still choose Windows as my main system.
>Because I need a system that I can pick up and use immediately for work, one that’s out-of-the-box – not one that I have to debug for ten minutes only for it to still not work, one that crashes and loses everything after hours of tinkering.
>I need a system with full features and good device support – not one where I have to keep adjusting my hardware, and where the software is only a basic version.
>And in this regard, only Windows delivers. macOS falls a bit short, and Linux hasn’t even crossed the threshold.
>——@13-trixie
