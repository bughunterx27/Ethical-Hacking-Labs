# Detecting DoS Attack traffic
KFSensor is a Windows-based honeypot IDS. It acts as a honeypot to attract and detect hackers and worms by simulating vulnerable system services and Trojans. 
By acting as a decoy server, it can divert attacks form critical system and provides a higher level of information than firewalls and NIDS alone.

## Objectives
Detect DoS attack using KFSensor
Analyze the incoming packet dump using Wireshark

## Requisites
Windows 10 virtual machine
Windows Server 2012 or 2016 virtual machine
Kali Linux virtual machine

## Setting up
1. Install KFSensor and Wireshark on Windows 10 virtual machine.

2. Launch the KFSensor as Administrator.

3. Click on ## Settings on the top menu and Set Up Wizard:
  ![image](https://github.com/user-attachments/assets/a4125ae8-0ccc-4941-b34a-3cd8f380f3d4)

Leave the options as default until and stop on DoS options.

4.Select Cautious from Denial of Service Options drop-down list, and select Enable packet dump files from the Network Protocol Analyzer drop-down list:

![image](https://github.com/user-attachments/assets/20eef005-bf19-4f25-91da-d6b747842abe)



5. Click next and Finish the wizard:

   
![image](https://github.com/user-attachments/assets/6f46e28b-981f-4851-b2e1-4774f8f8b149)

On the left panel you will see the FTP icon is green, and the FTP section is empty, it means currently there is no traffic through port 21.


![image](https://github.com/user-attachments/assets/59290359-e1b3-4891-8748-94e6ff07d150)

Now, the KFSensor is configured to detect the DoS attacks.

## Perform DoS Attack
Switch to the Kali Linux and open a new terminal window.
  1. Check if the port 21 is open:
     ```bash
     nmap -p 21 <Windows 10 IP address>

```bash
    Starting Nmap 7.80 ( https://nmap.org ) at 2020-01-22 14:02 EST
    Nmap scan report for 10.0.2.45
    Host is up (0.00051s latency).
 PORT   STATE SERVICE
    21/tcp open  ftp

** As you can see above, the port 21 is open.**
 2. Perform SYN flooding by typing:


```bash
    hping3 -d 100 -S -p 21 --flood <Windows 10 IP Address>
After you enter the command, switch to the Windows 10, observe that the machine is almost frozen, which means that the resources of Windows are completely exhausted. This means that the DoS attack is being successfully performed.

Switch back to the Kali Linux and press Ctrl+C to terminate SYN flooding.

![image](https://github.com/user-attachments/assets/02f9ea62-ad64-46d4-a0e0-96e9a133de7e)


**Detecting DoS Attack**

