# Elastic-Stack-SIEM

In this guide, I'll walk you through the process of setting up a home lab for Elastic Stack SIEM using the Elastic Cloud portal and a Kali Linux VM through the VMware Fusion hypervisor. I will generate security events on the Kali VM, configure an agent to forward the data to the SIEM, and then query and analyze the logs within the SIEM platform.


# 1. Setting up the Kali Linux VM
After downloading VMware Fusion, I will download the Apple-Silicon (ARM64) Installer Image. This version of the Kali Linux installer is specifically designed for Macs with Apple-Silicon chips (such as M1, M2, or M3).

![image](https://github.com/user-attachments/assets/5c7f8c27-b771-407e-93a8-e590956dc3be)



<img width="1710" alt="Screenshot 2024-12-30 at 1 51 20 PM" src="https://github.com/user-attachments/assets/61e79e0e-33e9-4397-8351-621c5336dfd4" />

To set up Kali Linux in a virtual machine, download the appropriate VM image for VirtualBox or VMware from the official Kali Linux website, then create a new virtual machine using the downloaded image. Start the VM, follow the installation prompts, and use "kali" as both the username and password. Once installed, verify internet connectivity by pinging a site like google.com
