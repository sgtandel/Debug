Ethernet Debugging
====

1. Interface Details
   
```
   # ifconfig 
eth0      Link encap:Ethernet  HWaddr 34:08:E1:84:AD:2F  
          UP BROADCAST MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
          
    # ifconfig  eth0 down
    # ifconfig  eth2 up
[  221.835051] remoteproc remoteproc8: powering up 300b4000.pru
[  221.842932] remoteproc remoteproc8: Booting fw image ti-pruss/am65x-sr2-pru0-prueth-fw.elf, size 38148
[  221.852306] remoteproc remoteproc8: unsupported resource 5
[  221.857828] remoteproc remoteproc8: remote processor 300b4000.pru is now up
[  221.864849] remoteproc remoteproc9: powering up 30084000.rtu
[  221.871883] remoteproc remoteproc9: Booting fw image ti-pruss/am65x-sr2-rtu0-prueth-fw.elf, size 30852
[  221.881271] remoteproc remoteproc9: remote processor 30084000.rtu is now up
[  221.888267] remoteproc remoteproc10: powering up 3008a000.txpru
[  221.895607] remoteproc remoteproc10: Booting fw image ti-pruss/am65x-sr2-txpru0-prueth-fw.elf, size 37208
[  221.905248] remoteproc remoteproc10: remote processor 3008a000.txpru is now up
[  221.913837] pps pps1: new PPS source ptp2
[  221.919468] net eth2: started

```

2. Ping
   
   Connect point to pont host with the device and run ping
