# MITE - Mobile Internet to Ethernet
How to share mobile internet (wifi hotspost) to wired ethernet (LAN) devices with dd-wrt
this assumes you have a router flashed with dd-wrt and repeater bridge option available

# Hardware used in this tutorial
Linksys WRT54G/GL/GS | Samsung Galaxy S6 
----|-------
(Broadcom BCM5352 chip rev 0) flashed with dd-wrt firmware v24-sp2 (07/22-09) micro - build 12548M NEWD Eko
(useful pages @ https://wiki.dd-wrt.com/wiki/index.php/Linksys_WRT54G/GL/GS/GX) | Any wifi router could also be used instead or any other phone with hotspot function
![WRT54G](https://user-images.githubusercontent.com/67799618/91707965-8351cb00-eb78-11ea-9bcf-6762f3a32230.png) | ![Samsung_Galaxy_S6_Scaled](https://user-images.githubusercontent.com/67799618/91667284-4dbacc80-eafb-11ea-92c1-f597a17c8265.png)

# Router status page
detail of softweare flashed and router spec

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
    - **Wireless mode:** Repeater Bridge
    - **Wireless Network Mode:** Mixed or choose G-Only
    - **Wireless Network Name (SSID):** WIFI_1 (same as phone hotspot)
    - **Sensitivity Range (ACK Timing):** 2000 (default) unless you know what your doing
    - **Network Configuration:** Bridged
    - **Click add a virtual Interface**
    - **Wireless Netwrok Name (SSID):** WIFI_2 (or any other name)
    - **Wireless SSID Broadcast:** Enable (or Disable if you want to hide the network)
    - **AP Isolation:** Disbale
    - **Network Configuration:** Bridged
    
    ![image](https://user-images.githubusercontent.com/67799618/91712835-7e911500-eb80-11ea-8aad-554c59e26ac6.png)
  
