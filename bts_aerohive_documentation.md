BTS Touring Aerohive Router Documentation
=========================================

This touring router is a repurposed _HiveAP_ 330 WiFi access point from Aerohive Networks, flashed with
custom firmware. This firmware allows the unit's (relatively powerful) internal hardware to act as a
fully-fledged router, firewall, and DHCP server (among other functions).

The custom firmware used on this device is _OpenWRT_ (see: https://openwrt.org/). This is a Linux-based
router firmware, intended as an open-source alternative to the stock firmware on a wide variety of
network appliances. OpenWRT can be configured either through a web interface (HTTP) or directly through 
its regular Linux command prompt (SSH/telnet/serial).

For BTS use-cases, this router is most useful when setting up small shared event networks on an ad-hoc
basis. For example, a network containing a video PC and some BirdDogs, connected together through an 
unmanaged switch.

This router's main functionality consists of three parts:

1. DHCP server: Provides IP addresses to its connected device(s);
   
2. Router: Since the unit has two Ethernet ports, it can receive an external internet connection on its
   _Eth0_ "WAN" (wide area network) interface and mediate access between this and local connected
   devices on the _Eth1_ "LAN" (local area network) interface. Crucially, the router only "appears" to
   the WAN as a single device, regardless of how many downstream LAN devices are connected;
   
3. Wireless access point: The Aerohive contains a WiFi antenna which is internally linked to the _Eth1_
   LAN port. This means that wireless access to the LAN is possible when the router is connected.

Basic setup:
------------

The device receives power either through PoE on its _Eth0_ (WAN) port (if available), or through a 
centre-positive 12V DC barrel jack. Note that PoE is not supported on the _Eth1_ port.

First, connect the (unmanaged) network switch containing the LAN devices to the _Eth1_ Aerohive port.

Next, connect the _Eth0_ port to an upstream internet connection. On campus, this will be to _Docking_ 
(essentially "Eduroam through a wire"). Note that some campus Docking ports provide PoE, mitigating the 
need for a local power adapter. If WAN-side PoE is unavailable, connect a 12V DC power supply.

If the connections are made correctly, the light on the corner of the device's case will illuminate and
become green/amber once it has finished booting. At this point, the LAN devices should begin to receive DHCP
IP addresses and internet connectivity. The LAN-resident WiFi network should also become visible.

WiFi network details:
---------------------

- SSID: `BTSROAM`
- Password: `[REDACTED]`

IP addressing details:
----------------------

- Router LAN subnet: `10.10.210.0/24`
- Router LAN IP address: `10.10.210.254`
- Router WAN IP address: [Determined by upstream DHCP]

Configuration access:
---------------------

Configuration access is only possible from the device's _LAN_ side. This is for security reasons, to prevent
anybody on the upstream (WAN) network gaining access.

- Web-based configuration: Enter the LAN IP address (10.10.210.254) into a web browser. Enter the root
  credentials when prompted.

- SSH configuration: Use a program such as _PuTTY_ (Windows) or _OpenSSH_ (Linux) to connect to the OpenWRT
  Linux terminal. Use the LAN IP adddress (10.10.210.254) and enter the root credentials when prompted.

- Serial configuration: Use this in the event that LAN network access is not possible. Connect a Cisco RJ45
  serial console cable directly to the "console" port on the underside of the device. The other end of the
  console cable should be connected to the RS232 port on a Real Computer (TM). Use a utility such as _Minicom_
  (Linux) or _Hyperterminal_ (Windows) to establish a serial connection from the PC at 9600 baud. Successful
  serial connection will result in direct access to the OpenWRT command prompt.
