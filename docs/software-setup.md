# Instalasi Software

## Jetson Xavier NX - Ubuntu 20.04

### 1. Instalasi dependencies package

Update system sebelum melakukan install package dan dependencies

```bash
sudo apt update && sudo apt upgrade -y
```

Install Python PIP

```bash
sudo apt install python3-pip
```

Install jtop untuk pengaturan internal jetson

```bash
sudo pip3 install -U jetson-stats
```

Reboot jetson 

```bash
sudo reboot
```

**Setting Fan Speed Jetson**

```bash
jtop
```

Buka menu control atau ctrl lalu atur putaran kipas menjadi manual dan konfigurasikan kecepatan kipas hingga mencapai maksimal

Terminator

```bash
sudo apt update && sudo apt install terminator
```

**Konfigurasi di Jetson**

1. Buka bagian setting pada ubuntu 20.04
2. Masuk ke bagian power dan pastikan mode sleep nonaktif atau mode never sleep
3. Kemudian masuk ke bagian sharing dan pastikan bagian sharing monitor aktif dan tanpa password encription
4. Kemudian masuk ke bagian privacy dan pastikan bagian black screen turn off, nonaktifkan screen lock dan suspend lock, dan turn off automatic screen lock delay
5. Masuk ke bagian user dan pastikan bahwa pengaturan login tidak membutuhkan password
6. Restart device

### 2. Setup LXDE Desktop Environment

```bash
sudo apt install lxde
```

* Pastikan memilih mode lightdm
* Restart device
* Pada saat tampilan memasukkan password, pilih tampilan utama lxde
* Setelah itu, masuk ke pengaturan xscreensaver di sebelah kiri bawah, pastikan mode screenxsaver berada pada posisi disable

### 3. Konfigurasi NoMachine pada Jetson

Install No Machine

```bash
sudo apt update && sudo apt upgrade
sudo apt install wget
wget https://www.nomachine.com/free/arm/v8/deb -O nomachine.deb
sudo dpkg -i nomachine.deb
```

* Jika bagian baris terakhir gagal dijalankan, maka masuk ke direktori Downloads dan masukkan command sebelumnya
* Install nomachine di perangkat pc/laptop anda
* Jika sudah selesai, matikan device dan pasang ke dalam tubuh robot
* Jika sudah terinstall di tubuh robot, nyalakan jetson dan sambungkan kabel lan pada laptop/pc ke jetson
* Buka terminator dan ketik perintah berikut

Pengaturan WiFi

```bash
sudo nmtui
```

* Masuk ke bagian edit connection dan konfigurasi pengaturan wired connection menjadi statis dengan ip 192.168.123.xx, nilai xx bergantung pada nomor robot
* Pastikan anda sudah konfigurasi ip untuk ethernet pada pc/laptop anda. Caranya pergi ke menu Control Panel\Network and Internet\Network and Sharing Centre, lalu klik kanan pada bagian ethernet dan pilih properties, kemudian pilih ipv4 control dan klik properties, dan selanjutnya masukkan ip statis yang memiliki class yang sama dengan ip robot nantinya. Lalu save pengaturan anda
* Buka nomachine di pc/laptop anda dan masukkan ip robot pada koneksi baru, lalu coba sambungkan. Jika gagal maka ada kesalahan di konfigurasi nmtui pada robot. Ulang lagi step 8

### 3. Setup Driver Video

```bash
sudo apt update && sudo apt upgrade
sudo apt install nano
sudo apt-get install xserver-xorg-core
sudo apt-get install xserver-xorg-video-dummy
sudo apt-get install --reinstall xserver-xorg-input-all
sudo nano /usr/share/X11/xorg.conf.d/xorg.conf
```

Masukkan baris program berikut

```bash
Section "Module"
        
    Disable     "dri"
        SubSection  "extmod"
            Option  "omit xfree86-dga"
        EndSubSection
    EndSection

    Section "Device"
        Identifier  "Tegra0"
        Driver      "nvidia"
        Option      "AllowEmptyInitialConfiguration" "true"
    EndSection

    Section "Monitor"
       Identifier "DSI-0"
       Option    "Ignore"
    EndSection

    Section "Screen"
       Identifier    "Default Screen"
       Monitor        "Configured Monitor"
       Device        "Default Device"
       SubSection "Display"
           Depth    24
           Virtual 1280 720 #optional resolution
       EndSubSection
    EndSection
```

Restart Jetson

### 4. Install Dependencies & Library

Install Packages

```bash
sudo apt-get install libncurses5-dev screen
sudo apt-get install build-essential wget subversion cmake swig libreadline6-dev g++ lua5.1
```

Install Boost

```bash
sudo apt update
mkdir BarelangFc_Library && cd BarelangFc_Library
wget https://archives.boost.io/release/1.85.0/source/boost_1_85_0.tar.gz
tar -xvf boost_1_85_0.tar.gz
sudo mv boost_1_85_0 /usr/local/
cd /usr/local/include
sudo ln -s /usr/local/boost_1_47_0/boost boost 
cd –
```

Jika instalasi memiliki waktu tidak lebih dari 3 menit, maka dipastikan proses penginstalan anda telah gagal.

