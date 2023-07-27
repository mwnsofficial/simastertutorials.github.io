---
title: Setting hotspot linux armbian hg680p b860h
layout: post
description: Cara mengatur hotspot linux armbian di perangkat hg680p dan b860h
image: images/blog/setting-hotspot-linux-armbian.jpg
image-alt: mengatur hotspot linux armbian hg680p dan b860h
tags: [armbian]
---
Pada kali ini kita akan belajar cara bagaimana membuat hotspot di linux armbian pada
perangkat hg680p atau b860h (wajib support wifi).

hal yang pertama kita lakukan adalah menginstall beberapa repository terlebih dahulu.

Silahkan buka terminal emulator pada masing masing perangkat anda. Kemudian buatkan perintah di bawah ini:

<pre rel="HTML" class="code-box"><code>
sudo apt update
</code></pre>

Kemudian kita install

<pre rel="HTML" class="code-box"><code>
sudo apt-get install hostapd isc-dhcp-server
</code></pre>

Tunggu hingga selesai dan tidak ada kendala apa pun.

Kemudian buat perintah kembali

<pre rel="HTML" class="code-box"><code>
sudo nano /etc/default/isc-dhcp-server
</code></pre>

nanti isikan seperti di bawah ini

<pre rel="HTML" class="code-box"><code>
# Defaults for isc-dhcp-server (sourced by /etc/init.d/isc-dhcp-server)

# Path to dhcpd's config file (default: /etc/dhcp/dhcpd.conf).
#DHCPDv4_CONF=/etc/dhcp/dhcpd.conf
#DHCPDv6_CONF=/etc/dhcp/dhcpd6.conf

# Path to dhcpd's PID file (default: /var/run/dhcpd.pid).
#DHCPDv4_PID=/var/run/dhcpd.pid
#DHCPDv6_PID=/var/run/dhcpd6.pid

# Additional options to start dhcpd with.
#	Don't use options -cf or -pf here; use DHCPD_CONF/ DHCPD_PID instead
#OPTIONS=""

# On what interfaces should the DHCP server (dhcpd) serve DHCP requests?
#	Separate multiple interfaces with spaces, e.g. "eth0 eth1".
INTERFACESv4="wlan0"
INTERFACESv6="wlan0"
</code></pre>

Untuk interface hotspot kalian pastikan sama dengan settingan di advance connection di armbian anda.

Jika sudah, silahkan tekan `Control` atau `CTRL` tekan barengan sama tombol `O` (o besar bukan angka 0 ya bro) kemudian tekan enter lalu `CTRL` barengan dengan tombol `X`.

Itu adalah langkah awal untuk setting interfaces di armbian anda.

Kemudian buat perintah kembali untuk setting dhcp server nya

<pre rel="HTML" class="code-box"><code>
sudo nano /etc/dhcp/dhcpd.conf
</code></pre>

lalu isikan seperti di bawah ini

<pre rel="HTML" class="code-box"><code>
# dhcpd.conf
#
# Sample configuration file for ISC dhcpd
#
# Attention: If /etc/ltsp/dhcpd.conf exists, that will be used as
# configuration file instead of this file.
#

# option definitions common to all supported networks...
#option domain-name "example.org";
#option domain-name-servers ns1.example.org, ns2.example.org;

default-lease-time 600;
max-lease-time 7200;

# The ddns-updates-style parameter controls whether or not the server will
# attempt to do a DNS update when a lease is confirmed. We default to the
# behavior of the version 2 packages ('none', since DHCP v2 didn't
# have support for DDNS.)
#ddns-update-style none;

# If this DHCP server is the official DHCP server for the local
# network, the authoritative directive should be uncommented.
#authoritative;

# Use this to send dhcp log messages to a different log file (you also
# have to hack syslog.conf to complete the redirection).
#log-facility local7;

# No service will be given on this subnet, but declaring it helps the 
# DHCP server to understand the network topology.

#subnet 192.168.10.0 netmask 255.255.255.0 {
#}

# This is a very basic subnet declaration.

subnet 192.168.10.0 netmask 255.255.255.0 {
  range 192.168.10.2 192.168.10.200;
  option routers 192.168.10.1;
}

# This declaration allows BOOTP clients to get dynamic addresses,
# which we don't really recommend.

