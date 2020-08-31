# MITE - Mobile Internet to Ethernet
How to share mobile internet (wifi hotspost) to wired ethernet (LAN) devices with dd-wrt
this assumes you have a router flashed with dd-wrt and repeater bridge option available

# Hardware used in this tutorial
Linksys WRT54G/GL/GS | Samsung Galaxy S6 
----|-------
(Broadcom BCM5352 chip rev 0) flashed with dd-wrt firmware v24-sp2 (07/22-09) micro - build 12548M NEWD Eko
(useful pages @ https://wiki.dd-wrt.com/wiki/index.php/Linksys_WRT54G/GL/GS/GX) | Any wifi modem router could also be used instead or any other phone with hotspot function
![WRT54G](https://user-images.githubusercontent.com/67799618/91707965-8351cb00-eb78-11ea-9bcf-6762f3a32230.png) | ![Samsung_Galaxy_S6_Scaled](https://user-images.githubusercontent.com/67799618/91667284-4dbacc80-eafb-11ea-92c1-f597a17c8265.png)

# Router status page
 - Detail of softweare flashed and router spec

![image](https://user-images.githubusercontent.com/67799618/91665740-c87dea80-eaef-11ea-96f2-606682c35c73.png)

# Step by Step
Note: Click 'Save' everytime you change a settings, once all settings have been modified select 'Apply Settings' and wait forr router to reboot.

## 1. Configure android phone hotspot 
  - Network Name : e.g. WIFI_1
  - Password: choose your own wifi password
  - Hide my device: unselected (optional, select if you want to hide SSID)
  - Security: WPA2 PSK
  - Wifi Sharing: On
  - Timeout Setting: Never Timeout (optional)
  - Band: 2.4Ghz
  - Turn Mobile HotSpot On
  - Connect a device to check ip address range and subnet mask
  (in this case address range is 192.168.43.x subnet 255.255.255.0)
  hotspot ip address is 192.168.43.1
  
## 2. Configure WRT54G (Setup Page)
  - reset router by pressing the hardware switch
  
  ![image](https://user-images.githubusercontent.com/67799618/91711337-a8950800-eb7d-11ea-9bd9-6d3493751369.png)
  - connect to open wifi dd-wrt or use an ethernet cable instead
  - open browser and type 192.168.1.1
  - you should be greeted with a page inviting to set admininistrator user and password.
  - once set go to Setup -> basic setup
    - disable STP
    - choose rooter name (optional)
    - set local IP address of router to 192.168.43.2
    - subnet mask = 255.255.255.0
    - Gateway adress: 192.168.43.1
    - Local DNS: 192.168.43.1
    - Assign WAN Port to Switch: (Optional) select if you want to make an extra ethernet port available for an additional device
    - NTP Client: disbale (optional)
    ![image](https://user-images.githubusercontent.com/67799618/91711631-17726100-eb7e-11ea-900e-5d6594bd6df0.png)
     
   - Setup -> DDNS (disable)
   - Setup -> Mac Address Clone (disable)
   - Setup -> Advanced Routing
      - Operating Mode: Select Router
      - Dynamic Routing: Disbale
      - Static Routing: leave default settings
    ![image](https://user-images.githubusercontent.com/67799618/91712110-02e29880-eb7f-11ea-9f57-ecb00fc2936f.png)
  
   - Setup -> VLAN
   
   ![image](https://user-images.githubusercontent.com/67799618/91712664-1fcb9b80-eb80-11ea-98b1-0368ccc45d53.png)
   
   - Setup -> Networking
   
   ![image](https://user-images.githubusercontent.com/67799618/91712716-3b36a680-eb80-11ea-874d-c1ac96c34102.png)

## 3. Configure WRT54G (Wireless Page)
  - Wireless-> Basic Settings
    - Wireless mode: Repeater Bridge
    - Wireless Network Mode: Mixed or choose G-Only
    - Wireless Network Name (SSID): WIFI_1 (same as phone hotspot)
    - Sensitivity Range (ACK Timing): 2000 (default) unless you know what your doing
    - Network Configuration: Bridged
    - Click add a virtual Interface
    - Wireless Netwrok Name (SSID): WIFI_2 (or any other name)
    - Wireless SSID Broadcast: Enable (or Disable if you want to hide the network)
    - AP Isolation: Disable
    - Network Configuration: Bridged
    
   ![image](https://user-images.githubusercontent.com/67799618/91714337-6a9ae280-eb83-11ea-9621-9bba039719c2.png)
  
  - Wireless -> Radius (skip this, only configurable in AP isolation mode anyway)
  - Wireless -> Wireless Security
  
      --Physical Interface-- Encryption has to match mobile hotspot encryption (these are settings that worked for me)
      - Security Mode: WPA2 Personal
      - WPA algorithms: AES
      - WPA Shared Key: Same as Mobile HotSpot
      - Key Renewal Interval (in seconds): 3600 (default)
      
      --Virtual Interfaces-- Encryption has to match mobile hotspot encryption (these are settings that worked for me)
      - Security Mode: WPA2 Personal
      - WPA algorithms: AES
      - WPA Shared Key: Same as Mobile HotSpot
      - Key Renewal Interval (in seconds): 3600 (default)
      
      ![image](https://user-images.githubusercontent.com/67799618/91714546-ea28b180-eb83-11ea-8e78-0d8a09f7864f.png)
      
   - Wireless -> Mac Filter 
    (optional - specify MAC address of devices allowed on the network if you want to restrict access to certain devices only
    this option is also available on the mobile hotspot).
    
   ![image](https://user-images.githubusercontent.com/67799618/91715033-d6317f80-eb84-11ea-8c37-8dac6b0730dd.png)
    
   - Wireless -> Advanced Settings (leave everything to default)
     - Wireless GUI Access: Enable (if Disable is selected you will not be able to access this configuration interface via Wifi anymore).
    
   ![image](https://user-images.githubusercontent.com/67799618/91715371-67085b00-eb85-11ea-9beb-46df46eb4a6d.png)
    
   - Wireless -> WDS (skip, leave default settigns)
    
   ![image](https://user-images.githubusercontent.com/67799618/91715514-b058aa80-eb85-11ea-9067-9c3bc162bb2b.png)
   
 ## 4. Configure WRT54G (Services Page)
  - Services -> Services (leave default settings except DNSMasq)
    - DNSMasq: Disable
    - Telnet: Enable --default-- (set to Disable if you do not want to allow configuration via telnet)
   
   ![image](https://user-images.githubusercontent.com/67799618/91716271-39241600-eb87-11ea-862e-e5b00249e81f.png)
   
   - Services -> Hostpot (leave default settings)
   
   ![image](https://user-images.githubusercontent.com/67799618/91716323-578a1180-eb87-11ea-83ce-8794ada5a670.png)
   
   - Services -> My Ad Network (skip - leave default settings)
   
   ![image](https://user-images.githubusercontent.com/67799618/91716398-7a1c2a80-eb87-11ea-9f41-6e24c15db3b3.png)
   
  - Security -> Firewall
    - SPI Firewall: Disable
    - Additional Filter: uncheck all
    - Block Wan Requests: check only Filter Multicast
    
    ![image](https://user-images.githubusercontent.com/67799618/91716696-0af30600-eb88-11ea-8a64-2b86e9c3ba52.png)
    
    - Security -> VPN Passthrough (skip, leave default settings)
    
    ![image](https://user-images.githubusercontent.com/67799618/91716809-3c6bd180-eb88-11ea-938a-1e857b50f83f.png)
  
 ## 5. Configure WRT54G (Access Restrictions Pages) 
  - Access Restrictions -> WAN Access (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91716938-763cd800-eb88-11ea-8ff6-ee0fc8da4273.png)
  
## 6. Configure WRT54G (NAT / QoS Pages) (skip, leave default settings)
  - Access Restrictions -> Port Forwarding (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91717288-21e62800-eb89-11ea-800f-74d17cbceeed.png)

  - Access Restrictions -> Port Range Forwarding (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91717330-35918e80-eb89-11ea-8c82-8410f6172b8b.png)

  - Access Restrictions -> Port Triggering (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91717356-480bc800-eb89-11ea-8ec1-18a4b1c87825.png)

  - Access Restrictions -> UPnP (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91717396-5823a780-eb89-11ea-8ed8-5be904b38f1d.png)

  - Access Restrictions -> DMZ (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91717433-6a054a80-eb89-11ea-850d-df1a2bc29d4f.png)
  
  - Access Restrictions -> Quality of Service (QoS) (skip, leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91717466-7ab5c080-eb89-11ea-9031-3dcadef3ca2e.png)

## 7. Configure WRT54G (Administration Pages)
  - Administration -> Management
    - Router Username: set router username if not already configured
    - Router password: set if not already configured
    - leave rest to default (no changes required unless specfic need)
    
  ![image](https://user-images.githubusercontent.com/67799618/91718036-88b81100-eb8a-11ea-9520-0ca8f3e1f161.png)
 
  - Adminstration -> Keep Alive (skip leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91718099-a2595880-eb8a-11ea-87b4-541a94d8c6cf.png)

  - Administration -> Commands (skip leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91718168-c9b02580-eb8a-11ea-87cd-6d030efb1f03.png)

  - Administration -> WOL (skip leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91718228-e2204000-eb8a-11ea-8a1b-e9df7890d1ba.png)
  
  - Administration -> Factory Defaults (skip leave default settings)
  
  ![image](https://user-images.githubusercontent.com/67799618/91718277-f3694c80-eb8a-11ea-8690-30d3f8199a3f.png)

  - Administration -> Firmware Upgrade (skip leave default settings)
 
 ![image](https://user-images.githubusercontent.com/67799618/91718389-290e3580-eb8b-11ea-95a6-f70ced21f867.png)

  - Administration -> Backup
  
 here is the final screen, this is opportunity to backup all these settings to a file should you ever have to reset the router in the future you wil be able to retrieve yor settings.
 
 ![image](https://user-images.githubusercontent.com/67799618/91718594-93bf7100-eb8b-11ea-9f29-92c31fa3b058.png)
 
 Connect your wired devices to the router ethernet port, they should get automatice IP addresses via DHCP from the phone (make sure the device set to receive IP address via DHCP, you can also assign an IP address as long as it is in the same address range e.g. 192.168.43.x (x = 3 to 254) in this scenario.
 You should then be able to access the ethernet on these devices useing the mobile phone internet connection.
 You can also connect wifi devices using either WIFI_1 or WIFI_2 network, you can therfore place the wifi router in an other location  than the phone in orther to extend coverage of the wifi network.
 
You can turn off the phone mobile hotspot at anytime, the router will keep functioning you will simply no longer have access to the internet with these devices.
