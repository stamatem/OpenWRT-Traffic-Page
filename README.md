## Traffic-Page Installation Guide

<br>

I have just made an app that is based on Traffic Push URL of **Bandix**.

It receives all the metrics from Bandix and displays them on an external page, accesible for all connected clients.

Additionally it has a Data Quota engine that blocks Internet access for users that reached the allocated quota.

<br>

### Install Bandix

Bandix Releases:
https://github.com/timsaya/openwrt-bandix/releases

Upload the .apk file through: LuCI –> System -> Software –> Upload Package

Connect SSH and run:
```bash
apk add --allow-untrusted /tmp/upload.apk
```
<br>

### Install LuCI App Bandix

LuCI App Bandix Releases:
https://github.com/timsaya/luci-app-bandix/releases

Upload the .apk file through: LuCI –> System -> Software –> Upload Package

Connect SSH and run:
```bash
apk add --allow-untrusted /tmp/upload.apk
```

<br>

### Install Traffic-Page

https://github.com/stamatem/Traffic-Page/releases

Upload the .apk file through: LuCI –> System -> Software –> Upload Package

Connect SSH and run:
```bash
apk add --allow-untrusted /tmp/upload.apk
```

No additional configuration is required for **Bandix** itself.

All necessary settings are automatically applied during the Traffic-Page installation.

<br>

**What Traffic-Page Creates Automatically**
- Guest Interface/Device: TRAFFIC_PAGE
- Wi-Fi networks: TRAFFIC_PAGE
- Firewall Zone: TRAFFIC_PAGE

You may change the Wi-Fi SSID name, password, and other wireless settings inside LuCI.

**Important:**

DO NOT rename the Guest Network Interface/Device or Firewall Zone.

Leave the Interface/Device name as: TRAFFIC_PAGE

Leave the Firewall Zone as: TRAFFIC_PAGE

<br>

### Initial Setup
1. Connect to the TRAFFIC_PAGE Wi-Fi network (or whatever SSID name you configured).
2. Open your browser and go to: http://10.99.100.1/data/ 
3. Click the **Admin** button.
4. Default admin password: **password**    (The password can be changed later.)
   
**Important Configuration Notes**
- Leave the DHCP Subnet unchanged (unless you know what are you doing)
- Leave the Firewall Zone unchanged

<br>

### Creating Your First User

Create your first user and add **your own MAC address** first.

Once the first user is created:
- Dynamic DHCP will be disabled
- Only registered MAC addresses will receive IP addresses

This prevents unregistered users to get an IP, even if they know the Wi-Fi password.

<br>

### Data Quotas
Assign the desired data quota for each user and press **Save**.

You may add:
- Multiple users
- Multiple MAC addresses under a single user

If a user has multiple registered MAC addresses, all traffic usage from those devices will be combined under the same quota.

<br>

### Multiplier Value
The Multiplier setting can be used to adjust traffic calculations so they match your ISP’s reported usage, if necessary.

<br>

### Reboot Required
After configuring users and MAC addresses, reboot your router so the fixed DHCP leases can take effect!

<br>

### Backend Functionality
The backend automatically creates firewall rules so that only registered MAC addresses can access the internet.

When a user reaches their assigned data quota:
- All registered MAC addresses for that user are blocked from internet access
- Existing active connections are terminated using conntrack

Fixed DHCP leases are also automatically created for every registered MAC address.

<br>

**Firewall Rules:**
- traffic_page (Allows users over quota to access the Traffic page)
- allow-dns-guest (Allows DNS traffic out from the guest zone)
- allow-dhcp-guest (Allows devices to use DHCP)
- traffic_allowed (Contains MAC addresses of users under quota)
- traffic_blocked (Contains MAC addresses of users over quota)
- traffic_unknown (Blocks unregistered MAC addresses)

<br> 

### Additional Automatic Configuration
- Sets the TRAFFIC_PAGE interface DNS to **8.8.8.8** (You may change this if desired)
- Creates a cron job for the Quota Engine run interval (The frequency can be modified from the Admin page  - **Quota Interval**)

<br>

### Admin User
The selected Admin User will never be blocked by the firewall, regardless of quota usage.

<br>

### PAID Switch
The PAID switch is used to mark users who have completed payment.

<br>

### Reset All Traffic Data
The Reset All Traffic Data button deletes all contents of:
/usr/share/bandix

Everything is designed to operate with minimal flash storage wear.

<br>

### Screenshots

<img width="670" height="525" alt="image" src="https://github.com/user-attachments/assets/528dd452-d3db-42d7-9b60-e28903ad51c1" />
<br>
<br>
<img width="781" height="600" alt="Screenshot_4" src="https://github.com/user-attachments/assets/22e10b2a-d475-4052-be0a-0c36cabab211" />
<br>
<br>
<img width="790" height="627" alt="Screenshot_3" src="https://github.com/user-attachments/assets/9be7339c-7bdf-46e6-80f9-a533e28e68e7" />

<br>

## Credits
All was possiblr due to timsaya’s **Bandix**:
https://github.com/timsaya/openwrt-bandix 
