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

> Some tools depend on where I am.

## Make the `T` work on a [Surface Pro X](https://www.microsoft.com/en-us/search/result.aspx?q=Surface+Pro+X)

The Surface Pro X comes with Windows 10 for ARM and I wanted to have a machine that I can carry around and that also has touch input with a pen I don't lose easily. Additionally, what made me decide for the X was the ability to be always connected via LTE. Lets see how this worked. 

I bought the 16GB RAM / 256GB disk bundle as I have an complete cloud desktop with a Debian VM where I do most of the heavy lifting for everything not related to physical devices. Since we are an IoT startup I have to be able to access physical devices now and then. 

...