```
# ping 192.168.1.10
PING 192.168.1.10 (192.168.1.10): 56 data bytes
^C
--- 192.168.1.10 ping statistics ---
3 packets transmitted, 0 packets received, 100% packet loss
```
3. Run ethtool to see configurations & statistics , while parallely running ping
```
# ethtool -i eth2
driver: icssg-prueth
version: 5.10.168
firmware-version: 
expansion-rom-version: 
bus-info: icssg1-eth
supports-statistics: yes
supports-test: no
supports-eeprom-access: no
supports-register-dump: no
supports-priv-flags: yes
# ethtool eth2
Settings for eth2:
        Supported ports: [ TP MII ]
        Supported link modes:   10baseT/Full 
                                100baseT/Full 
                                1000baseT/Full 
        Supported pause frame use: No
        Supports auto-negotiation: Yes
        Supported FEC modes: Not reported
        Advertised link modes:  10baseT/Full 
                                100baseT/Full 
                                1000baseT/Full 
        Advertised pause frame use: No
        Advertised auto-negotiation: Yes
        Advertised FEC modes: Not reported
        Link partner advertised link modes:  10baseT/Half 10baseT/Full 
                                             100baseT/Half 100baseT/Full 
                                             1000baseT/Full 
        Link partner advertised pause frame use: Symmetric Receive-only
        Link partner advertised auto-negotiation: Yes
        Link partner advertised FEC modes: Not reported
        Speed: 1000Mb/s
        Duplex: Full
        Port: Twisted Pair
        PHYAD: 2
        Transceiver: external
        Auto-negotiation: on
        MDI-X: Unknown
        Current message level: 0x00007fff (32767)
                               drv probe link timer ifdown ifup rx_err tx_err tx_queued intr tx_done rx_status pktdata hw wol
        Link detected: yes
# ethtool -T eth2
Time stamping parameters for eth2:
Capabilities:
        hardware-transmit     (SOF_TIMESTAMPING_TX_HARDWARE)
        software-transmit     (SOF_TIMESTAMPING_TX_SOFTWARE)
        hardware-receive      (SOF_TIMESTAMPING_RX_HARDWARE)
        software-receive      (SOF_TIMESTAMPING_RX_SOFTWARE)
        software-system-clock (SOF_TIMESTAMPING_SOFTWARE)
        hardware-raw-clock    (SOF_TIMESTAMPING_RAW_HARDWARE)
PTP Hardware Clock: 2
Hardware Transmit Timestamp Modes:
        off                   (HWTSTAMP_TX_OFF)
        on                    (HWTSTAMP_TX_ON)
Hardware Receive Filter Modes:
        none                  (HWTSTAMP_FILTER_NONE)
        all                   (HWTSTAMP_FILTER_ALL)

# ethtool -P eth2
Permanent address: 00:00:00:00:00:00

# ethtool -l eth2
Channel parameters for eth2:
Pre-set maximums:
RX:             1
TX:             4
Other:          0
Combined:       0
Current hardware settings:
RX:             1
TX:             1
Other:          0
Combined:       0

# ethtool -S eth2
NIC statistics:
     rx_good_frames: 0
     rx_broadcast_frames: 0
     rx_multicast_frames: 0
     rx_crc_error_frames: 1
     rx_mii_error_frames: 0
     rx_odd_nibble_frames: 0
     rx_frame_max_size: 32000
     rx_max_size_error_frames: 0
     rx_frame_min_size: 1024
     rx_min_size_error_frames: 1
     rx_overrun_frames: 1
     rx_class0_hits: 1
     rx_class1_hits: 0
     rx_class2_hits: 0
     rx_class3_hits: 0
     rx_class4_hits: 0
     rx_class5_hits: 0
     rx_class6_hits: 0
     rx_class7_hits: 0
     rx_class8_hits: 1
     rx_class9_hits: 1
     rx_class10_hits: 0
     rx_class11_hits: 0
     rx_class12_hits: 0
     rx_class13_hits: 0
     rx_class14_hits: 0
     rx_class15_hits: 0
     rx_smd_frags: 0
     rx_bucket1_size: 1024
     rx_bucket2_size: 2048
     rx_bucket3_size: 4096
     rx_bucket4_size: 8192
     rx_64B_frames: 0
     rx_bucket1_frames: 1
     rx_bucket2_frames: 0
     rx_bucket3_frames: 0
     rx_bucket4_frames: 0
     rx_bucket5_frames: 0
     rx_total_bytes: 0
     rx_tx_total_bytes: 1881
     tx_good_frames: 15
     tx_broadcast_frames: 3
     tx_multicast_frames: 15
     tx_odd_nibble_frames: 0
     tx_underflow_errors: 0
     tx_frame_max_size: 32000
     tx_max_size_error_frames: 0
     tx_frame_min_size: 1024
     tx_min_size_error_frames: 0
     tx_bucket1_size: 1024
     tx_bucket2_size: 2048
     tx_bucket3_size: 4096
     tx_bucket4_size: 8192
     tx_64B_frames: 0
     tx_bucket1_frames: 0
     tx_bucket2_frames: 15
     tx_bucket3_frames: 0
     tx_bucket4_frames: 0
     tx_bucket5_frames: 0
     tx_total_bytes: 1296



```
4. Disable ipv6 , if you're testing ipv4
```
echo 1 > /proc/sys/net/ipv6/conf/eth2/disable_ipv6
ip addr add 192.168.1.35/24 dev eth2
ip link set dev eth2 up

```
5. Run phytool (Phy chip is TI's DP83867)
   * Check for Rxt error count
    ```
    phytool read eth2/0x02/0x0015
    ```
    * Strap register
      ```
      phytool read eth2/0x02/0x006E
      phytool read eth2/0x02/0x006F
      ```
    * MII Loopback with 1 GBPS auto neg:
    ```
    phytool write eth2/0x02/0X0000 0x5140
    phytool read eth2/0x02/0X0000
    ```
    * MII Loopback with 100MBPS:
    ```
    phtytool write eth2/0x02/0x0000 0x6100
    ```
    
    * Reset:
     ```
     phytool write eth2/0x02/0x0000 0x8000 
     phytool write eth2/0x02/0x001F 0x8000
   
     ```
     * Delay Control register. RGMII Delay Control Register (RGMIIDCTL)
       tx delay = 1.75ns 
       rx delay = 3.5 ns
       ```
       phytool read eth2/0x02/0x0086
       phytool read eth2/0x02/0x0086
       0x006D
       ```
6. Verify DTS file for ethernet & phy node
7. Verify pinmuxing 
