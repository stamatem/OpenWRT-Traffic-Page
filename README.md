## Bandix + Traffic-Page Installation Guide


### Install Bandix

Bandix Releases:
https://github.com/timsaya/openwrt-bandix/releases/tag/v0.12.9 

Upload the .apk file through LuCI – System - Software – Upload Package

Connect SSH and run:      apk add --allow-untrusted /tmp/upload.apk


### Install LuCI App Bandix

LuCI App Bandix Releases:
https://github.com/timsaya/luci-app-bandix/releases/tag/v0.12.8 

Upload the .apk file through LuCI – System - Software – Upload Package

Connect SSH and run:      apk add --allow-untrusted /tmp/upload.apk


### Install Traffic-Page

https://github.com/stamatem/Traffic-Page/releases

Upload the .apk file through LuCI – System - Software – Upload Package

Connect SSH and run:      apk add --allow-untrusted /tmp/upload.apk

No additional configuration is required for Bandix itself.

All necessary settings are automatically applied during the Traffic-Page installation.

**What Traffic-Page Creates Automatically**
- Guest Interface/Device: TRAFFIC_PAGE
- Wi-Fi networks: TRAFFIC_PAGE
- Firewall Zone: TRAFFIC_PAGE

You may change the Wi-Fi SSID name, password, and other wireless settings inside LuCI.

**Important:**

DO NOT rename the Guest Network interface/device inside Interfaces or Devices.
Leave the interface name as: TRAFFIC_PAGE

### Initial Setup
1. Connect to the TRAFFIC_PAGE Wi-Fi network (or whatever SSID name you configured).
2. Open your browser and go to: http://10.99.100.1/data/ 
3. Click the Admin button.
4. Default admin password: password    (The password can be changed later.)
   
**Important Configuration Notes**
- Leave the DHCP Subnet unchanged
- Leave the Firewall Zone unchanged
  
### Creating Your First User

Create your first user and add **your own MAC address** first.

Once the first user is created:
- Dynamic DHCP will be disabled
- Only registered MAC addresses will receive IP addresses

This prevents unregistered users from accessing the network, even if they know the Wi-Fi password.

### Data Quotas
Assign the desired data quota for each user and press Save.

You may add:
- Multiple users
- Multiple MAC addresses under a single user

If a user has multiple registered MAC addresses, all traffic usage from those devices will be combined under the same quota.

### Multiplier Value
The Multiplier setting can be used to adjust traffic calculations so they match your ISP’s reported usage, if necessary.

### Reboot Required
After configuring users and MAC addresses, reboot your router so the fixed DHCP leases can take effect!

### Backend Functionality
The backend automatically creates firewall rules so that only registered MAC addresses can access the internet.

When a user reaches their assigned data quota:
- All registered MAC addresses for that user are blocked from internet access
- Existing active connections are terminated using conntrack

Fixed DHCP leases are also automatically created for every registered MAC address.

**Firewall Rules:**
- traffic_page (Allows users over quota to access the Traffic page)
- allow-dns-guest (Allows DNS traffic out from the guest zone)
- allow-dhcp-guest (Allows devices to use DHCP)
- traffic_allowed (Contains MAC addresses of users under quota)
- traffic_blocked (Contains MAC addresses of users over quota)
- traffic_unknown (Blocks unregistered MAC addresses)
  
### Additional Automatic Configuration
- Sets the TRAFFIC_PAGE interface DNS to 8.8.8.8 (You may change this if desired)
- Creates a cron job for the Quota Engine run interval (The frequency can be modified from the Admin page  - Quota Interval)
  
### Admin User
The selected Admin User will never be blocked by the firewall, regardless of quota usage.

### PAID Switch
The PAID switch is used to mark users who have completed payment.

### Reset All Traffic Data
The Reset All Traffic Data button deletes all contents of:
/usr/share/bandix

Everything is designed to operate with minimal flash storage wear.

### Screenshots

<img width="670" height="525" alt="image" src="https://github.com/user-attachments/assets/528dd452-d3db-42d7-9b60-e28903ad51c1" />
<br>
<br>
<img width="799" height="592" alt="image" src="https://github.com/user-attachments/assets/a19451d9-6033-4bba-953d-53de9c2eb0f9" />
<br>
<br>
<img width="772" height="485" alt="image" src="https://github.com/user-attachments/assets/a521004a-4aae-4c3b-8fca-f79b431540be" />






## Credits
All credits go to timsaya’s **Bandix**:
https://github.com/timsaya/openwrt-bandix 
