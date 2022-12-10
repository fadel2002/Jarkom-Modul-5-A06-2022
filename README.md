# Lapres Jarkom Kelompok A06

## Anggota Kelompok

1. Hans Sean Nathanael - 5025201019
2. Mohammad Fany Faizul Akbar - 5025201225
3. Fadel Pramaputra Maulana - 502520126

## VLSM

Pembagian IP topologi menggunakan metode VLSM. Berikut adalah pembagian subnet

![Pembagian Subnet](images/topologi.png)

Kemudian dihitung jumlah host yang dibutuhkan, netmask, dan IP setiap subnet.

![Tabel VLSM](images/Tabel%20VLSM.png)
![Tree IP Subnet](images/Tree%20Jaringan%20VLSM.png)

IP Subnet didapat dari Tree pembagian IP.

## Konfigurasi Node

1. Strix

```bash
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.2.0.1
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.2.0.5
	netmask 255.255.255.252
```

2. Ostania

```bash
auto eth0
iface eth0 inet static
	address 10.2.0.2
	netmask 255.255.255.252
	gateway 10.2.0.1

auto eth1
iface eth1 inet static
	address 10.2.0.9
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 10.2.1.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 10.2.2.1
	netmask 255.255.254.0
```

3. Westalis

```bash
auto eth0
iface eth0 inet static
	address 10.2.0.6
	netmask 255.255.255.252
	gateway 10.2.0.5

auto eth1
iface eth1 inet static
	address 10.2.0.17
	netmask 255.255.255.248

auto eth2
iface eth2 inet static
	address 10.2.4.1
	netmask 255.255.252.0

auto eth3
iface eth3 inet static
	address 10.2.0.129
	netmask 255.255.255.128
```

4. Eden

```bash
auto eth0
iface eth0 inet static
	address 10.2.0.18
	netmask 255.255.255.248
	gateway 10.2.0.17
```

5. WISE

```bash
auto eth0
iface eth0 inet static
	address 10.2.0.19
	netmask 255.255.255.248
	gateway 10.2.0.17
```

6. Garden

```bash
auto eth0
iface eth0 inet static
	address 10.2.0.10
	netmask 255.255.255.248
	gateway 10.2.0.9
```

7. SSS

```bash
auto eth0
iface eth0 inet static
	address 10.2.0.11
	netmask 255.255.255.248
	gateway 10.2.0.9
```

8. Forger, Desmond, Blackbell, dan Briar

```bash
auto eth0
iface eth0 inet dhcp
```

## Pembagian Tugas

1. Eden adalah DNS Server

Karena Eden harus menjadi DNS Server, maka bind9 diinstall pada Eden.

```bash 
apt-get update
apt-get install bind9 -y
```

2. WISE adalah DHCP Server

Pada WISE diinstall isc-dhcp-server

```bash
apt-get update
apt-get install isc-dhcp-server -y
```

3. Garden dan SSS adalah Web Server

Pada Garden dan SSS diinstall apache2 dan php

```bash 
apt-get update
apt-get install apache2 -y
service apache2 start
apt-get install php -y
```

4. DHCP Relay

Karena pemberian IP subnet Forger, Desmond, Blackbell, dan Briar harus secara dinamis menggunakan DHCP Server yaitu dengan WISE sebagai DHCP Server, maka diperlukan DHCP Relay pada setiap router yang terhubung dengan keempat subnet tersebut, yaitu router Ostania dan Westalis. Pada kedua router tersebut diinstall isc-dhcp-relay

```bash
apt-get update
echo "10.2.0.19" | apt-get install isc-dhcp-relay -y
```
