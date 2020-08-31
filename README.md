# MITE - Mobile Internet to Ethernet
How to share mobile internet (wifi hotspost) to wired ethernet (LAN) devices with dd-wrt

# Hardware used in this tutorial
Linksys WRT54G/GL/GS | Samsung Galaxy S6 
----|-------
(Broadcom BCM5352 chip rev 0) flashed with dd-wrt firmware v24-sp2 (07/22-09) micro - build 12548M NEWD Eko
(useful pages @ https://wiki.dd-wrt.com/wiki/index.php/Linksys_WRT54G/GL/GS/GX) | Any wifi router should do
![WRT54G](https://user-images.githubusercontent.com/67799618/91707965-8351cb00-eb78-11ea-9bcf-6762f3a32230.png) | ![Samsung_Galaxy_S6_Scaled](https://user-images.githubusercontent.com/67799618/91667284-4dbacc80-eafb-11ea-92c1-f597a17c8265.png)

# Router front page
detail of softweare flashed and router spec

![image](https://user-images.githubusercontent.com/67799618/91665740-c87dea80-eaef-11ea-96f2-606682c35c73.png)

# Step by Step
1. Configure android phone hotspot 
  - Network Name : e.g. WIFI 1
  - Password: choose your own wifi password
  - Hide my device: unselected (optional, select if you want to hide SSID)
  - Security: WPA2 PSK
  - Wifi Sharing: On
  - Timeout Setting: Never Timeout (optional)
  - Band: 2.4Ghz
  - Turn Mobile HotSpot On
  
 2. Configuer WRT54G
  
