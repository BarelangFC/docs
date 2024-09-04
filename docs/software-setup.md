# Instalasi Software

## Jetson Xavier NX - Ubuntu 20.04

1. Buka terminal (CTRL + ALT + T)
2. Ketikkan perintah berikut ini di terminal
```bash
sudo apt update && sudo apt upgrade -y
```
3. Install Python3 pada jetson
```bash
sudo apt install python3-pip
```
4. install jtop untuk pengaturan internal jetson
```bash
sudo pip3 install -U jetson-stats
```
5. Reboot jetson 
```bash
sudo reboot
```
6. Buka terminal dengan shortcut ctrl + alt + t
7. Ketikkan perintah berikut ini di terminal
```bash
jtop
```
8. Pergi ke menu control atau ctrl lalu atur putaran kipas menjadi manual dan konfigurasikan kecepatan kipas hingga mencapai maksimal
9. Ketikkan perintah berikut ini di terminal untuk menginstal terminator
```bash
sudo apt update && sudo apt install terminator
```
10. Buka bagian setting pada ubuntu 20.04
11. Masuk ke bagian power dan pastikan mode sleep nonaktif atau mode never sleep
12. Kemudian masuk ke bagian sharing dan pastikan bagian sharing monitor aktif dan tanpa password encription
13. Kemudian masuk ke bagian privacy dan pastikan bagian black screen turn off, nonaktifkan screen lock dan suspend lock, dan turn off automatic screen lock delay
14. Masuk ke bagian user dan pastikan bahwa pengaturan login tidak membutuhkan password
15. Restart device

## Mode lxde
1. Buka terminator ubuntu
2. Ketik perintah berikut ini
```bash
sudo apt install lxde
```
3. Pastikan memilih mode lightdm
4. Restart device
5. Pada saat tampilan memasukkan password, pilih tampilan utama lxde
6. Setelah itu, masuk ke pengaturan xscreensaver di sebelah kiri bawah, pastikan mode screenxsaver berada pada posisi disable

## Konfigurasi Nomachine pada jetson
1. Buka terminator
2. Ketikkan perintah berikut ini
```bash
sudo apt update && sudo apt upgrade
sudo apt install wget
wget https://www.nomachine.com/free/arm/v8/deb -O nomachine.deb
sudo dpkg -i nomachine.deb
```
3. Jika bagian baris terakhir gagal dijalankan, maka masuk ke direktori Downloads dan masukkan command sebelumnya
4. Install nomachine di perangkat pc/laptop anda
5. Jika sudah selesai, matikan device dan pasang ke dalam tubuh robot
6. Jika sudah terinstall di tubuh robot, nyalakan jetson dan sambungkan kabel lan pada laptop/pc ke jetson
7. Buka terminator dan ketik perintah berikut
```bash
sudo nmtui
```
8. Masuk ke bagian edit connection dan konfigurasi pengaturan wired connection menjadi statis dengan ip 192.168.123.xx, nilai xx bergantung pada nomor robot
9. Pastikan anda sudah konfigurasi ip untuk ethernet pada pc/laptop anda. Caranya pergi ke menu Control Panel\Network and Internet\Network and Sharing Centre, lalu klik kanan pada bagian ethernet dan pilih properties, kemudian pilih ipv4 control dan klik properties, dan selanjutnya masukkan ip statis yang memiliki class yang sama dengan ip robot nantinya. Lalu save pengaturan anda
10. Buka nomachine di pc/laptop anda dan masukkan ip robot pada koneksi baru, lalu coba sambungkan. Jika gagal maka ada kesalahan di konfigurasi nmtui pada robot. Ulang lagi step 8
