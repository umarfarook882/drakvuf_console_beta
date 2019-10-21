### Drakvuf Console (Log Analysis Toolkit)

### **My Goal:**

- Build a automated malware analysis sandbox using Drakvuf for Windows - 80% is done (We can't use injector when drakvuf is intialized)
	
    **Note:** If we use injector along with drakvuf to open malware sample, at first injector create new process using injection technique and then  drakvuf is intialized. So we won't get much context about how the intial malware process creation in drakvuf log.  That's why we have to open the malware sample manually, after drakvuf is intialized. 
 
- Build a drakvuf console (Log Analysis Toolkit) to visualize and extract IOC from the drakvuf log - Beta Version is ready :) 

### **Prerequisties:**

- Drakvuf (Check here https://drakvuf.com/)
- Other tools (dnschef, pdbparser, rekall, volatility - optional) 

### **Automated Malware Analysis - Drakvuf**

Using automated malware analysis setup, will be generating the following artifacts.

- Drakvuf Log (JSON)
- Tcpdump (Pcap)
- Memory Dump of analysis vm (for later analysis with volatility)

**Note:** Drakvuf git repo includes LibVMI and Xen Installation.

**Demo:**

Malware: Emotet <br/>
Sample: Emotet.exe (source from https://www.malware-traffic-analysis.net/)

[![Alt text](https://img.youtube.com/vi/FAJb1X2hX2s/0.jpg)](https://www.youtube.com/watch?v=FAJb1X2hX2s)


### **Drakvuf Console (Log Analysis Toolkit)**


Drakvuf Console is desktop app build using electronjs (quasar) to visualize and extract IOC from drakvuf log.

**Frontend:** Vue js (Quasar) <br/>
**Backend:** Elasticsearch for store drakvuf log and query result faster <br/>
**Build on:** ElectronJs <br/>

**Purpose:**

- Visualize the drakvuf log quickly and understand the malware behavior
- Extract IOC and create signature to prevent new threats

**Supported Plugin**

The following are the currently supported plugin

- Syscall (Only malicious syscall are trapped for analysis)
- FileTracer
- FileDelete
- Fileextractor
- Socketmon
- Regmon
- Procmon
- LibraryMon
- MemDump
- Tcpdump (pcap - custom parser)


**How to extract IOC from Drakvuf Log**

1. Once drakuvuf log for malware sample is generated, using drakvuf_console_client.py script will convert the Drakvuf Log into Structured JSON format.  

   `python3 drakvuf_console_client.py --output_dir <drakvuf_automated_analysis_output_dir>`
  	
2. Run the eleasticsearch service 
3. Setup the required indices for drakuv console toolkt using drakvuf_console_client.py script

    `python3 drakvuf_console_client.py --setup auth username:password` (one time setup)
   
4. Run the drakvuf console toolkit 
5. Create a new analysis for the malware sample in the drakvuf console toolkit 
6. Upload the log and select the suspicious process with "enabled child parent" option
7. Once log is uploaded sucessfully in elasticsearch, click view on the analysis project
8. Now we can visual drakvuf log in following tab

    - Overview  - Sample Information
    - ProcessGraph  - Process flow graph for selected parent process
    - Behavior - Group activities for each process

        The each process will show following activities, 

        - File
        - Process
        - Thread
        - Registry
        - Module
        - Memory
        - System
        - Driver
        - Privilege
        - Section
        - network

    - Files - Show the file information which are created and modified along with option to download the file
    - Memory   - Show information about memory event like NtWriteVirtualMemory and the dump of the memory
    - Network - Show information about the dns, tcp, udp and tcpdump pcap log
    - IOC  - Show information about IOC extracted for drakvuf log

**Demo:**


[![Alt text](https://img.youtube.com/vi/njZ_FKywiHk/0.jpg)](https://www.youtube.com/watch?v=njZ_FKywiHk)

### **Ongoing Dev**

It's just a beta version, developed to exlpore Drakvuf for my malware research. Will be improving the performance on elasticsearch.

### **Future Plan**

Will be focusing on LibVMI and also planning to add new plugin to https://github.com/tklengyel/drakvuf



### :octocat:Credits:
* [Tamas K Lengyel](https://tklengyel.com/)
* Umar Farook: [OSCE | Technology Security Analyst | DevSecops | Researcher](https://www.linkedin.com/in/Umar-Farook)
* FOS Team : [Fools of Security](https://www.youtube.com/channel/UCEBHO0kD1WFvIhf9wBCU-VQ)


### Support !
  
Email address: umarfarookmech712@gmail.com  or pingus@foolsofsecurity.com <br/>
Youtube: [Fools Of Security](https://www.youtube.com/channel/UCEBHO0kD1WFvIhf9wBCU-VQ)<br/>
Website: [Fools Of Security Community](https://foolsofsecurity.com) <br/>


### **Reference:**

- [Drakvuf](https://drakvuf.com/)
- [Drakvuf-git](https://github.com/tklengyel/drakvuf)
- [LibVMI](http://libvmi.com/)
