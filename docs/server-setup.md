# Server Setup

Dokumentasi terkait instalasi software pada komputer server.

## 1. Instalasi Ubuntu

TODO: Zaky
NOTES: Lengkap dengan dokumentasi gambar

## 2. Instalasi CUDA dan NVIDIA Toolkit

TODO: Zaky

## 3. Instalasi Darknet

TODO: Zaky

## 4. Instalasi CVAT

TODO: Zaky

## 5. Instalasi HALCON Software
Buka browser pilihan anda, disarankan untuk memakai browser chrome agar lebih mudah. Lalu pergi ke link instalasi [halcon](https://www.mvtec.com/downloads).
Anda akan menemukan tampilan seperti di bawah ini.

![alt text](images/1.png)

Anda perlu mengklik bagian *download halcon*. Akan tetapi, anda juga perlu menginstall *deep learning tool* jika ingin menganotasi gambar di *halcon software*. 
Setelah itu anda perlu login akun ke dalam web Halcon. Jika anda tidak memilikinya, maka anda bisa registrasi terlebih dahul. Mohon pastikan bahwa akun email yang akan anda pakai adalah akun resmi suatu lembaga atau perusahaan, bukan mili pribadi.

![alt text](images/2.png)

Selanjutnya anda perlu memilih jenis platform dan versi halcon yang diinginkan. Pilihlah sesuai device yang sedang atau akan anda gunakan.

![alt text](<images/Screenshot from 2024-10-29 10-01-50.png>)
Jika anda sudah mendownload halcon, maka anda bisa mencari berkas file nya di direktori downloads. 

![alt text](<images/Screenshot from 2024-10-29 10-03-48.png>)
Anda ekstrak berkas tersebut dan masuk kedalam foldernya.

![alt text](<images/Screenshot from 2024-10-29 10-04-10.png>)
Kemudian anda buka terminal anda jika anda berada di linux, lalu ketikkan perintah seperti gambar di bawah ini.

![alt text](<images/Screenshot from 2024-10-29 10-04-32.png>)

Jika anda berada di windows atau MacOS, maka anda perlu membuka aplikasi SOM.

Tampilan dari som akan membuka browser pilihan secara otomatis.

![alt text](<images/Screenshot from 2024-10-29 10-06-14.png>)

Kemudian, tekan tanda titik tiga sebelah atas kanan, lalu pilih manage packages. Lalu pilih ALL.

![alt text](<images/Screenshot from 2024-10-29 10-06-33.png>)

Jika sudah, maka tekan apply dan file akan terinstall di device anda. Folder utama berada di direktori home.

![alt text](<images/Screenshot from 2024-10-29 10-07-25.png>)

Untuk menjalankan software halcon, anda harus memiliki file licensi yang terdapat di direktori ./license pada folder halcon. Jika sudah anda bisa menjalankan software halcon lewat terminal dengan perintah ./hdevelop.

![alt text](<images/Screenshot from 2024-10-29 10-08-48.png>)

Tampilan jendela dari halcon software akan seperti ini.

![alt text](<images/Screenshot from 2024-10-29 10-09-04.png>)

Jangan lupa anda berikan pengaturan environtment pada .bashrc jika anda menjalankan aplikasi ini di linux.

![alt text](<images/Screenshot from 2024-10-29 10-12-34.png>)

Untuk penggunaan di embedded system, halcon tidak bisa dijalankan dengan perintah ./hdevelop, melainkan harus dijalankan dengan perintah ./hrun alamat file serta file. Sebagai contoh ada di gambar berikut.

![alt text](<images/Screenshot from 2024-10-29 10-11-02.png>)

Untuk manual book bisa diliat di link [ini](https://drive.google.com/drive/folders/1u7xizRHurcoYx97DMh4Sz7V3gZ5-cOQv?usp=sharing).

## 6. Instalasi Software untuk Training SSD

### 1. Instalasi Anaconda dan Membuat Virtual Environment
#### Instalasi pada Linux
Ketikkan perintah berikut pada terminal
```bash
sudo apt update && sudo apt upgrade -y
wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh
chmod +x Anaconda3-2020.11-Linux-x86_64.sh
./Anaconda3-2020.07-Linux-x86_64.sh
```
Lakukan proses instalasi diatas dengan pilihan default. Setelah proses instalasi selesai lakukan eksekusi terhadap file `~/.bashrc`dengan mengetikkan perintah berikut ini.
```bash
source ~/.bashrc
```
Setelah mengeksekusi perintah tersebut, di terminal akan muncul environment default `base` yang sedang digunakan seperti berikut.
```bash
(base) username@machine-name:~$
```
#### Membuat Virtual Environment
Membuat virtual environment dapat dilakukan dengan dua cara:

1. Menggunakan `anaconda-navigator`
2. Menggunakan terminal
Jika menggunakan terminal, format perintah yang digunakan sebagai berikut.
```bash
conda create -n envname python=x.x anaconda
```
Contoh: membuat virtual environment dengan nama `ssdmobile` dan menggunakan Python versi 3.7.x.
```bash
conda create -n ssdmobile python=3.7 anaconda
```
#### Mengaktifkan Virtual Environment
Setelah membuat virtual environment, aktifkan virtual environment yang ingin digunakan dengan format perintah sebagai berikut.
```bash
conda activate envname
```
Contoh: mengaktifkan virtual environment `ssdmobile` yang telah dibuat.
```bash
conda activate ssdmobile
```
Sekarang di terminal akan muncul nama environment yang aktif `ssdmobile` seperti berikut ini.
```bash
(ssdmobile) username@machine-name:~$
```
### 2. Install Tensorflow
Tensorflow yang digunakan pada ssdmobile adalah tensorflow 1.15.

mengintall tensorflow run di CPU.
```bash
pip intall tensorflow==1.15
```
mengintal tensorflow run GPU.
```bash
pip install tensorflow-gpu==1.15
```
### 3.  Instal Object Detection API
Install tf_slim.
```bash
pip install tf_slim
```
Membuat direktori penyimpanan file.
```bash
mkdir content && cd content -y
mkdir models && cd models -y
```
Install protobuf-compiler and the tensorflow's Object Detection API.
```bash
apt-get install protobuf-compiler
git clone https://github.com/tensorflow/models.git
cd research
```
Compile all the protobuf dependencies.
```bash
protoc object_detection/protos/*.proto --python_out=.
```
Set up and install the object detection API.
```bash
cp object_detection/packages/tf1/setup.py .
python3 -m pip install .
```
Run a test to make sure setup is correct.
```bash
python3 object_detection/builders/model_builder_test.py
```
### 4. Unduh dan persiapkan kumpulan data.
Download dataset training
```bash
# Now let's download our training dataset.
mkdir /content/dataset
cd /content/dataset
wget http://www.robots.ox.ac.uk/~vgg/data/pets/data/images.tar.gz
wget http://www.robots.ox.ac.uk/~vgg/data/pets/data/annotations.tar.gz
!tar zxf images.tar.gz
!tar zxf annotations.tar.gz

# Only picking Abyssinian Cat and the American Bulldog
# If you wish to train the model on all classes, simply skip this entire cell.
cp /content/dataset/annotations/list.txt /content/dataset/annotations/list_petsdataset.txt
cp /content/dataset/annotations/trainval.txt /content/dataset/annotations/trainval_petsdataset.txt
cp /content/dataset/annotations/test.txt /content/dataset/annotations/test_petsdataset.txt
grep "Abyssinian" /content/dataset/annotations/list_petsdataset.txt >  /content/dataset/annotations/list.txt
grep "american_bulldog" /content/dataset/annotations/list_petsdataset.txt >> /content/dataset/annotations/list.txt
grep "Abyssinian" /content/dataset/annotations/trainval_petsdataset.txt > /content/dataset/annotations/trainval.txt
grep "american_bulldog" /content/dataset/annotations/trainval_petsdataset.txt >> /content/dataset/annotations/trainval.txt
grep "Abyssinian" /content/dataset/annotations/test_petsdataset.txt > /content/dataset/annotations/test.txt
grep "american_bulldog" /content/dataset/annotations/test_petsdataset.txt >> /content/dataset/annotations/test.txt
```

## 5. Setup Remote Access over Internet (RDP dan SSH)

TODO: Zaky