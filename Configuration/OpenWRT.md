# OpenWRT

## Create Virtual Machines on Hyper-V

1. `Virtual Switch Manager` >> New `virtual network switch` >> `External` >> Create `virtual switch` >> `External Switch` >> Select Ethernet network
2. New >> `Virtual Machine`
  1. `Specify Name and Location`
    1. Enter `Name`
    2. Tick `Store the virtual machine in a different location` >> Change `Location`
  2. `Specify Generation` >> Select `Generation 2`
  3. `Configure Networking` >> Select `External Switch`
  4. `Connect Virtual Hard Disk` >> `Use an existing virtual hard disk` >> Select vhdx
3. Select Virtual Machine >> `Settings`
  1. `Security` >> Untick `Enable Secure Boot`
  2. `Processor` >> Change number of processors

## OpenWRT Installation

1. Download `https://downloads.openwrt.org/releases//targets/x86/64/openwrt--x86-64-generic-ext4-combined-efi.img.gz`
2. Open `StarWind V2V Converter` and Convert `openwrt--x86-64-generic-ext4-combined-efi.img` to `VHDX growable image`
3. Copy the vhdx file to another location for storing
3. Create Virtual Machine
4. In OpenWRT

```bash
vi /etc/config/network
```

Type `i` to Edit

```
config interface 'lan'
    option device 'br-lan'
    option proto 'static'
    option ipaddr '<IPAddress>'
    option netmask '255.255.255.0'
    option ip6assign '60'
```

Type `Esc` then `:wq` to save and quit

```bash
/etc/init.d/network reload
```

5. Visit `<IPAddress>` to goto OpenWRT Dashboard
  1. System >> Administration >> Change Password
  2. Network
    1. Interface
      1. LAN: Edit
        1. `General Settings` >> Edit `IPv4 Gateway`
        2. `Advanced Settings` >> `Use custom DNS servers`
        3. (For Bypass Gateway) `DHCP Server`
          1. `General Setup` >> `Ignore interface`
          2. `IPv6 Settings` >> Disable `RA-Service`, `DHCPv6-Service`, `NDP-Proxy`
      2. `Add new interface...` >> Add `DHCP Client` and `DHCPv6 Client`
    2. `DHCP and DNS` >> `Hostnames` >> Add Hostnames
    3. `Firewall` >> `Port Forwards` >> Add rules for devices connected to OpenWRT

6. Install `Tabby Terminal` from [https://github.com/Eugeny/tabby/releases/](https://github.com/Eugeny/tabby/releases/) and connect to `<IPAddress>`

### Problems

- Read-only file system
  - `e2fsck -y /dev/sda2`
  - Increase disk size
- Error relocating /usr/bin/curl: curl_global_trace: symbol not found
  - `opkg install libcurl4`
- Cannot read properties of null (reading 'dnsmasq')
  - `service dnsmasq restart`

## OpenClash Installation

1. In OpenWRT

```bash
#iptables
opkg update
opkg install coreutils-nohup bash iptables dnsmasq-full curl ca-certificates ipset ip-full iptables-mod-tproxy iptables-mod-extra libcap libcap-bin ruby ruby-yaml kmod-tun kmod-inet-diag unzip luci-compat luci luci-base

#nftables
opkg update
opkg install coreutils-nohup bash dnsmasq-full curl ca-certificates ipset ip-full libcap libcap-bin ruby ruby-yaml kmod-tun kmod-inet-diag unzip kmod-nft-tproxy luci-compat luci luci-base

#Problems
opkg remove dnsmasq && opkg install dnsmasq-full # opkg_install_cmd: Cannot install package dnsmasq-full.
opkg install coreutils
opkg install jsonfilter
opkg install ip6tables-mod-nat
opkg upgrade libcurl # avoid curl conflicts
```

2. Download `.ipk` from [https://github.com/vernesong/OpenClash/releases](https://github.com/vernesong/OpenClash/releases)
3. In OpenWRT

```bash
opkg install openssh-sftp-server
```

4. SFTP >> Upload OpenClash File to `/root`

```bash
opkg install /root/luci-app-openclash_<version>.ipk
```

5. Re-login Dashboard to access `Services`: `OpenClash`
6. `Plugin Settings` >> `Version Update`
7. `Config Subscribe` >> `Add` >> `Update Config`
8. `Overview` >> `Running Mode` >> `TUN`
9. `Plugin Settings` >> `IPv6 Settings`
  1. `Proxy IPv6 Traffic`
  2. `IPv6 Proxy Mode`
  3. `IPv6 DNS Resolve`
10. `Overwrite Settings` >> `General Settings` >> `Log Level` >> `Info Mode`

### Install Clash Core manually

1. OpenClash >> Plugin Settings >> Version Update
2. Download `.tar.gz` of `dev`, `meta`, `premium` from [https://github.com/vernesong/OpenClash/tree/core/master](https://github.com/vernesong/OpenClash/tree/core/master)
3. Extract and rename `clash` files to `clash`(`dev`), `clash_tun`(`premium`), `clash_meta`(`meta`)
4. Copy to `/etc/openclash/core`

## Possible solutions of network problems

- Problems
  - Disable Private DNS
  - Use Device MAC Address
  - Avoid DNS Server conflicts
  - Avoid IP Address conflicts
  - Synchronize System Time
- YouTube problems
  - Disable all dns in Overwrite Settings >> Developer Settings
  - Change clash config: dns > fallback
  - Add clash config: dns > nameserver-policy > "+.googlevideo.com": 8.8.8.8
  - Disable QUIC in Browser
- Meta Core only display IP in Log
  - Overwrite Settings >> Meta Settings >> Enable `Enable Sniffer`, `Forced Sniff Pure IP`, `Custom Sniffer Settings`
- OpenWRT Hostname not working
  1. Network >> Global network options >> Set `IPv6 ULA-Prefix` (e.g.: `fc00::/64`)
  2. Set Client IPv6 DNS Server
- Port Forward not working
  - Switch to TUN mode
- WSL2 network problem
  - Switch to MIX mode

## Shadowsocks Installation

1. In OpenWRT

  ```bash
  opkg install shadowsocks-libev-ss-local shadowsocks-libev-ss-redir shadowsocks-libev-ss-rules shadowsocks-libev-ss-tunnel
  opkg install shadowsocks-libev-ss-server
  opkg install luci-app-shadowsocks-libev
  ```

2. Relogin Dashboard to access service: `Shadowsocks-libev`
3. `Shadowsocks-libev` >> `Local Instances` >> Edit and Enable `ss_server`
4. `Network` >> `Firewall` >> `Port Forwards` >> `Forward SS Ports`