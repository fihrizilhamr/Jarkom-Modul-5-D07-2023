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

