<p align="center">
<img width="600" height="300"  alt="download (1)" src="https://github.com/user-attachments/assets/17a37c1d-3eca-4976-a339-0e2fd80fe10e" />
</p>

<h1>Zabbix Monitoring Deployment</h1>
Zabbix is an open-source enterprise monitoring platform used by organizations to track the health, performance, and availability of their IT infrastructure. It provides real-time visibility across servers, virtual machines, networks, applications, and cloud environments — all from a single centralized dashboard. This demonstration will showcase a small monitoring environment using Zabbix to installing and configuring monitoring agents, setting up triggers, creating dashboards, receiving alerts, and responding to simulated incidents. <br />


<h2>Environments and Technologies Used</h2>

- Digital Ocean (Virtual Machines/Compute)
- Putty

<h2>Operating Systems Used </h2>

- Ubuntu 24.04 (LTS) x64
- Centos 9 Stream x64
- Windows 11 x64


<h2>Setting up Items and Triggers</h2>

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/b8b97c73-51a9-40dc-acee-a7602a9d4c36" /> <img width="400" alt="image" src="https://github.com/user-attachments/assets/b0b0e16f-af60-473e-bd7a-395fe236cf96" />
</p>
<p>
Each of these hosts that I created has many items and those items were configured automatically because I assigned templates. Now, instead of using a template, I'm going to manually configure these items. I started off with Host-2 and clicked unlink and clear to clear the template and hit update. Host 2 now has no items, triggers, graphs, and discoveries rules to it.
</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/21e13126-a956-4136-8a78-3ac338eeb1dd" /> <img width="400" alt="image" src="https://github.com/user-attachments/assets/1392e59c-7ff0-4f13-a9b1-9f1477971590" />

</p>
<p>
Then I manually created items for Host-2.
</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/b24d23da-4f87-42e2-8679-7f6125db854f" /> <img width="400" alt="Screenshot 2025-12-24 221737" src="https://github.com/user-attachments/assets/3e83fbd9-b9dd-4e7a-bad3-e7dc7c604204" />
</p>
<p>
Now for the triggers. The first one, I titled "No data for 60 seconds." Then in expression, I selected Zabbix Agent Ping which was the item I created previously. For function I chose No data received during a period of time then, in last of time, I added 60 seconds and result equals to 1. So if there is no data coming from Host-2 for 60 seconds, it will equal to 1 therfore switching the trigger which will then send an alert.
</p>
<br />

<p>
<img width="500" alt="Screenshot 2025-12-24 222123" src="https://github.com/user-attachments/assets/7ff47894-73a5-4bc0-a08f-5d04d925f003" />
</p>
<p>
The second trigger I made
</p>
<br />

<p>
<img width="500" alt="Screenshot 2025-12-24 222326" src="https://github.com/user-attachments/assets/9ed16979-4ac6-4e7a-8602-450c2db925b5" />
</p>
<p>
The third trigger I created is CPU
</p>
<br />

<p>
<img width="400" height="115" alt="image" src="https://github.com/user-attachments/assets/db69814c-5291-459a-95d9-a4c29ea822a3" /> <img width="400" alt="Screenshot 2025-12-24 224024" src="https://github.com/user-attachments/assets/bf8c8b45-82e0-455d-96b7-bc1dde1b59e4" />
</p>
<p>
Now I'm going to test the triggers. If I go into Host-2, and type in the command "service zabbix-agent stop," then go to Monitoring → Problems, there will be a new problem show on Host-2 with a Disaster Severity level. This will also appear in Monitoring → Hosts with a yellow icon under availability saying there's a problem with Host-2. If I also click update problem, I could put a note in there so if anybody else is monitoring Zabbix, they will see the information provided on the problem.
</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/bcf23f45-7b30-439c-a3eb-946f2272500b" /> <img width="400" alt="Screenshot 2025-12-24 224158" src="https://github.com/user-attachments/assets/dfb7cf2f-90fe-4848-9275-501506b9481b" />
</p>
<p>
Then, on Host-2 again, if I type in, "service zabbix-agent start," then the issue will then quickly resolve itself.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
