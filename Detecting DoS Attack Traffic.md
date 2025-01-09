![image](https://github.com/user-attachments/assets/56b46cb2-02a5-44f7-a7f3-459dfa1089aa)


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

3. Click on **Settings** on the top menu and Set Up Wizard:
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

As you can see above, the port 21 is open.

Let's use this port to flood the target:


2. Perform SYN flooding by typing:
   ```bash
   hping3 -d 100 -S -p 21 --flood <Windows 10 IP Address>

After you enter the command, switch to the Windows 10, observe that the machine is almost frozen, which means that the resources of Windows are completely exhausted. This means that the DoS attack is being successfully performed.

Switch back to the Kali Linux and press Ctrl+C to terminate SYN flooding.

![image](https://github.com/user-attachments/assets/62aa0783-8096-47ee-b7de-989b4d928ccb)


   
## Detecting DoS Attack

Switch to the **Windows** 10, you should now be able to access it.

Now the FTP icon in the left pane changes to red, and the FTP section in the right pane is flooded with events.

![image](https://github.com/user-attachments/assets/51910167-dc87-4f13-bd26-80c272f7456b)

Scroll down and try to find an event named DOS Attack

![image](https://github.com/user-attachments/assets/74d21933-623a-42e5-aeb3-23b65a99c9f9)


This concludes that KFSensor has detected the DoS attack.

Choose another random event and double click it to show the event details.

On the Event window, which contains the event summary, you can see the severity level of the event (High), the description of the event (Syn Scan), 
the visitor of the event (Attacker machine's IP address), sensor name (FTP), and so on as you can see below.


![image](https://github.com/user-attachments/assets/5717fa5f-59ad-44fb-aa9d-2545da93dc4d)

## Analyze Packet Dump on Wireshark

Next, analyze the packet dump file containing the traffic captured during the DoS attack. KFSensor stores the packet dump file on **C:\kfsensor\dumps** by default.

Open the Wireshark and click **File > Open** and open the packet dump stored in **C:\kfsensor\dumps**

![image](https://github.com/user-attachments/assets/ebd9fc1a-8980-478f-bb04-b5e5df8cb33b)

Wireshark loads the file and displays the packet's details, as show above.

You can analyze the packets to get information related to headers of the packets, source IP addresses, and so on.
