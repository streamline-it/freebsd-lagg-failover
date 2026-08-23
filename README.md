Role Name
=========

freebsd-lagg-failover

This role is primarily created to deal with laptop networking failover.  It's designed to use ethernet for the primary and WiFi for the secondary failover.

Requirements
------------

None.

Role Variables
--------------

# Usually this will be the WiFi MAC to not confuse
# the router due to the failover to a different MAC address
# this avoids this by spoofing the WiFi's MAC to the ethernet
freebsd_lagg_failover_spoofed_mac_address:

# Set the protocol for the secondary device
freebsd_lagg_failover_wifi_protocol: WPA

# lagg device name, usually lagg0
freebsd_lagg_failover_lagg_device: lagg0

# for secondary device to use
# Ex for Wifi 
# freebsd_lagg_failover_wifi_device: "ath0"
# This will allow setup for the following line that will exist in the LineInFile module
# wlans_{{ freebsd_lag_failover_wifi_device }}={{ freebsd_lagg_failover_secondary_port }}
# This will result in the following line in the config
# wlans_ath0="wlan0"
freebsd_lagg_failover_wifi_device:

# primary port for lagg to use
freebsd_lagg_failover_primary_port:

# failover secondary port 
freebsd_lagg_failover_secondary_port:

# if true use IPv4
freebsd_lagg_failover_use_ipv4: true

# ipv4 address to use for the lagg device
freebsd_lagg_failover_ipv4_address:

# ipv4 netmask      
# make sure to inlude the word "netmask" before the netmask value
freebsd_lagg_failover_ipv4_netmask:

# if true use IPv6
freebsd_lagg_failover_use_ipv6: true

# ipv6 address to use for the lagg device
freebsd_lagg_failover_ipv6 address:

# ipv6 netmask
# make sure to inlude the word "netmask" before the netmask value
freebsd_lagg_failover_ipv6netmask:

# any network related options not provided for here can go into this variable
freebsd_lagg_failover_network_options:

# vars file

# filepath to the config file
freebsd_lagg_failover_config_filepath: /etc/rc.conf
freebsd_lagg_failover_loader_config_filepath: /boot/loader.conf

Dependencies
------------

None

Example Playbook
----------------

- name: lagg failover
  host: node1.example.com

  vars: 
    # the following variable should be secured in an ansible vault file
    my_wifi_ssid_passhphrase: "password"
    freebsd_lagg_failover_spoofed_mac_address: f0:33:62:92:b3:b7
    freebsd_lagg_failover_wifi_device: rtwn0
    freebsd_lagg_failover_primary_port: em0
    freebsd_lagg_failover_secondary_port: wlan0
    freebsd_lagg_failover_network_options: "SYNCDHCP group main_int"
    freebsd_lagg_failover_wifi_ssid:
      - mywifissid
    freebsd_lagg_failover_wifi_ssid_passphrase: "{{ my_wifi_ssid_passphrase }}"
    freebsd_lagg_failover_wifi_firmware_module: if_rtwn_usb
    freebsd_lagg_failover_wifi_driver_module: rtwn-rtl8821aufw

  roles:

    name: freebsd-lagg-failover
   

License
-------

BSD

Author Information
------------------

Rich O'Hara


