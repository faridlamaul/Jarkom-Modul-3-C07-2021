# Jarkom-Modul-3-C07-2021

Kelompok C07

|      NRP       |                  Nama                   |
| :------------: | :-------------------------------------: |
| 05111940000046 |       Titian Pamungkas Anjasmara        |
| 05111940000134 |           Ahmad Lamaul Farid            |
| 05111940000150 | Jonathan Leonardo Hasiholan Simanjuntak |

## Soal 1

```
Luffy bersama Zoro berencana membuat peta tersebut dengan kriteria EniesLobby sebagai DNS Server, Jipangu sebagai DHCP Server, Water7 sebagai Proxy Server
```

### Jawaban

**Config**

Kita perlu mengkonfigurasi node foosha dan node pada switch 2, agar dapat melakukan penginstalan package

![1](https://user-images.githubusercontent.com/77373958/141627482-bc8bc896-dfd0-48dc-ac44-1ac01b5abbe7.PNG)

![2](https://user-images.githubusercontent.com/77373958/141627543-8007a85d-1682-421e-afa0-8fc75d319fc6.PNG)

![3](https://user-images.githubusercontent.com/77373958/141627589-1e549a29-be5c-439c-a257-6af2c4a3d855.PNG)

![4](https://user-images.githubusercontent.com/77373958/141627624-6b324278-aa7a-4bb8-b5cd-2a379f8ec4e8.PNG)

**EniesLobby**

- Lakukan Penginstalan bind9 dengan menggunakan `apt-get update` dan `apt-get install bind9 -y`

**Jipangu**

- Lakukan Penginstalan dhcp server dengan menggunakan `apt-get update` dan `apt-get install isc-dhcp-server -y`

**Water7**

- Lakukan Penginstalan proxy dengan menggunakan `apt-get update` dan `apt-get install squid -y`

## Soal 2

```
Foosha sebagai DHCP Relay
```

### Jawaban

**Foosha**

- Lakukan Penginstalan DHCP relay dengan menggunakan `apt-get update` dan `apt-get install isc-dhcp-relay -y`

- Buka file `/etc/default/isc-dhcp-relay`, kemudian ubah isinya menjadi sebagai berikut. Server mengarah ke IP jipangu (DHCP server) dan ethernet 1, 2, dan 3.

![5](https://user-images.githubusercontent.com/77373958/141632902-81719b15-c142-4f89-80f3-a995c00705fe.PNG)


## Soal 3

```
Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.20 - [prefix IP].1.99 dan [prefix IP].1.150 - [prefix IP].1.169
```

### Jawaban

**Config client**

- Lakukan config pada semua client terlebih dahulu (Loguetown, Alabasta, Tottoland, Skypie) dengan konfigurasi sebagai berikut.

![12](https://user-images.githubusercontent.com/77373958/141642281-074fce7d-1846-4858-bad0-4c4e0f0b2c35.PNG)

**Jipangu**

- Buka `/etc/default/isc-dhcp-server`, dan ubah interface menjadi eth0

![6](https://user-images.githubusercontent.com/77373958/141634679-dfea2faa-d3d3-4e97-b018-f16aa8b63b3b.PNG)

- Buka `/etc/dhcp/dhcpd.conf`, dan tambahkan `range 192.187.1.20 192.187.1.99` dan `range 192.187.1.150 192.188.1.169`.

![10](https://user-images.githubusercontent.com/77373958/141636315-e2714e56-d9ac-4e07-91ed-162dd31cd195.PNG)


## Soal 4

```
Client yang melalui Switch3 mendapatkan range IP dari [prefix IP].3.30 - [prefix IP].3.50
```

### Jawaban

**Jipangu**

- Buka `/etc/dhcp/dhcpd.conf`, dan tambahkan `range 192.187.3.30 192.187.3.50`.

![11](https://user-images.githubusercontent.com/77373958/141636416-5ed187ec-de8d-4b6d-9d1d-03c1a2156178.PNG)

## Soal 5

```
Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut.
```

### Jawaban

**Jipangu**

- Ubah option domain nameserver pada masing-masing subnet dengan penambahan IP EniesLobby.

![10](https://user-images.githubusercontent.com/77373958/141641679-9d56ccb9-b48b-4323-8166-d2be32f8e36c.PNG)

![11](https://user-images.githubusercontent.com/77373958/141641731-0302afc5-3fe5-4d70-a110-b75472afdc9c.PNG)

## Soal 6

```
Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit.
```

### Jawaban

**Jipangu**

- Ubah max lease time pada kedua subnet menjadi 7200, sedangkan default lease time pada subnet 1 yaitu 360 dan default lease time pada subnet 3 yaitu 720

![10](https://user-images.githubusercontent.com/77373958/141642122-7568e98e-03ac-4c57-8ee5-5fde2bee1b70.PNG)

![11](https://user-images.githubusercontent.com/77373958/141642125-51b50925-fe3c-472d-b92b-7fa61539b990.PNG)

## Pengecekan kriteria

![kenek](https://user-images.githubusercontent.com/77373958/141642158-290590eb-01bb-4081-b03f-5d9421eb4a8e.PNG)

![kenek2](https://user-images.githubusercontent.com/77373958/141642165-b8244315-059a-4d9e-97a1-0379ca43c14c.PNG)

![kenek3](https://user-images.githubusercontent.com/77373958/141642166-a0a62ef9-5d51-4264-a42a-f0fdbff067cf.PNG)

![kenek4](https://user-images.githubusercontent.com/77373958/141642168-662a195e-c8c0-4cda-abb5-b34ea429afb1.PNG)

## Soal 7

```
Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP [prefix IP].3.69
```

### Jawaban

**Jipangu**

-   Edit file `/etc/dhcp/dhcpd.conf` seperti pada gambar berikut:

    ![7.1](images/7.1-Jipangu.PNG)

-   Perhatikan pada baris hardware ethernet. Nilai `hardware ethernet tersebut merupakan nilai MAC address dari interface eth0 milik Skypie`. Cara mendapatkannya, masukkan perintah `ip a` pada node Skypie, dan salin IP Mac eth0 yang ditunjukkan. Untuk lebih jelasnya, perhatikan gambar berikut.

    ![7.2](images/7.2-Skypie.PNG)

-   Restart service isc-dhcp-server pada Jipangu dengan perintah :

    ```
      service isc-dhcp-server restart
    ```

**Skypie**

-   Edit file `/etc/network/interfaces` seperti pada gambar berikut:

    ![7.3](images/7.3-Skypie.PNG)

    _Nilai hwaddress menyesuaikan dengan MAC Address milik node Skypie_

-   Restart node Skypie. Maka, IP address node Skypie akan menjadi fixed IP address, sesuai dengan nilai yang telah ditetapkan.

    ![7.4](images/7.4-Skypie.PNG)

## Soal 8

```
Pada Loguetown, proxy harus bisa diakses dengan nama jualbelikapal.yyy.com dengan port yang digunakan adalah 5000
```

### Jawaban

**EniesLobby**

-   Update library dari ubuntu dengan perintah `apt-get update`.

-   Install `bind9` dengan memasukkan perintah `apt-get install bind9 -y`.

-   Edit file `/etc/bind/named.conf.local` seperti pada gambar berikut :

    ![8.1](images/8.1-EniesLobby.PNG)

-   Buat folder `jarkom` di direktori `/etc/bind/` dengan perintah :

    ```
    mkdir /etc/bind/jarkom
    ```

-   Ketikkan `cp /etc/bind/db.local /etc/bind/jarkom/jualbelikapal.c07.com` untuk meng-copy file dari `db.local` menjadi `jualbelikapal.c07.com`.

-   Edit file `/etc/bind/jarkom/jualbelikapal.c07.com` seperti pada gambar berikut :

    ![8.2](images/8.2-EniesLobby.PNG)

-   Restart service bind9 dengan perintah :
    ```
    service bind9 restart
    ```

**Water7**

-   Update library dari ubuntu dengan perintah `apt-get update`.

-   Install `squid3` dengan memasukkan perintah `apt-get install squid -y`.

-   Lakukan backup file `squid.conf` dengan merubah nama filenya menggunakan perintah :

    ```
    mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
    ```

-   Edit file `/etc/squid/squid.conf` seperti pada gambar berikut :

    ![8.3](images/8.3-Water7.PNG)

-   Restart service squid3 dengan perintah :
    ```
    service squid restart
    ```

**Loguetown**

-   Update library dari ubuntu dengan perintah `apt-get update`.

-   Install `lynx` dengan memasukkan perintah `apt-get install lynx -y`.

-   Aktifkan proxy pada node client Loguetown dengan menggunakan perintah :

    ```
    export http_proxy="http://jualbelikapal.c07.com:5000"
    ```

-   Pastikan konfigurasi proxy sudah berhasil dengan memasukkan perintah :

    ```
    env | grep -i proxy
    ```

    ![8.4](images/8.4-LogueTown.PNG)

-   Kemudian, buka alamat `google.com` dengan menggunakan perintah :

    ```
    lynx google.com
    ```

-   Ketika berhasil dikunjungi, maka akan tampil seperti pada gambar berikut :

    ![8.5](images/8.5-LogueTown.PNG)

    _P.S : Konfigurasi pada server proxy Water7 masih di set untuk menolak semua akses HTTP (secara default)_

## Soal 9

```
 Agar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu luffybelikapalyyy dengan password luffy_yyy dan zorobelikapalyyy dengan password zoro_yyy
```

### Jawaban

**Water7**

-   Update library dari ubuntu dengan perintah `apt-get update`.

-   Install `apache2-utils` dengan memasukkan perintah `apt-get install apache2-utils -y`.

-   Untuk membuat dua akun autentikasi user yang diminta, gunakan perintah :

    ```
    htpasswd -cbm /etc/squid/passwd luffybelikapalc07 luffy_c07
    htpasswd -bm /etc/squid/passwd zorobelikapalc07 zoro_c07
    ```

    Penjelasan :

    -   c = create. Untuk membuat passwdfile tempat dua akun tersebut disimpan.
    -   b = batch mode. Digunakan untuk memasukkan password lewat command line, sehingga tidak perlu ada menu prompt untuk input password.
    -   m = MD5 encryption

-   Edit file `/etc/squid/squid.conf` seperti pada gambar berikut :

    ![9.1](images/9.1-Water7.PNG)

-   Restart service squid3 dengan meggunakan perintah :

    ```
    service squid restart
    ```

**Loguetown**

-   Pastikan node sudah terhubung menggunakan proxy dengan memasukkan perintah :

    ```
    env | grep -i proxy
    ```

    ![9.2](images/9.2-LogueTown.PNG)

-   Buka alamat `google.com` dengan menggunakan perintah :

```
lynx google.com
```

-   Ketika tersambung, proxy akan melakukan autentikasi user terlebih dahulu. Masukkan username yang telah di konfigurasikan sebelumnya (contohnya luffybelikapalc07).

    ![9.3](images/9.3-LogueTown.PNG)

-   Masukkan password username yang digunakan (contohnya luffy_c07)

    ![9.4](images/9.4-LogueTown.PNG)

-   Jika benar, maka akan terlihat halaman yang diminta sebelumnya (google.com)

    ![9.5](images/9.5-LogueTown.PNG)

## Soal 10

```
Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari Senin-Kamis pukul 07.00-11.00 dan setiap hari Selasa-Jum’at pukul 17.00-03.00 keesokan harinya (sampai Sabtu pukul 03.00)
```

### Jawaban

**Water7**

-   Buat file baru pada `/etc/squid/acl.conf`. Kemudian, edit file menjadi seperti gambar berikut :

    ![10.1](images/10.1-Water7.PNG)

-   Edit file `/etc/squid/squid.conf` menjadi seperti gambar berikut :

    ![10.2](images/10.2-Water7.PNG)

-   Restart service squid3 dengan meggunakan perintah :

    ```
    service squid restart
    ```

**Loguetown**

-   Lihat jam saat ini terlebih dahulu, gunakan perintah :

    ```
    date
    ```

    ![10.3](images/10.3-LogueTown.PNG)

-   Pastikan node sudah terhubung menggunakan proxy dengan memasukkan perintah :

    ```
    env | grep -i proxy
    ```

    ![10.4](images/10.4-LogueTown.PNG)

-   Buka alamat `google.com` dengan menggunakan perintah :

    ```
    lynx google.com
    ```

-   Pada kasus ini, halaman website tidak bisa dibuka karena waktunya tidak sesuai dengan aturan yang sudah dibuat sebelumnya.

    ![10.5](images/10.5-LogueTown.PNG)

    _P.S : Proxy tidak meminta autentikasi user, sebab rule evaluationnya dimulai dengan membandingkan waktu saat ini dengan aturan yang ditetapkan_

-   Untuk melihat apakah aturannya berjalan dengan baik, set waktu saat ini dengan perintah :

    ```
    date -s (waktu yang diinginkan)
    ```

    ![10.6](images/10.6-LogueTown.PNG)

-   Setelah waktunya sudah sesuai dengan aturan, akses kembali `google.com` dengan menggunakan perintah :

    ```
    lynx google.com
    ```

-   Ketika tersambung, proxy akan melakukan autentikasi user terlebih dahulu.

    ![10.7](images/10.7-LogueTown.PNG)

-   Jika benar, maka akan terlihat halaman yang diminta sebelumnya (google.com)

    ![10.8](images/10.8-LogueTown.PNG)

## Soal 11

```
Agar transaksi bisa lebih fokus berjalan, maka dilakukan redirect website agar mudah mengingat website transaksi jual beli kapal. Setiap mengakses google.com, akan diredirect menuju super.franky.yyy.com dengan website yang sama pada soal shift modul 2. Web server super.franky.yyy.com berada pada node Skypie
```

### Jawaban

**Skypie**

-   Pertama - tama, update library dari ubuntu dengan perintah `apt-get update`.

-   Install `apache2 dan librarynya` dengan memasukkan perintah `apt-get install apache2 -y` dan `apt-get install libapache2-mod-php7.0 -y`.

-   Jalankan apache yang telah dipasang dengan memasukkan perintah `service apache2 start`.

-   Install `php` dengan memasukkan perintah `apt-get install php -y`.

-   Install tools `wget` dengan memasukkan perintah `apt-get install wget -y`.

-   Install tools `unzip` dengan memasukkan perintah `apt-get install unzip -y`.

-   Setelah semua tools sudah berhasil dipasang, download terlebih dahulu file library web yang telah disediakan dengan perintah :

    ```
    wget https://raw.githubusercontent.com/FeinardSlim/Praktikum-Modul-2-Jarkom/main/super.franky.zip
    ```

-   Copy konfigurasi 000-default web server yang akan digunakan sebagai template konfigurasi web server super.franky.c07.com dengan perintah :

    ```
    cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/super.franky.c07.com.conf
    ```

-   Edit file `/etc/apache2/sites-available/super.franky.c07.com.conf` seperti pada gambar berikut :

    ![11.1](images/11.1.png)

-   Jalankan konfigurasi website yang telah dibuat dengan menjalankan perintah :

    ```
    cd /etc/apache2/sites-available/
    a2ensite super.franky.c07.com.conf
    ```

-   Kemudian unzip file yang telah didownload dan letakkan pada directory `/var/www/`. Setelah itu rename file menjadi `super.franky.c07.com` dengan command berikut :

    ```
    unzip super.franky.zip -d /var/www/
    mv /var/www/super.franky /var/www/super.franky.c07.com
    ```

-   Edit file `/etc/apache2/ports.conf` seperti pada gambar berikut :

    ![11.2](images/11.2.png)

-   Restart service apache dengan perintah :

    ```
    service apache2 restart
    ```

**EniesLobby**

-   Edit file `/etc/bind/named.conf.local` dan tambahkan config berikut :

    ```
    zone "super.franky.c07.com" {
        type master;
        file "/etc/bind/jarkom/super.franky.c07.com";
    };
    ```

    ![11.3](images/11.3.png)

-   Edit file `/etc/bind/jarkom/super.franky.c07.com` seperti pada gambar berikut:

    ![11.4](images/11.4.png)

-   Restart bind9 dengan perintah

    ```
    service bind9 restart
    ```

**Water7**

-   Edit file `/etc/squid/squid.conf` dan tambahkan config berikut :

    ```
    dns_nameservers 192.187.2.2 192.168.122.1

    acl WHEN_ACCESS dstdomain google.com
    deny_info http://super.franky.c07.com:5000 WHEN_ACCESS
    http_reply_access deny WHEN_ACCESS
    ```

    ![11.5](images/11.5.png)

-   Restart service squid dengan perintah :

    ```
    service squid restart
    ```

**Loguetown**

-   Pastikan node sudah terhubung menggunakan proxy dengan memasukkan perintah :

    ```
    env | grep -i proxy
    ```

-   Kemudian buka alamat `google.com` dengan menggunakan perintah :

    ```
    lynx google.com
    ```

-   Masukkan username dan password yang telah diatur pada soal sebelumnya, seperti pada gambar berikut :

    ![11.6](images/11.6.png)

    ![11.7](images/11.7.png)

-   Jika username dan password valid, maka setiap kali kita mengakses URL `google.com` maka kita akan secara otomatis dialihkan ke `super.franky.c07.com` seperti pada gambar berikut :

    ![11.8](images/11.8.png)

## Soal 12

```
Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di super.franky.yyy.com. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar (.png, .jpg), sedangkan Zoro mencari sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps
```

### Jawaban

**Water7**

-   Edit file `/etc/squid/squid.conf` dan tambahkan config berikut :

    ```
    acl LUFFY proxy_auth luffybelikapalc07
    acl ZORO proxy_auth zorobelikapalc07

    acl DOWNLOAD url_regex -i \.jpg$ \.png$

    delay_pools 2
    delay_class 1 1
    delay_parameters 1 -1/-1
    delay_access 1 allow ZORO
    delay_access 1 deny all

    delay_class 2 1
    delay_parameters 2 1250/1250
    delay_access 2 allow LUFFY DOWNLOAD
    delay_access 2 deny all
    ```

    ![12.1](images/12.1.png)

    _P.S : Config diatas bertujuan untuk membatasi bandwidth setiap user, dimana pada soal diminta agas `user luffy` dapat mendownload file (`.png` dan `.jpg`) dengan kecepatan `10 kbps` sedangkan `user zoro` tidak memiliki batas kecepatan (`unlimited`)_

-   Restart service squid3 dengan meggunakan perintah :

    ```
    service squid restart
    ```

**Loguetown - sebagai user luffy**

-   Pastikan node sudah terhubung menggunakan proxy dengan memasukkan perintah :

    ```
    env | grep -i proxy
    ```

-   Kemudian buka alamat `google.com` dengan menggunakan perintah :

    ```
    lynx google.com
    ```

-   Masukkan username dan password untuk user luffy, seperti pada gambar berikut :

    ![12.2](images/12.2.png)

    ![12.3](images/12.3.png)

-   Jika username dan password valid, maka akan dialihkan ke `super.franky.c07.com` seperti pada gambar berikut :

    ![12.4](images/12.4.png)

-   Lakukan download untuk salah satu file `.png` atau `.jpg` seperti pada gambar berikut dan lihat kecepatan downloadnya :

    ![12.5](images/12.5.png)

    ![12.6](images/12.6.png)

    ![12.7](images/12.7.png)

    _P.S : Kecepatan download untuk user luffy telah dibatasi yaitu `10 kbps` dan dapat dilihat dari gambar diatas_

## Soal 13

```
Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya
```

### Jawaban

**Water7**

-   Edit file `/etc/squid/squid.conf` dengan menambahkan config berikut :

    ```
    acl LUFFY proxy_auth luffybelikapalc07
    acl ZORO proxy_auth zorobelikapalc07

    acl DOWNLOAD url_regex -i \.jpg$ \.png$

    delay_pools 2
    delay_class 1 1
    delay_parameters 1 -1/-1
    delay_access 1 allow ZORO
    delay_access 1 deny all

    delay_class 2 1
    delay_parameters 2 1250/1250
    delay_access 2 allow LUFFY DOWNLOAD
    delay_access 2 deny all
    ```

    ![13.1](images/13.1.png)

    _P.S : Config diatas bertujuan untuk membatasi bandwidth setiap user, dimana pada soal diminta agas `user luffy` dapat mendownload file (`.png` dan `.jpg`) dengan kecepatan `10 kbps` sedangkan `user zoro` tidak memiliki batas kecepatan (`unlimited`)_

-   Restart service squid3 dengan meggunakan perintah :

    ```
    service squid restart
    ```

**TottoLand - sebagai user zoro**

-   Pastikan node sudah terhubung menggunakan proxy dengan memasukkan perintah :

    ```
    env | grep -i proxy
    ```

-   Kemudian buka alamat `google.com` dengan menggunakan perintah :

    ```
    lynx google.com
    ```

-   Masukkan username dan password untuk user zoro, seperti pada gambar berikut :

    ![13.2](images/13.2.png)

    ![13.3](images/13.3.png)

-   Jika username dan password valid, maka akan dialihkan ke `super.franky.c07.com` seperti pada gambar berikut :

    ![13.4](images/13.4.png)

-   Lakukan download untuk salah satu file `.png` atau `.jpg` seperti pada gambar berikut dan lihat kecepatan downloadnya :

    ![13.5](images/13.5.png)

    ![13.6](images/13.6.png)

    _P.S : Kecepatan download untuk user zoro tidak dibatasi atau `unlimited` sehingga ia tidak menampilkan kecepatan dowloadnya_
