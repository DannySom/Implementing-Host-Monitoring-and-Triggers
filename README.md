<p align="center">
<img width="600" height="300"  alt="download (1)" src="https://github.com/user-attachments/assets/17a37c1d-3eca-4976-a339-0e2fd80fe10e" />
</p>

<h1>Zabbix Monitoring Deployment</h1>
In this repository, I configured custom Zabbix items, triggers, and graphs to monitor system performance and service availability across a network.

- Items were created to collect key metrics such as CPU utilization, memory usage, disk space, and service status using the Zabbix Agent, SNMP, and ICMP checks.

- Triggers were configured to evaluate collected data and detect abnormal conditions, such as high resource utilization, host unavailability, or service downtime.

- Graphs were designed to visualize performance trends over time, allowing for quick identification of spikes, degradation, and capacity concerns. <br />


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
<img width="400" alt="image" src="https://github.com/user-attachments/assets/21e13126-a956-4136-8a78-3ac338eeb1dd" /> 

</p>
<p>
Then I manually created items for Host-2. Each item monitors a specific metric that reflects system health. Triggers cannot exist without items, because triggers evaluate item data.


| name         | type   | keys                     | units  |
|--------------|--------|--------------------------|--------|
| Zabbix Agent Ping    | Zabbix Agent  | `agent.ping`          |       |
| Free Space  | Zabbix Agent    | `vfs.fs.size[/,free]`                  | B     |
| CPU      | Zabbix Agent  | `system.cpu.util[,user]`    | %   |

`agent.ping` verifies that the Zabbix agent is reachable and responding. If the agent stops responding, no monitoring data can be collected. </p>
`vfs.fs.size[/,free]` monitors available disk space on the root filesystem. Low disk space is a common cause of system and application failures. </p>
`system.cpu.util[,user]` monitors CPU utilization caused by user processes. High user CPU usage can indicate overloaded applications which consumes a lot of resources.</p>

</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/b24d23da-4f87-42e2-8679-7f6125db854f" /> <img width="400" alt="Screenshot 2025-12-24 221737" src="https://github.com/user-attachments/assets/3e83fbd9-b9dd-4e7a-bad3-e7dc7c604204" />
</p>
<p>
Now for the triggers. The first one, I titled "No data for 60 seconds." Then in expression, I selected Zabbix Agent Ping which was the item I created previously. The expression I put was "nodata(/host/agent.ping,60)=1." This fires if Zabbix hasn’t received a ping from the agent in 60 seconds. If this triggers, it could indicate the host is down, the network is unreachable, or the agent has failed. Without this trigger, I might not notice other metrics stop reporting.
</p>
<br />

<p>
<img width="600" alt="Screenshot 2025-12-24 222123" src="https://github.com/user-attachments/assets/7ff47894-73a5-4bc0-a08f-5d04d925f003" />
</p>
<p>
The second trigger I made is for Disk Space. The expression I put was "last(/host/vfs.fs.size[/,free]) < 5000000000." This fires when free disk space on / drops below 5 GB. Disk-full conditions can crash services or cause application errors.
</p>
<br />

<p>
<img width="600" alt="Screenshot 2025-12-24 222326" src="https://github.com/user-attachments/assets/9ed16979-4ac6-4e7a-8602-450c2db925b5" />
</p>
<p>
The third trigger I created is for CPU usage. The expression I put was "avg(/host/system.cpu.util[,user],2m) > 75." This fires if average CPU usage by user processes exceeds 75% over 2 minutes. High CPU can indicate overloaded applications.
</p>
<br />

<p>
<img width="400" height="115" alt="image" src="https://github.com/user-attachments/assets/db69814c-5291-459a-95d9-a4c29ea822a3" /> <img width="450" alt="image" src="https://github.com/user-attachments/assets/39e292ce-f896-471b-8883-21b9bb6e4a93" /> <img width="400" alt="image" src="https://github.com/user-attachments/assets/32e12f4c-6160-4106-8e40-0cdfd5382b7c" />

</p>
<p>
Now I'm going to test the dashboard to see if Zabbix server will give me a response if an agent goes down. I went into Host-2, and typed in the command `service zabbix-agent stop.` </p>
Once the agent was stopped, Zabbix detected the issue and displayed a new problem under Monitoring → Problems, classified with a Disaster severity level. The issue was also reflected in Monitoring → Hosts, where Host-2 showed a red availability indicator, signaling a problem state. </p> The error message states "Get value from agent failed: Cannot establish TCP connection to [[10.120.0.3]:10050]: [111] Connection refused"</p>
This error confirmed that the network is Ok, the Host is up, but the Agent is down. If the host was actually down, then the error message would state that the host is unreachable and couldn't ping host-1 but we could still ping the Host </p>
If I also click update problem, I could put a note in there so if anybody else is monitoring Zabbix, they will see the information provided on the problem. </p>
</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/bcf23f45-7b30-439c-a3eb-946f2272500b" /> <img width="450" alt="image" src="https://github.com/user-attachments/assets/02cf0bdf-ea17-4234-8c3f-4d193fd27534" />

</p>
<p>
To resolve the incident, I restarted the Zabbix Agent service on Host-2 by typing `service zabbix-agent start` . Zabbix then automatically detected recovery, cleared the alert, and restored the host to a normal operational state. </p>
This test confirmed that triggers were correctly configured to detect service outages, generate alerts, and resolve incidents once the underlying issue was corrected.
</p>
<br />

<p>
<img width="600" alt="Screenshot 2026-01-01 160652" src="https://github.com/user-attachments/assets/c8f3e190-3784-469a-8aca-1d55dbaf5530" />

</p>
<p>
I added a couple more items. These will be used to create the graphs.
  
| name         | keys   | type                     | units  |
|--------------|--------|--------------------------|--------|
| Total Memory    | `vm.memory.size[total]`  | Numeric (unsigned)          | B      |
| Free Memory  | `vm.memory.size[free]`    | Numeric (unsigned)`                  | B     |
| CPU Utilization      | 	`system.cpu.util`  | Numeric (float)    | %   |
| CPU Utilization (5)     | `system.cpu.util[,,avg5]`  | Numeric (float)    | %   |
| CPU Utilization (15m)      | `system.cpu.util[,,avg15]`  | Numeric (float)    | %   |

</p>
<br />

<p>
<img width="400" alt="image" src="https://github.com/user-attachments/assets/7f638f2c-a418-43ab-b6c1-823a58267cde" /> </p> <img width="600" alt="Screenshot 2026-01-01 162731" src="https://github.com/user-attachments/assets/ee39967f-a65b-4dc9-8f67-02a29795f4ae" />

</p>
<p>
Now to create the graphs. I added two items which was the two items that I had just created for memory which was Total Memory and Free Memory.</p>
I could choose to adjust the functions, lines, y axis side, and colors to make it easier to view but for now, I leave them at default.
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
