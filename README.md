# Jarkom-Modul-5-F13-2022

## Penyelesaian Soal Praktikum Modul 5 Jaringan Komputer

* Muhammad Andi Akbar Ramadhan (5025201264)
* Natya Madya Marciola	(5025201238)
* Neisa Hibatillah Alif	(5025201170)

### (A) Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Loid
![image](https://user-images.githubusercontent.com/91374949/206849493-a399cd05-8907-47a7-9c7e-3d9c91f4dfbc.png)

Keterangan :	Eden adalah DNS Server
- WISE adalah DHCP Server
- Garden dan SSS adalah Web Server
- Jumlah Host pada Forger adalah 62 host
- Jumlah Host pada Desmond adalah 700 host
- Jumlah Host pada Blackbell adalah 255 host
- Jumlah Host pada Briar adalah 200 host

### (B) Untuk menjaga perdamaian dunia, Loid ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM setelah melakukan subnetting.
### Subnetting (VLSM)

Dari topologi di atas, tentukan jumlah subnet yang ada di dalam topologi tersebut.
![topologi](https://user-images.githubusercontent.com/91374949/206849668-8e3d79c7-4c1e-4a43-9333-8ef99f3ed1e7.png)

Terdapat 8 subnet di dalam topologi. Lalu tentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan.
| Subnet | Jumlah IP | Netmask |
|--|--|--|
| A1 | 3 | /29 |
| A2 | 63 | /25 |
| A3 | 701 | /22 |
| A4 | 2 | /30 |
| A5 | 2 | /30 |
| A6 | 256 | /23 |
| A7 | 201 | /24 |
| A8 | 3 | /29 |
| **Total** | **1231** | **/21** |

Berdasarkan total IP dan netmask yang dibutuhkan, diperoleh hasil total IP yang digunakan sebanyak 1231, sehingga netmask yang digunakan adalah /21.

Dari tabel subnetting sebelumnya, dilakukan pembagiann IP berdasarkan NID dan netmask menggunakan pohon seperti gambar di bawah sampai semua subnet yang diminta pada topologi mendapat bagiannya.

![subnetting (1)](https://user-images.githubusercontent.com/91374949/206850588-a6f463c2-d80b-4f92-92a1-59cc83450788.jpg)
Kemudian, dari pohon tersebut akan didapat pembagian IP sebagai berikut.
![image](https://user-images.githubusercontent.com/91374949/206851053-71d6a041-28fd-4efe-a0b9-e2407a1bf95c.png)

Berdasarkan pembagian tadi, atur IP untuk masing-masing interface yang ada di setiap device
- [Ostania]
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.35.0.6
netmask 255.255.255.252
gateway 10.35.0.5

auto eth1
iface eth1 inet static
address 10.35.2.1
netmask 255.255.254.0

auto eth2
iface eth2 inet static
address 10.35.0.25
netmask 255.255.255.248

auto eth3
iface eth3 inet static
address 10.35.1.1
netmask 255.255.255.0
```

- [Strix]
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
address 10.35.0.5
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 10.35.0.2
netmask 255.255.255.252
```

- [Westalis]
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.35.0.2
netmask 255.255.255.252
gateway 10.35.0.1

auto eth1
iface eth1 inet static
address 10.35.4.1
netmask 255.255.252.0

auto eth2
iface eth2 inet static
address 10.35.0.129
netmask 255.255.255.128

auto eth3
iface eth3 inet static
address 10.35.0.17
netmask 255.255.255.248
```

- [Eden]
```
auto eth0
iface eth0 inet static
address 10.35.0.19
netmask 255.255.255.248
gateway 10.35.0.17
```

- [Garden]
```auto eth0
iface eth0 inet static
address 10.35.0.26
netmask 255.255.255.248
gateway 10.35.0.25
```

- [SSS]
```
auto eth0
iface eth0 inet static
address 10.35.0.27
netmask 255.255.255.248
gateway 10.35.0.25
```

- [WISE]
```
auto eth0
iface eth0 inet static
address 10.35.0.18
netmask 255.255.255.248
gateway 10.35.0.17
```

- [Forger]
```
auto eth0
iface eth0 inet static
address 10.35.0.130
netmask 255.255.255.128
gateway 10.35.0.129
```

- [Desmond]
```
auto eth0
iface eth0 inet static
address 10.35.4.2
netmask 255.255.252.0
gateway 10.35.4.1
```

- [Blackbell]
```
auto eth0
iface eth0 inet static
address 10.35.2.2
netmask 255.255.254.0
gateway 10.35.2.1
```

- [Briar]
```
auto eth0
iface eth0 inet static
address 10.35.1.2
netmask 255.255.255.0
gateway 10.35.1.1
```

### (C) Anya, putri pertama Loid, juga berpesan kepada anda agar melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.
### Routing

- [Ostania]
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.35.0.5
```

- [Strix]
```
route add -net 10.35.0.16 netmask 255.255.255.248 gw 10.35.0.2 
route add -net 10.35.0.128 netmask 255.255.255.128 gw 10.35.0.2 
route add -net 10.35.4.0 netmask 255.255.252.0 gw 10.35.0.2 

route add -net 10.35.2.0 netmask 255.255.254.0 gw 10.35.0.6 
route add -net 10.35.1.0 netmask 255.255.255.0 gw 10.35.0.6 
route add -net 10.35.0.24 netmask 255.255.255.248 gw 10.35.0.6 
```

- [Westalis]
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.35.0.1
```

### (D) Tugas berikutnya adalah memberikan ip pada subnet Forger, Desmond, Blackbell, dan Briar secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

- [Forger, Desmond, Blackbell, Briar]
Edit network config masing-masing dan masukkan :
```
auto eth0
iface eth0 inet dhcp
```

- [WISE]
Pertama, lakukan ```apt install isc-dhcp-server```, kemudian edit file ```/etc/dhcp/dhcpd.conf```, isikan file tersebut dengan berikut.

```
# Ke A2 (Forger)
subnet 10.35.0.128 netmask 255.255.255.128 {
    range 10.35.0.130 10.35.0.254;
    option routers 10.35.0.129;
    option broadcast-address 10.35.0.255;
    option domain-name-servers 10.35.0.19; # IP Eden
    default-lease-time 600;
    max-lease-time 7200;
}

# Ke A3 (Desmond)
subnet 10.35.4.0 netmask 255.255.252.0 {
    range 10.35.4.2 10.35.7.255;
    option routers 10.35.4.1;
    option broadcast-address 10.35.5.255;
    option domain-name-servers 10.35.0.19; # IP Eden
    default-lease-time 600;
    max-lease-time 7200;
}

# Ke A6 (Blackbell)
subnet 10.35.2.0 netmask 255.255.254.0 {
    range 10.35.2.2 10.35.3.255;
    option routers 10.35.2.1;
    option broadcast-address 10.35.3.255;
    option domain-name-servers 10.35.0.19;
    default-lease-time 600;
    max-lease-time 7200;
}

# Ke A7 (Briar)
subnet 10.35.1.0 netmask 255.255.255.0 {
    range 10.35.1.2 10.35.1.255;
    option routers 10.35.1.1;
    option broadcast-address 10.35.1.255;
    option domain-name-servers 10.35.0.19;
    default-lease-time 600;
    max-lease-time 7200;
}

# Ke A1
subnet 10.35.0.16 netmask 255.255.255.248 {
}
```

- [Strix]
Lanjut ke Strix, lakukan ```apt-get update``` serta ```apt-get -y install isc-dhcp-relay```.
Setelah itu, buka ```/etc/default/isc-dhcp-relay``` dan sesuaikan bagian-bagian di file dengan berikut.
```
SERVERS="10.35.0.18"			// address dhcp server

INTERFACES="eth1 eth2"

OPTIONS=""
```
Kemudian, ```cp /etc/default/isc-dhcp-relay isc-dhcp-relay```, dan restart isc-dhcp-relay.

- [Ostania, Westalis]
Untuk Ostania dan Westalis, langkah mirip dengan Strix barusan namun terdapat perbedaan di config ```/etc/default/isc-dhcp-relay```. Kembali sesuaikan bagian-bagian di file dengan berikut.
```
SERVERS="10.35.0.18"			// address dhcp server

INTERFACES="eth0 eth1 eth2 eth3"

OPTIONS=""
```

Gunakan ```cp /etc/default/isc-dhcp-relay isc-dhcp-relay```, dan restart isc-dhcp-relay.
