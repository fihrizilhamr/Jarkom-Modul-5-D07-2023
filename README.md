# Jarkom-Modul-5-D07-2023

## Pendahuluan

Repository ini dibentuk untuk menyelesaikan tugas praktikum Jaringan Komputer.

Anggota Kelompok D07:
| Nama | NRP |
| :---: | :---: |
| Danno Denis Dhaifullah | 5025211027 |
| Fihriz Ilham Rabbany | 5025211040 |

## Permasalahan

Setelah pandai mengatur jalur-jalur khusus, kalian diminta untuk membantu North Area menjaga wilayah mereka dan kalian dengan senang hati membantunya karena ini merupakan tugas terakhir.

  A. Tugas pertama, buatlah peta wilayah sesuai berikut ini:

<img width="587" alt="image" src="https://github.com/fihrizilhamr/Jarkom-Modul-5-D07-2023/assets/105486369/9504f936-4498-4cad-bb31-ce0a0d74b746">
  
      Keterangan:	
      - Richter adalah DNS Server
      - Revolte adalah DHCP Server
      - Sein dan Stark adalah Web Server
      - Jumlah Host pada SchwerMountain adalah 64
      - Jumlah Host pada LaubHills adalah 255
      - Jumlah Host pada TurkRegion adalah 1022
      - Jumlah Host pada GrobeForest adalah 512

  B. Untuk menghitung rute-rute yang diperlukan, gunakan perhitungan dengan metode VLSM. Buat juga pohonnya, dan lingkari subnet yang dilewati.
  
  C. Kemudian buatlah rute sesuai dengan pembagian IP yang kalian lakukan. 

  D. Tugas berikutnya adalah memberikan ip pada subnet SchwerMountain, LaubHills, TurkRegion, dan GrobeForest menggunakan bantuan DHCP.

### Soal

1. Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

2. Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

3. Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

4. Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

5. Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

6. Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

7. Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

8. Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

9. Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. 
(clue: test dengan nmap)

10. Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 


## Pembahasan

### A. Peta Wilayah

**Topologi VLSM**

<img alt="image" src="images/RUTE JARKOM MODUL 5 D07.png">



**Topologi GNS**

<img alt="image" src="images/TOPOLOGI JARKOM MODUL 5 D07.png">



### B. Rute, Tree, dan Pembagian IP

**Rute**

| Nama Subnet                             | Rute                                        | Jumlah IP | Netmask |
|-----------------------------------------|---------------------------------------------|-----------|---------|
| A1                                      | Aura-Frieren                                | 2         | /30     |
| A2                                      | Frieren-Stark                               | 2         | /30     |
| A3                                      | Frieren-Himmel                              | 2         | /30     |
| A4                                      | Himmel-LaubHills                            | 256       | /23     |
| A5                                      | Himmel-Switch1-Fern-Switch1-SchwerMountain | 66        | /25     |
| A6                                      | Fern-Richter                                | 2         | /30     |
| A7                                      | Fern-Switch2-Revolte                        | 2         | /30     |
| A8                                      | Aura-Heiter                                | 2         | /30     |
| A9                                      | Heiter-TurkRegion                           | 1023      | /21     |
| A10                                     | Heiter-Switch3-Sein-Switch3-GrobeForest    | 514       | /22     |
| Total                                   |                                             | 1871      | /20     |


**Tree**

<img alt="image" src="images/VLSM TREE JARKOM MODUL 5 D07.png">


**Pembagian IP**

| Subnet | Network ID    | Netmask             | Broadcast       |
|--------|---------------|---------------------|-----------------|
| A1     | 10.25.14.128  | 255.255.255.252     | 10.25.14.131    |
| A2     | 10.25.14.132  | 255.255.255.252     | 10.25.14.135    |
| A3     | 10.25.14.136  | 255.255.255.252     | 10.25.14.139    |
| A4     | 10.25.12.0    | 255.255.254.0       | 10.25.13.255    |
| A5     | 10.25.14.0    | 255.255.255.128     | 10.25.14.127    |
| A6     | 10.25.14.140  | 255.255.255.252     | 10.25.14.143    |
| A7     | 10.25.14.144  | 255.255.255.252     | 10.25.14.147    |
| A8     | 10.25.14.148  | 255.255.255.252     | 10.25.14.151    |
| A9     | 10.25.0.0     | 255.255.248.0       | 10.25.7.255     |
| A10    | 10.25.8.0     | 255.255.252.0       | 10.25.11.255    |

### C. Subnetting dan Routing

Setelah mengetahui pembagian IP dari masing masing subnet, sekarang kami dapat melakukan subnetting pada masing masing node yang ada dalam setiap subnet.

**Aura**

```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 10.25.14.129
	netmask 255.255.255.252

auto eth2
iface eth2 inet static
	address 10.25.14.149
	netmask 255.255.255.252
```

**Heiter**

