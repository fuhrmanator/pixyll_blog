---
layout: post
title: Pharo in Windows Subsystem for Linux (WSL)
date: 2019-02-27T00:00:00.000Z
summary: How to run Pharo in Windows Subsystem for Linux (WSL)
categories: null
published: true
---

Pharo 7 runs well in Windows 10 (I have a Surface Pro 4), but I wanted to do some testing of a project also under Linux. Initially I had run Ubuntu in a VM VirtualBox, but given Windows Subsystem for Linux (WSL) is now Ubuntu 18 and is much lighter weight on disk space, I wanted to see if it would work with Pharo.

Since [Pharo.org](http://Pharo.org) doesn't yet have specific instructions for installing on Ubuntu 18, I was unsure how to proceed. So, I went with the KISS principle and did a command-line (ZeroConf) install, which was successful. Here are the steps:

- Install and activate WSL following [Microsoft's instructions](https://docs.microsoft.com/en-us/windows/wsl/install-win10).
- Install an X Server for Windows. I used [VcXsrv](https://sourceforge.net/projects/vcxsrv/) mentioned in the instructions [here](https://jaipblog.wordpress.com/2018/01/21/running-linux-gui-apps-on-windows-10/). You must `export DISPLAY=localhost:0` (e.g., in your WSL `~/.bashrc`).
- Install [Mesa](https://wiki.debian.org/Mesa) with the command `sudo apt install mesa-utils`. This is apparently needed because there are missing libraries for the X11 display used by Pharo. I'm not sure if this is the official dependency, but it worked in my case. For reference, if you don't do this step, you'll get the following message that's somewhat misleading IMO:

  ```
  $ ./pharo-ui
  could not find display driver vm-display-X11; either:
  - check that /home/myusername/pharo-dir/pharo-vm/lib/pharo/5.0-201901051900//vm-display-X11.so exists, or
  - use the '-plugins <path>' option to tell me where it is, or
  - remove DISPLAY from your environment.
  ```

- Install Pharo with ZeroConf command line as below:

  ```
  $ mkdir MyPharo
  $ cd MyPharo/
  $ curl -L https://get.pharo.org/64/ | bash
  ```

- Start the X Server on Windows (e.g., XLaunch from the Start menu in Windows 10).
- Run Pharo and have fun in Ubuntu 18 (WSL)

  ```
  $ ./pharo-ui
  ```
  
  ![Pharo 7 Unix running in an XWindow]({{site.baseurl}}/images/Pharo7WSL.png)


It also works with the [Pharo Launcher](http://pharo.org/download).