Jika gagal maka download secara manual file boost [disini](https://drive.google.com/drive/folders/1mASY3kszQpr9RsSgJzbuhznYQetVOChP?usp=sharing)

Hapus folder boost yang ada di /usr/local dan pindahkan secara manual folder boost

Install Lua

```bash
cd BarelangFc_Library
wget http://www.lua.org/ftp/lua-5.1.4.tar.gz
tar -xvf lua-5.1.4.tar.gz
cd lua-5.1.4
make clean
make linux
sudo make install
cd ..
sudo apt install git
sudo apt install luarocks
sudo luarocks install luasocket
```

Install Uppenalizers-framework

```bash
cd BarelangFc_Library
git clone https://github.com/BarelangFC/BarelangFC-Setup.git
sudo apt-get install unzip
unzip UPennalizers-master.zip
cd UPennalizers-master
cd Lib
make clean
make setup_op
sudo rm /lib/udev/rules.d/95-upower-wup.rules
```

### 5. Konfigurasi Persistance USB

**Catatan** : Pada bagian ini, semua sub-pengendali robot harus aktif dan harus terhubung ke komputer.

Identifikasi serial sub-pengontrol untuk setiap ttyUSB0 dan ttyUSB1:

```bash
udevadm info -a -n /dev/ttyUSB0 | grep '{serial}' | head -n1
udevadm info -a -n /dev/ttyUSB1 | grep '{serial}' | head -n1
cd /etc/udev/rules.d
sudo nano BarelangFC.rules
```

Tambahkan kode berikut ini:

```bash
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", ATTRS{serial}=="AH03PJVL", SYMLINK+="CM730" // all value is unique

SUBSYSTEM=="tty", ATTRS{serial}=="0000:00:14.0", SYMLINK+="strategyUSB" // all value is unique
```

```bash
sudo usermod -a -G dialout $USER
reboot
```

### 6. Konfigurasi Latency Timer

```bash
sudo su
cd /etc/udev/rules.d
touch BFCLatency.rules
echo ACTION==\"add\", SUBSYSTEM==\"usb-serial\", DRIVER==\"ftdi_sio\", ATTR{latency_timer}=\"1\" > BFCLatency.rules
sudo udevadm control --reload-rules
sudo udevadm trigger --action=add
```

### 7. Setting Port UART Jetson

```bash
git clone https://github.com/JetsonHacksNano/UARTDemo
cd UARTDemo
systemctl stop nvgetty
systemctl disable nvgetty
udevadm trigger
sudo reboot or sudo shutdown -P now
```

```bash
sudo apt-get install python3-serial
```

### 8. Setting CPU Isolation

```bash
sudo nano /boot/extlinux/extlinux.conf
```

Lalu isi bagian yang sesuai dengan lingkaran di gambar

![alt text](./images/isolate-cpu.jpg)

Selanjutnya, reboot jetson

Menjalankan program dengan prioritas CPU tertentu

```bash
taskset -c <core> program
```

**Contohnya**

```bash
taskset -c 0,1,2,3,4 ros2 run groot Groot
```

### 9. Install libzmq, zmqpp, dan libsodium

```bash
wget https://download.libsodium.org/libsodium/releases/libsodium-1.0.18-stable.tar.gz
tar -xvzf libsodium-1.0.18-stable.tar.gz
cd libsodium-stable/
./configure 
make && make check
sudo make install
sudo ldconfig
cd
```

Jika ada terjadi error di awal, pindahkan terlebih dahulu file libsodium dari folder Downloads ke folder home

Buka terminal dan masukkan perintah berikut

```bash
git clone https://github.com/zeromq/libzmq
cd libzmq/
./autogen.sh && ./configure && make -j 4
sudo make check && sudo make install && sudo ldconfig
./autogen.sh ./configure -with-libsodium && sudo make
sudo make install
sudo ldconfig
cd
```

```bash
git clone https://github.com/zeromq/zmqpp.git
cd zmqpp/
sudo make
sudo make check
sudo make install
sudo make installcheck
cd
```

### 10. Install ROS2 Foxy dan Colcon

Untuk instalasi ROS2 Foxy silahkan merujuk ke [web](https://docs.ros.org/en/foxy/Installation/Ubuntu-Install-Debians.html)

Untuk instalasi colcon silahkan ke [web](https://docs.ros.org/en/foxy/Tutorials/Beginner-Client-Libraries/Colcon-Tutorial.html)

Instalasi ROS2 package usb_cam

```bash
Sudo apt install ros-foxy-usb-cam
```

Install library Adafruit-SSD1306

```bash
pip install Adafruit-SSD1306
```

Install image_pipeline

```bash
Sudo apt install ros-foxy-image-pipeline
```

### 11. Install BehaviorTreeV3_CPP dan Groot

```bash
sudo apt-get install libzmq3-dev libboost-dev
sudo apt-get install ros-foxy-behaviortree-cpp-v3
git clone --branch v3.8 https://github.com/BehaviorTree/BehaviorTree.CPP.git
cd BehaviorTree.CPP
mkdir build; cd build
cmake ..
make
sudo make install
```

Untuk menginstall groot, buka terminal dan masukkan perintah berikut

```bash
sudo apt install qtbase5-dev libqt5svg5-dev libzmq3-dev libdw-dev
git clone --recurse-submodules https://github.com/BehaviorTree/Groot.git
cd Groot
cmake -S . -B build
cmake --build build
```

Masukkan dua folder ini ke workspace ROS2 anda dan compile dengan colcon build