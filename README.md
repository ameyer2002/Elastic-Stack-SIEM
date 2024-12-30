# Elastic-Stack-SIEM

In this guide, I'll walk you through the process of setting up a home lab for Elastic Stack SIEM using the Elastic Cloud portal and a Kali Linux VM through the VMware Fusion hypervisor. I will generate security events on the Kali VM, configure an agent to forward the data to the SIEM, and then query and analyze the logs within the SIEM platform.


# 1. Setting up the Kali Linux VM
After downloading VMware Fusion, you will download the Apple-Silicon (ARM64) Installer Image. This version of the Kali Linux installer is specifically designed for Macs with Apple-Silicon chips (such as M1, M2, or M3).

![image](https://github.com/user-attachments/assets/5c7f8c27-b771-407e-93a8-e590956dc3be)


Open the directory in which the .iso was saved after downloading. Drag the downloaded .iso to the window and begin the installation (Debian 12.x 64-bit Arm). We can also just  click on “install from disk or image”, or “use another disc, or disc image” option from the VMware Fusion application window.

![image](https://github.com/user-attachments/assets/31b69dc9-2f4d-44cf-8045-60f9ae0dac01)
![image](https://github.com/user-attachments/assets/46c3f03b-c9e3-4f59-87b3-cda4d676a136)
![image](https://github.com/user-attachments/assets/9a874344-e279-4177-8383-742b24e381a6)




Start the VM, follow the installation prompts, and use "kali" as both the username and password. Once installed, verify internet connectivity by pinging a site like google.com.

<img width="1710" alt="Screenshot 2024-12-30 at 1 51 20 PM" src="https://github.com/user-attachments/assets/61e79e0e-33e9-4397-8351-621c5336dfd4" />

# 2. Setting up the Agent to Collect Logs
The next step is to create an account in Elastic and then head over to integrations in Kibana. Search for "Elastic Defend" and download.

<img width="1710" alt="Screenshot 2024-12-30 at 2 58 09 PM" src="https://github.com/user-attachments/assets/470bc49b-07c4-4129-a754-830d0265a119" />


Make sure "Linux Tar" is selected and then copy that command to your clipboard which will then be pasted into the Kali terminal command line.

![image](https://github.com/user-attachments/assets/e73c0c66-f59f-4928-bb53-f4bba1f70c57)

![image](https://github.com/user-attachments/assets/e1a82aa8-3705-4f1b-a9a8-0163f593d257)



Once the agent is installed, which may take a few minutes, you should see a message indicating that the "Elastic Agent has been successfully installed." The agent will then begin automatically collecting and forwarding logs to your Elastic SIEM instance. However, it might take a few minutes for the logs to appear in the SIEM.

![image](https://github.com/user-attachments/assets/57cad58b-6bf0-4e5e-891f-cf10c65d801c)

You can also verify that the agent has been installed by running the command: sudo systemctl status elastic-agent.service

<img width="645" alt="Screenshot 2024-12-30 at 4 00 35 PM" src="https://github.com/user-attachments/assets/c9a80db2-2117-4b18-8631-24886865e911" />

# 3. Generating Security Events on Kali VM

Since Nmap already comes preinstalled in Kali, open a new terminal and start running some of these commands. These scans generate security events, such as the detection of open ports and the services running on those ports.

# Root Terminal Emulator:

nmap -sS (ip address)

nmap -sT (ip address)

nmap -p- (ip address)

nmap -A -p- (ip address)

# Terminal Emulator:

sudo nmap -sS (ip address)

sudo nmap -sT (ip address)

sudo nmap -p- (ip address)

sudo nmap -A -p- (ip address)

You can also just type "local host" in place of your host IP address which will return the same results.