```
auto eth0
iface eth0 inet static
        address 10.25.14.150
        netmask 255.255.255.252
        gateway 10.25.14.149

auto eth1
iface eth1 inet static
        address 10.25.0.1
        netmask 255.255.248.0

auto eth2
iface eth2 inet static
        address 10.25.8.1
        netmask 255.255.252.0
```

**Frieren**

```
auto eth0
iface eth0 inet static
        address 10.25.14.130
        netmask 255.255.255.252
        gateway 10.25.14.129

auto eth1
iface eth1 inet static
        address 10.25.14.133
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
        address 10.25.14.137
        netmask 255.255.255.252
```

**Himmel**

```
auto eth0
iface eth0 inet static
        address 10.25.14.138
        netmask 255.255.255.252
        gateway 10.25.14.137

auto eth1
iface eth1 inet static
        address 10.25.12.1
        netmask 255.255.254.0

auto eth2
iface eth2 inet static
        address 10.25.14.1
        netmask 255.255.255.128
```

**Fern**

```
auto eth0
iface eth0 inet static
        address 10.25.14.2
        netmask 255.255.255.128
        gateway 10.25.14.1

auto eth1
iface eth1 inet static
        address 10.25.14.141
        netmask 255.255.255.252

auto eth2
iface eth2 inet static
        address 10.25.14.145
        netmask 255.255.255.252
```

**Sein**

```
auto eth0
iface eth0 inet static
	address 10.25.8.2
	netmask 255.255.252.0
	gateway 10.25.8.1
```

**Stark**

```
auto eth0	
iface eth0 inet static	
	address 10.25.14.134
	netmask 255.255.255.252	
	gateway 10.25.14.133
```

**Revolte**

```
auto eth0	
iface eth0 inet static
	address 10.25.14.146
	netmask 255.255.255.252
	gateway 10.25.14.145
```

**Richter**

```
auto eth0	
iface eth0 inet static	
	address 10.25.14.142
	netmask 255.255.255.252	
	gateway 10.25.14.141
```

**Client**

```
auto eth0
iface eth0 inet dhcp
```

Setelah melakukan subnetting pada masing masing node yang ada, Selanjutnya kami bisa melakukan Routing:

**Aura**

```
route add -net 10.25.14.132 netmask 255.255.255.252 gw 10.25.14.130
route add -net 10.25.14.136 netmask 255.255.255.252 gw 10.25.14.130
route add -net 10.25.12.0 netmask 255.255.254.0 gw 10.25.14.130
route add -net 10.25.14.0 netmask 255.255.255.128 gw 10.25.14.130
route add -net 10.25.14.140 netmask 255.255.255.252 gw 10.25.14.130
route add -net 10.25.14.144 netmask 255.255.255.252 gw 10.25.14.130
route add -net 10.25.0.0 netmask 255.255.248.0 gw 10.25.14.150
route add -net 10.25.8.0 netmask 255.255.252.0 gw 10.25.14.150
```

**Heiter**

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.25.14.149
```

**Frieren**

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.25.14.129
route add -net 10.25.12.0 netmask 255.255.254.0 gw 10.25.14.138
route add -net 10.25.14.0 netmask 255.255.255.128 gw 10.25.14.138
route add -net 10.25.14.140 netmask 255.255.255.252 gw 10.25.14.138
route add -net 10.25.14.144 netmask 255.255.255.252 gw 10.25.14.138
```

**Himmel**

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.25.14.137
route add -net 10.25.14.140 netmask 255.255.255.252 gw 10.25.14.2
route add -net 10.25.14.144 netmask 255.255.255.252 gw 10.25.14.2
```

**Fern**

```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.25.14.1
```



### D. Konfigurasi

#### Konfigurasi DHCP Server
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf

apt-get update
apt-get install isc-dhcp-server -y

echo "
INTERFACESv4=\"eth0\"
INTERFACESv6=\"\"" > /etc/default/isc-dhcp-server

service isc-dhcp-server restart

echo "
subnet 10.25.14.128 netmask 255.255.255.252 {
}
subnet 10.25.14.132 netmask 255.255.255.252 {
}
subnet 10.25.14.136 netmask 255.255.255.252 {
}
subnet 10.25.14.140 netmask 255.255.255.252 {
}
subnet 10.25.14.144 netmask 255.255.255.252 {
}
subnet 10.25.14.148 netmask 255.255.255.252 {
}
subnet 10.25.0.0 netmask 255.255.248.0 {
	range 10.25.0.2 10.25.7.254;
	option routers 10.25.0.1;
	option broadcast-address 10.25.7.255;
	option domain-name-servers 10.25.14.142;
	default-lease-time 720;
	max-lease-time 5760;
}

subnet 10.25.8.0 netmask 255.255.252.0 {
	range 10.25.8.3 10.25.11.254;
	option routers 10.25.8.1;
	option broadcast-address 10.25.11.255;
	option domain-name-servers 10.25.14.142;
	default-lease-time 720;
	max-lease-time 5760;
}
subnet 10.25.12.0 netmask 255.255.254.0 {
	range 10.25.12.2 10.25.13.254;
	option routers 10.25.12.1;
	option broadcast-address 10.25.13.255;
	option domain-name-servers 10.25.14.142;
	default-lease-time 720;
	max-lease-time 5760;
}

subnet 10.25.14.0 netmask 255.255.255.128 {
	range 10.25.14.3 10.25.14.126;
	option routers 10.25.14.1;
	option broadcast-address 10.25.14.127;
	option domain-name-servers 10.25.14.142;
	default-lease-time 720;
	max-lease-time 5760;
}
" > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

#### Konfigurasi DHCP Relay
```
apt-get update
apt-get install isc-dhcp-relay -y

