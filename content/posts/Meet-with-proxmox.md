--
title: "Meet with Proxmox"
date: 2026-05-18T22:35:32+02:00
draft: false
---

## Meet with Proxmox

I have a used laptop with 64 GB RAM and 1 TB storage. So, what now?
I need Virtual Machines to run Kubernetes nodes, CI/CD pipelines, and maybe a firewall and VPN ... and goes on...

I needed Type 1 Bare-Metal virtualizytion solution. It should be free, there shoudl be a lot of documentation. So I found Proxmox. 

To be honest, I always used cloud or Vmware for VMs (Virtual Machines). I had no idea about Proxmox. Now I love it!

Enough with talking.

### Installing Proxmox 
- Take note IP of default gateway and DNS server in your home network
- Check date time. It is a simple step, but check it, check timezone
- Turning off the screen on a laptop running Proxmox:

    Configure lid power settings:
    Open the /etc/systemd/logind.conf file for editing.
    - Find and change these lines (remove the `#` to uncomment):
    - `HandleLidSwitch=ignore`
    - `HandleLidSwitchExternalPower=ignore`
    - `HandleLidSwitchDocked=ignore`
    Save (Ctrl+O, Enter) and Exit (Ctrl+X), then restart the service:
      `systemctl restart systemd-logind`
- Professionalize the Repositories:
    Proxmox defaults to an "Enterprise" repository that requires a paid subscription. Since you are likely using the free version, you’ll get errors during updates unless you switch to the No-Subscription track.
    - Remove Enterprise: Go to your Node -> Repositories and disable the pve-enterprise list.
    - Add No-Subscription: Click Add, select "No-Subscription" from the dropdown, and save.
- Test your internet speed. You will download ISO files next. So be sure about your network speed.
    `t=$(date +"%s"); wget http://speedtest.tele2.net/100MB.zip -O ->/dev/null ; echo -n "MBit/s: "; expr 8 \* 100 / $(($(date +"%s")-$t))`
- Update packages: apt update && upgrade