#subnet 10.254.239.32 netmask 255.255.255.224 {
#  range dynamic-bootp 10.254.239.40 10.254.239.60;
#  option broadcast-address 10.254.239.31;
#  option routers rtr-239-32-1.example.org;
#}

# A slightly different configuration for an internal subnet.
#subnet 10.5.5.0 netmask 255.255.255.224 {
#  range 10.5.5.26 10.5.5.30;
#  option domain-name-servers ns1.internal.example.org;
#  option domain-name "internal.example.org";
#  option subnet-mask 255.255.255.224;
#  option routers 10.5.5.1;
#  option broadcast-address 10.5.5.31;
#  default-lease-time 600;
#  max-lease-time 7200;
#}

# Hosts which require special configuration options can be listed in
# host statements.   If no address is specified, the address will be
# allocated dynamically (if possible), but the host-specific information
# will still come from the host declaration.

#host passacaglia {
#  hardware ethernet 0:0:c0:5d:bd:95;
#  filename "vmunix.passacaglia";
#  server-name "toccata.example.com";
#}

# Fixed IP addresses can also be specified for hosts.   These addresses
# should not also be listed as being available for dynamic assignment.
# Hosts for which fixed IP addresses have been specified can boot using
# BOOTP or DHCP.   Hosts for which no fixed address is specified can only
# be booted with DHCP, unless there is an address range on the subnet
# to which a BOOTP client is connected which has the dynamic-bootp flag
# set.
#host fantasia {
#  hardware ethernet 08:00:07:26:c0:a5;
#  fixed-address fantasia.example.com;
#}

# You can declare a class of clients and then do address allocation
# based on that.   The example below shows a case where all clients
# in a certain class get addresses on the 10.17.224/24 subnet, and all
# other clients get addresses on the 10.0.29/24 subnet.

#class "foo" {
#  match if substring (option vendor-class-identifier, 0, 4) = "SUNW";
#}

#shared-network 224-29 {
#  subnet 10.17.224.0 netmask 255.255.255.0 {
#    option routers rtr-224.example.org;
#  }
#  subnet 10.0.29.0 netmask 255.255.255.0 {
#    option routers rtr-29.example.org;
#  }
#  pool {
#    allow members of "foo";
#    range 10.17.224.10 10.17.224.250;
#  }
#  pool {
#    deny members of "foo";
#    range 10.0.29.10 10.0.29.230;
#  }
#}
</code></pre>

Kalo anda ingin IP DHCP yang berbeda boleh silahkan namun samakan dengan topologi anda.

Jika sudah mantap pada pilihan, silahkan anda simpan dengam menekan kembali tombol `CTRL` dengan tombol `O` barengan kembali lalu tekan `Enter` dan setelah itu tekan `CTRL` lalu barengan lagi dengan tombol `X`.

Dan langkah di bawah ini adalah langkah terakhir settingan kita

<pre rel="HTML" class="code-box"><code>
sudo nano /etc/hostapd/hostapd.conf
</code></pre>

Lalu pada driver, interface, ssid, hw mode, channel, wpa passphrase atau password dan lain nya samakan saja dengan settingan hotspot wifi kalian.

<pre rel="HTML" class="code-box"><code>
interface=wlan0
driver=rtl8189fs
ssid=simaster
hw_mode=b/g
channel=10
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_passphrase=scatternet
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
</code></pre>

Sampai disini kita sudah selesai setting bagian penting untuk management hotspot linux armbian di stb hg680p atau b860h anda.

tinggal membuat interface anda di menu lalu tekan advanced connection

ketikkan di terminal

<pre rel="HTML" class="code-box"><code>
nmtui
</code></pre>

lalu buatlah interface baru untuk di jadikan hotspot dengan menekan tombol `Add`.

mode wajib ke mode `Hotspot` bukan mode `client` ya bro.

lalu atur `ssid` anda dan samakan persis dengan settingan di `hostapd` dan `isc-dhcp-server` anda barusan.

Untuk MTU boleh default atau pun 1500 ya bro.

Dan perjalanan kita akan berakhir dengan membuat perintah

<pre rel="HTML" class="code-box"><code>
sudo systemctl start hostapd
</code></pre>

Ok bro, sampai disini dulu tutorial yang `Simaster Tutorials` berikan dan semoga bermanfaat.
