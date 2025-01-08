# 🖥️ File Transfer Using Netcat

## 📝 Objectives
This project demonstrates how to transfer files between a Kali Linux VM and a Windows VM using Netcat. The goal is to establish a connection between the two machines and successfully transfer the sbd.exe file from Kali to Windows while monitoring the network traffic using Wireshark.

---

## 🛠️ Skills Learned
- Using Netcat for file transfer
- Setting up a listener on Windows
- Ensuring connectivity between VMs
- Capturing and analyzing network traffic with Wireshark

---

## 🧰 Tools Used
- **Kali Linux (Oracle VM)**
- **Windows VM (Oracle VM)**
- **Netcat**
- **Wireshark**

---

## 📋 Steps

### 1️⃣ Set Up the Virtual Machines
- Ensure both the **Kali** and **Windows VMs** are configured as follows:
  - **Adapter 1**: NAT
  - **Adapter 2**: Host-Only
- Disable all firewalls and antivirus software on both machines to avoid interference.

---

### 2️⃣ **Locate `sbd.exe` on Kali**
1. Open the terminal on your **Kali Linux** machine.
2. Navigate to the directory containing `sbd.exe`:
   ```bash
   cd /usr/share/windows-resources/sbd/
   ```
3. Run the following command to ensure the file is present:
   ```bash
   ls
   ```

---

### 3️⃣ **Ensure Connectivity Between VMs**
1. Use the **ping** command from both machines to verify they can communicate:
   - From **Kali**:
     ```bash
     ping <Windows_IP>
     ```
   - From **Windows**:
     ```
     ping <Kali_IP>
     ```

<img width="750" alt="image" src="https://github.com/user-attachments/assets/9374c626-e5bc-4fc5-a12d-61f771a748d6" />

✅ **If both machines can ping each other successfully, proceed to the next step.**

---

### 4️⃣ Start Wireshark on Kali
1. Open **Wireshark** on your **Kali Linux** machine.
2. Set the capture filter to monitor traffic between the two machines:
   ```
   host <Kali_IP> and host <Windows_IP>
   ```

---

### 5️⃣ Set Up a Listener on Windows
1. Open **Command Prompt** on your **Windows VM**.
2. Run the following command to set up **Netcat** to listen on port **4444** and prepare to receive the file:
   ```
   nc -l -p 4444 > sbd.exe
   ```
<img width="350" alt="image" src="https://github.com/user-attachments/assets/89dd8314-5c95-4908-a8cf-4afc7860d601" />

✅ **If nothing shows up, that means the listener is set up correctly.**

---

### 6️⃣ Send the File from Kali Using Netcat
1. Go back to your **Kali terminal**.
2. Navigate to the directory containing `sbd.exe`:
   ```bash
   cd /usr/share/windows-resources/sbd/
   ```
3. Run the following command to send the file to the **Windows VM**:
   ```bash
   nc <Windows_IP> 4444 < sbd.exe
   ```

✅ **The file transfer should complete successfully, and you will see `sbd.exe` on the Windows machine.**

---

### 7️⃣ **Verify the File Transfer**
1. On the **Windows VM**, check that the `sbd.exe` file was received in the directory where **Netcat** was listening.
2. Open **Wireshark** on the **Kali VM** to review the captured traffic and confirm that the file transfer occurred.

<img width="600" alt="image" src="https://github.com/user-attachments/assets/21265b15-2502-4cdf-ad68-a278c8361356" />

---

## 🎯 **Summary**
In this project, a file transfer was successfully conducted between **Kali Linux** and **Windows** using **Netcat**. The process involved setting up a listener on the **Windows VM**, sending the file from **Kali**, and monitoring the traffic with **Wireshark** to ensure the transfer was secure and complete.


