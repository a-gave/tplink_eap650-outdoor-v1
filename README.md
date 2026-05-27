# Notes on tplink_eap650-outdoor-v1
Tested on 2 devices
- device1 - B2:xx:xx:xx:60:13
- device2 - B2:xx:xx:xx:61:13


## Resources
- GPL code: 
    - https://support.omadanetworks.com/us/product/eap650-outdoor/v1/?resourceType=download
    - https://static.tp-link.com/upload/gpl-code/2023/202305/20230516/ipq518_eap650_outdoor_v1.tar.gz


## Issues 
- 802.1ad interfaces created on top of the wireless mesh interface don't work
- Ethernet radomly fails


### 802.1ad over 80211s
**logs at firstboot with wifi not enabled**

Compiled with `CONFIG_PACKAGE_ATH_DEBUG=y`
```
echo 0xffffffff > /sys/module/ath11k/parameters/debug_mask
```
With a backported patch that seems related: [wifi: ath11k: fix peer resolution on rx path when peer_id=0](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/drivers/net/wireless/ath/ath11k?id=2a2451a34afdf563b3102d36a4b6cf335cf813e2)

```
logread -f
Thu Jan  1 00:01:53 1970 kern.debug kernel: [  113.416585] ath11k c000000.wifi: ce rx ce pipe 2 len 112
Thu Jan  1 00:01:53 1970 kern.debug kernel: [  113.416640] ath11k c000000.wifi: htc rx ep 2 skb 0000000091513778 trailer_present 0
Thu Jan  1 00:01:53 1970 kern.debug kernel: [  113.416672] ath11k c000000.wifi: wmi event diag
Thu Jan  1 00:01:53 1970 kern.debug kernel: [  113.516625] ath11k c000000.wifi: ce rx ce pipe 2 len 112
```
**full logs in**
- openwrt/ath11k_debug_ap
- openwrt/ath11k_debug-ap-mesh

The serial connection become unresponsive and had to `killall -9 logread`


**logs with wifi enabled**
```
root@eap:~# iwinfo wlan1-mesh assoclist
<redacted>  -58 dBm / -109 dBm (SNR 51)  10 ms ago
	RX: unknown                                      768 Pkts.
	TX: 162.0 MBit/s, MCS 12, 40MHz                    9 Pkts.
	expected throughput: 144.9 MBit/s

<redacted>  -50 dBm / -109 dBm (SNR 59)  0 ms ago
	RX: unknown                                      752 Pkts.
	TX: 309.7 MBit/s, HE-MCS 6, 40MHz, HE-NSS 2, HE-GI 0, HE-DCM 0         5 Pkts.
	expected throughput: 270.0 MBit/s

root@eap:~# iwinfo wlan1-mesh info
wlan1-mesh ESSID: "LiMe"
          Access Point: B2:19:21:AB:61:13
          Mode: Mesh Point  Channel: 36 (5.180 GHz)  HT Mode: HT40
          Center Channel 1: 38 2: unknown
          Tx-Power: 30 dBm  Link Quality: 55/70
          Signal: -55 dBm  Noise: -109 dBm
          Bit Rate: 235.8 MBit/s
          Encryption: WPA3 SAE (CCMP)
          Type: nl80211  HW Mode(s): 802.11ac/ax/n
          Hardware: 17CB:1104 17CB:1104 [Qualcomm Atheros QCN6024/9024/9074]
          TX power offset: none
          Frequency offset: none
          Supports VAPs: yes  PHY name: phy1
```


### Ethernet randomly fails
Observed on device2, here succed in attaching PHY driver:
```
[    3.773029] ssdk_dt_parse_mac_mode[300]:INFO:mac mode1 doesn't exit!
[    3.773080] ssdk_dt_parse_mac_mode[308]:INFO:mac mode2 doesn't exit!
[    3.778648] ssdk_dt_parse_port_bmp[1064]:INFO:port_bmp doesn't exist!
[    3.784813] ssdk_dt_parse_interrupt[942]:INFO:intr-gpio does not exist
[    5.295776] ssdk_mp_reset_init[1311]:INFO:MP reset successfully!
[    5.296819] ssdk_phy_driver_init[341]:INFO:dev_id = 0, phy_adress = 260, phy_id = 0xfffafffa phytype doesn't match
[    5.629824] regi_init[2548]:INFO:Initializing SCOMPHY Done!!
[    5.630015] regi_init[2574]:INFO:qca-ssdk module init succeeded!
[    5.638439] nss-dp 39d00000.dp2 lan (uninitialized): nss_dp_gmac: Registering netdev lan(qcom-id:2) with GMAC, mac_base: 0xffffffc081630000
[    5.642330] Generic PHY 90000.mdio-1:04: attached PHY driver (mii_bus:phy_addr=90000.mdio-1:04, irq=POLL)
```


## Warnings

This error randomly appears in device2 and never in device1
```
[   13.090830] pcieport 0000:00:00.0: AER: Multiple Correctable error message received from 0000:00:00.0
[   13.090932] pcieport 0000:00:00.0: PCIe Bus Error: severity=Correctable, type=Physical Layer, (Receiver ID)
[   13.099177] pcieport 0000:00:00.0:   device [17cb:1004] error status/mask=00000041/0000e000
[   13.108675] pcieport 0000:00:00.0:    [ 0] RxErr                 
[   13.116935] pcieport 0000:00:00.0:    [ 6] BadTLP                
[   13.123324] ath11k_pci 0000:01:00.0: PCIe Bus Error: severity=Correctable, type=Physical Layer, (Receiver ID)
[   13.129345] ath11k_pci 0000:01:00.0:   device [17cb:1104] error status/mask=00000001/0000e000
[   13.139196] ath11k_pci 0000:01:00.0:    [ 0] RxErr 
```