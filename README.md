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

<img width="1706" alt="Screenshot 2024-12-30 at 8 09 43 PM" src="https://github.com/user-attachments/assets/bb1d11e2-2916-4919-bf44-17ed7bc6bfcf" />


Make sure "Linux Tar" is selected and then copy that command to your clipboard which will then be pasted into the Kali terminal command line.

<img width="1703" alt="Screenshot 2024-12-30 at 3 36 06 PM" src="https://github.com/user-attachments/assets/9369d867-977e-455f-994b-7dfd9620b414" />


![image](https://github.com/user-attachments/assets/e1a82aa8-3705-4f1b-a9a8-0163f593d257)



Once the agent is installed, which may take a few minutes, you should see a message indicating that the "Elastic Agent has been successfully installed." The agent will then begin automatically collecting and forwarding logs to your Elastic SIEM instance. However, it might take a few minutes for the logs to appear in the SIEM.

![image](https://github.com/user-attachments/assets/57cad58b-6bf0-4e5e-891f-cf10c65d801c)

You can also verify that the agent has been installed by running the command: sudo systemctl status elastic-agent.service

<img width="645" alt="Screenshot 2024-12-30 at 4 00 35 PM" src="https://github.com/user-attachments/assets/c9a80db2-2117-4b18-8631-24886865e911" />

# 3. Generating Security Events on Kali VM

Since Nmap already comes preinstalled in Kali, open a new terminal and start running some of these commands. These scans generate security events, such as the detection of open ports and the services running on those ports.

# Root Terminal Emulator:

nmap -sS (ip address)   SYN scan

nmap -sT (ip address)   TCP connect scan

nmap -p- (ip address)   Port scan


# Terminal Emulator:

sudo nmap -sS (ip address)   SYN scan

sudo nmap -sT (ip address)   TCP connect scan

sudo nmap -p- (ip address)   Port scan


You can also just type "local host" in place of your host IP address which will return the same results.

<img width="643" alt="Screenshot 2024-12-30 at 4 37 00 PM" src="https://github.com/user-attachments/assets/35cbce4f-cb3e-45d9-8bc9-36b124f03d60" />


# 4. Querying Security Events in the Elastic SIEM

After generating security events using Nmap, you'll want to go back to Elastic and under Observability, click on "Logs". Use the search query "process.name: "nmap"" or "process.args: "nmap"". It can take a while for the events to show up on the SIEM so I am using events from this past week for this section. The results of the search query will be shown in the table below. You can view more details within each log as well.


![image](https://github.com/user-attachments/assets/9a16fe0e-2ffe-4ed1-b161-6581995d41d0)


# 5. Creating a Dashboard to Visualize the Events

Creating a dashboard is great for analyzing logs and identifying patterns or anomalies in the data. The dashboard below will show a count of security events over time. I chose to show events from the past 30 days. To create this dashbaord, go to "Dashboard" under "Analytics" and create a visualization.


<img width="1701" alt="Screenshot 2024-12-30 at 8 02 04 PM" src="https://github.com/user-attachments/assets/4570ea80-d675-48ce-8264-e3b4ffab884f" />


# 6. Creating an Alert

To create an alert, you must create a predefined rule first so that it can trigger specific actions when certain conditions are met. For this project, I created a rule to detect Nmap scans. To create a rule, go to "Alerts" under the "Security" tab, click on "Manager rules", and click "Create new rule". The rule I created can be seen below. I personally chose to be notified through email whenever a Nmap scan is conducted, however, you can choose any action that best suites you. 

![image](https://github.com/user-attachments/assets/dd799f51-a382-41b8-98bf-0c47e6fba4a2)
![image](https://github.com/user-attachments/assets/66fcd115-1221-44cc-827a-e429aa8eb10e)

# Alerts
<img width="1701" alt="Screenshot 2024-12-30 at 8 32 44 PM" src="https://github.com/user-attachments/assets/1f5546ed-bb94-49f4-ae7c-e2432bd37b72" />

# Summary
In this project, a home lab was set up using Elastic SIEM and a Kali Linux VM. First, I installed and configured the Elastic Defend agent on the Kali VM to collect and forward security-related logs to the Elastic SIEM. I then generated security events by running Nmap scans on the Kali VM, and used the Elastic SIEM to query and analyze these logs. To enhance visibility, I created a dashboard to visualize the events over time. Finally, I set up an alert to detect Nmap scan events, which automatically triggered notifications when such activities were detected. This project demonstrated the process of setting up a SIEM environment, generating and analyzing security events, and creating monitoring alerts.

















