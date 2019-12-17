## Adventures in the Windows ARM64 world

As the CTO of a small startup ([ubirch.com](https://ubirch.com)), my job jumps between management and development a lot. While the `C` part takes quite some time, now and then I need to switch over to `T` and do stuff the hard way. I have worked with Apple computers for years now, because they are a good mix of what I need on the command line while still providing a good UI experience all over.

My toolchain consists of (incomplete list) 
- command line terminal (bash, awk, ...)
- languages (Java VM, C/C++, Python, MicroPython, Golang, Assembler, ...)
- [Jetbrains](https://jetbrains.com) tools (IntelliJ IDEA, CLion, ...)
- [Kubernetes](https://en.wikipedia.org/wiki/Kubernetes)
- [Docker](https://www.docker.com/)
- a mail client (Mail.app, [Mailbird](https://getmailbird.com/))
- a web browser [Brave](https://brave.com)
- [Slack](https://slack.com)
- some chat tools ([Signal](https://signal.org), [WhatsApp Desktop](https://www.whatsapp.com/), [Keybase](https://keybase.io))
- [Adobe](https://adobe.com) stuff
- VPN (OpenVPN, IPSec)
- [Google Suite](https://gsuite.google.com/)
- password managers ([1Password](https://1password.com), [gopass](https://github.com/gopasspw/gopass))

## Make the T work on a [Surface Pro X](https://www.microsoft.com/en-us/search/result.aspx?q=Surface+Pro+X)

The Surface Pro X comes with Windows 10 for ARM and I wanted to have a machine that I can carry around and that also has touch input with a pen I don't lose easily. Additionally, what made me decide for the X was the ability to be always connected via LTE. Lets see how this worked. 

I bought the 16GB RAM / 256GB disk bundle as I have an complete cloud desktop with a Debian VM where I do most of the heavy lifting for everything not related to physical devices. Since we are an IoT startup I have to be able to access physical devices now and then. 

This is going to be a list of what I did to make it work for me (WIP):

### Base system
- first thing: upgraded to `Windows 10 Pro`, not having an encrypted disk and we need some developer stuff
- Browsers work okay in their Windows 32bit x86 variant
- 1Password doesn't work natively, but the browser extension for 1password online works
- enable [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and install a Linux distro
- get an X Window Server (I bought [X410](https://token2shell.com/x410/) as it was a $9.99 deal)
> I used the [setup for WSL2 from the X410 support page](https://token2shell.com/howto/x410/using-x410-with-wsl2/) to make sure I can 
> communicate with the host. Its not the ideal setup as it requires the X server to be allowed external connections. Additionally, I 
> went for the [X410 sidekick](https://token2shell.com/howto/x410/xidekick/) that allows a Linux program to be started easily. However I 
> modified the script slightly to allow for any X11 program to be started:
> ```bat
> @echo off
> start /B x410.exe /wm
> ubuntu.exe run "export DISPLAY=$(cat /etc/resolv.conf | grep nameserver | awk '{print $2; exit;}'):0.0; xfsettingsd --sm-client-> disable; cd; %1
> ```
- for the sake of simplicity, I use the windows file system for storage of stuff, so I linked Documents, Desktop and Downloads from `/mnt/c/Users/...`
- for ssh simplicity, I installed keychain: `sudo apt install keychain`
- as I use Keybase a lot, I need a way to communicate with it. It requires the GPG executable, but we need to compile and install Keybase itself from scratch. The GUI part won't work and I ignored it. 
- gopass needs to be compiled (requires a working go env)
- [Viscosity](https://www.sparklabs.com/viscosity/) is fortunately an OpenVPN client that has a native ARM64 binary of OpenVPN and works well

### Development tools
- as I do need local dev tools sometimes, I went and installes the [Java SDK 1.8 for ARM](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) (the only available as of this writing)
- the Jetbrains tools are now a no-brainer
- go is [installable](https://github.com/golang/go/wiki/Ubuntu) via Ubuntu
- Visual Studio Code works nicely, and also can use the serial port (Windows side), but I sometimes need the serial port on the Linux side and WSL2 does not yet allow that, see below.

### Stuff to come ...

- serial port forwarding (yes, I need that): there is a tool called [com0com](http://com0com.sourceforge.net/) which contains a compatible server/client ([hub4com](https://sourceforge.net/projects/com0com/files/hub4com/)) that also works with linux [ser2net](https://sourceforge.net/projects/ser2net/) or other tools (socat) and I can use it to port forward through ssh. However, we need to compile it for ARM64, which in turn requires a [Visual Studio](https://visualstudio.microsoft.com/) installation with the ARM64 MSC libraries. The compilation works beautifully after setting the target for ARM64. Now I need to learn how to use it.
  - https://gist.github.com/DraTeots/e0c669608466470baa6c
  - https://robosavvy.com/forum/viewtopic.php?t=7578
  
  
  
