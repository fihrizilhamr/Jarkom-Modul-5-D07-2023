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

<img width="666" alt="image" src="https://github.com/fihrizilhamr/Jarkom-Modul-5-D07-2023/assets/105486369/aa47913b-3e20-40b2-bfba-ceeddeebd735">



**Topologi GNS**

<img width="824" alt="image" src="https://github.com/fihrizilhamr/Jarkom-Modul-5-D07-2023/assets/105486369/93930d8c-e332-4a5e-8102-5a144c8fa421">



### B. Rute, Tree, dan Pembagian IP

**Rute**

DIISI FOTO

**Tree**

DIISI FOTO

**Pembagian IP**

<img width="909" alt="image" src="https://github.com/fihrizilhamr/Jarkom-Modul-5-D07-2023/assets/105486369/a8aea2b0-bfbd-4f1f-a4e3-962dfa14e037">



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