echo "
SERVERS=\"10.25.14.146\"
INTERFACES=\"eth0 eth1 eth2 eth3 eth4\"
OPTIONS=\"\"" > /etc/default/isc-dhcp-relay

echo "
net.ipv4.ip_forward=1" >> /etc/sysctl.conf

service isc-dhcp-relay start
```

#### Konfigurasi DNS Server
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf

apt-get update
apt-get install bind9 -y

service bind9 restart

echo "
options {
    directory \"/var/cache/bind\";

    forwarders {
        8.8.8.8;
        8.8.8.4;
        192.168.122.1;
        0.0.0.0;
    };

    // dnssec-validation auto;
    allow-query { any; };
    auth-nxdomain no;
    listen-on-v6 { any; };
};" > /etc/bind/named.conf.options

service bind9 restart
```
#### Konfigurasi Client
```
echo "nameserver 192.168.122.1" > /etc/resolv.conf
apt-get update
apt-get install netcat -y
apt-get install nmap -y
```


### 1. Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

#### Script

....................

#### Testing

....................

### 2. Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

#### Script

....................

#### Testing

....................

### 3. Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

#### Script

....................

#### Testing

....................

### 4. Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

#### Script

....................

#### Testing

....................

### 5. Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

#### Script

Jalankan script dibawah ini pada masing-masing webserver agar web server hanya dapat diakses saat jam kerja yaitu Senin-Jumat pada pukul 08.00 - 16.00.

```
# Allow HTTP access only outside restricted hours (Monday-Thursday 12:00-13:00, Friday 11:00-13:00)
iptables -A INPUT -p tcp --dport 80 -m time --timestart 07:00 --timestop 11:59 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -m time --timestart 13:01 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -m time --timestart 07:00 --timestop 10:59 --weekdays Fri -j ACCEPT
iptables -A INPUT -p tcp --dport 80 -m time --timestart 13:01 --timestop 16:00 --weekdays Fri -j ACCEPT

# Drop HTTP traffic during restricted hours (Monday-Thursday 12:00-13:00, Friday 11:00-13:00)
iptables -A INPUT -p tcp --dport 80 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP
iptables -A INPUT -p tcp --dport 80 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP

# Drop other HTTP traffic
iptables -A INPUT -p tcp --dport 80 -j DROP
```
#### Testing

Dibawah ini merupakan hasil ``iptables -L`` setelah kita menjalankan script diatas.

<img width="981" alt="image" src="https://github.com/fihrizilhamr/Jarkom-Modul-5-D07-2023/assets/105486369/dbb9bd99-c4e4-4c2f-8512-605e00bf9fa0">

Setelah itu kita bisa mencoba melakukan testing dengan mengubah waktu pada node sein dengan sintaks berikut:

```
date 121314002023.00
```

Argumen di atas akan membuat waktu menjadi pukul 14:00 dan sesuai dengan petunjuk di soal, selanjutnya kami perlu menjalankan ``nc -l -p 80`` pada **sein** dan ``nc 10.12.8.2 80`` pada **client**. Hasilnya sein dan client akan bisa saling berbagi pesan menggunakan netcat.

Jika waktu diubah menuju jam malam, yaitu 19:00 (tidak sesuai dengan syarat), maka kedua node tersebut tidak akan bisa berbagi pesan menggunakan netcat.

### 6. Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

#### Script

....................

#### Testing

....................

### 7. Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

#### Script

....................

#### Testing

....................

### 8. Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

#### Script

....................

#### Testing

....................

### 9. Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit. (clue: test dengan nmap)

#### Script

....................

#### Testing

....................

### 10. Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

#### Script

....................

#### Testing

....................

### Kendala

Dalam pengerjaan Soal nomor 9 dan 10, kami mengalami beberapa kendala. Untuk nomor 9, kami kesulitan menemukan informasi mengenai scanning port dalam modul, sehingga kami perlu mencari informasi tambahan melalui pencarian online, yang memakan waktu lebih lama. Sementara itu, pada nomor 10, kami menghadapi kesulitan dalam menciptakan log. Kami terus mendapatkan kesalahan saat mencoba mengimpor Image Ubuntu yang benar ke GNS3.