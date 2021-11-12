# Jarkom-Modul-3-C07-2021

Kelompok C07

|      NRP       |                  Nama                   |
| :------------: | :-------------------------------------: |
| 05111940000046 |       Titian Pamungkas Anjasmara        |
| 05111940000134 |           Ahmad Lamaul Farid            |
| 05111940000150 | Jonathan Leonardo Hasiholan Simanjuntak |

## Soal 1

```

```

### Jawaban

## Soal 2

```

```

### Jawaban

## Soal 3

```

```

### Jawaban

## Soal 4

```

```

### Jawaban

## Soal 5

```

```

### Jawaban

## Soal 6

```

```

### Jawaban

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

-   Buat folder `super.franky.c07.com` di direktori `/var/www/` dengan perintah :

    ```
    mkdir /var/www/super.franky.c07.com
    ```

-   Unzip file library web yang sebelumnya telah di download ke folder yang telah dibuat dengan perintah :

    ```
    unzip -j super.franky.zip -d /var/www/super.franky.c07.com
    ```

-   Jalankan konfigurasi website yang telah dibuat dengan menjalankan perintah :

    ```
    cd /etc/apache2/sites-available/
    a2ensite super.franky.c07.com.conf
    ```

-   Edit file `/etc/apache2/ports.conf` seperti pada gambar berikut :

    ![11.2](images/11.2.png)

-   Restart service apache dengan perintah :

    ```
    service apache2 restart
    ```

**Water7**

-   Edit file `/etc/squid/squid.conf` seperti pada gambar berikut :

    ![11.3](images/11.3.png)

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

    ![11.4](images/11.4.png)

-   Jika username dan password valid, maka setiap kali kita mengakses URL `google.com` maka kita akan secara otomatis dialihkan ke `super.franky.c07.com` seperti pada gambar berikut :

    ![11.5](images/11.5.png)

## Soal 12

```
Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di super.franky.yyy.com. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar (.png, .jpg), sedangkan Zoro mencari sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps
```

### Jawaban

## Soal 13

```
Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya
```

### Jawaban
