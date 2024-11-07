# Tutorial Tuning dan Konfigurasi Robot
 
 **Sebelum melakukan tuning motion, harap untuk mencadangkan/backup package Player terlebih dahulu**

  
## 1. Tutorial Tuning Walking

### a. Setup tuning motion

- Posisikan robot seperti sedang duduk dengan posisi HipRoll dan AnkleRoll lurus sejajar.
  
- buka terminal.
  
- masuk ke folder Player.
  
```bash
cd ~/bfc_ros2/src/Player/
./kill.sh
lua run_dcm.lua
```

- Hidupkan OpenCR, tunggu sampai lampu indikator servo menyala.

- Jika lampu indikator servo sudah menyala dan terminal menampilkan angka, maka periksa kabel servo pada ID tersebut.
  
- Jalankan setup tuning

```bash
lua run_setup.lua
```

- Tekan "8" untuk posisi berdiri. Angkat robot untuk membantunya berdiri.

- Jika posisi robot tidak berdiri atau posisi kaki robot miring, segera matikan OpenCR dan periksa kembali pengaturan titik 0 pada servo.

- Jika pergerakan robot tidak lancar ketika berdiri, periksa kembali kabel servo yang tidak tersambung dengan menjalankan perintah:
  
```bash
cd ~/bfc_ros2/src/Player/Lib/
lua test_dynamixel.lua
```

Jika ada angka yang tidak muncul antara 1-20 serta angka 200, maka periksa kembali kabel servo pada ID yang hilang tersebut.

### b. Tuning V

- Masuk ke setup tuning motion, angkat robot atau letakkan di paddock lalu tekan "V" pada terminal.
  
- Periksa servo pada kaki yang miring atau tidak sejajar dengan servo pada kaki sebelahnya.

- Tekan:
  
    "1" / "2" untuk berpindah ke servo sebelumnya atau setelahnya.
    
    "w" / "x" untuk menggerakkan servo pada kaki kanan.
    
    "a" / "d" untuk menggerakkan servo pada kaki kiri.
    
    "s"       untuk mengembalikan posisi servo ke posisi awal.

- Luruskan semua servo kaki yang miring dan sejajarkan dengan kaki sebelahnya.

- Setelah selesai *Tuning V*, tekan "0" untuk menyimpan data yang diubah atau tekan "v" untuk kembali tanpa menyimpan data. **Pastikan robot berada di *Paddock* atau tahan robot tersebut agar tidak terjatuh.**

### c. Tuning Jalan

- Masuk ke setup tuning motion.

- Apabila posisi robot kurang seimbang antara depan dan belakang, tekan "-" untuk condong ke depan atau "=" untuk condong ke belakang.

- Tekan "9" untuk jalan ditempat,

- Tekan:
    
    "i" untuk menambah kecepatan ketika maju.
    
    "," untuk menambah kecepatan ketika mundur.
    
    ":" untuk menambah kecepatan ketika jalan ke samping kanan.
    
    "h" untuk menambah kecepatan ketika jalan ke samping kiri.
    
    "l" untuk menambah kecepatan ketika memutar ke kanan.
    
    "j" untuk menambah kecepatan ketika memutar ke kiri.
    
    "k" untuk mengembalikan semua nilai kecepatan menjadi 0.
    
    "8" untuk berhenti.

- Jika pergerakan robot ketika jalan kurang stabil, anda bisa mengubah nilai parameter yang ada di beberapa file diantaranya:
    
    bfc_ros2/src/Player/run_setup.lua
    
    bfc_ros2/src/Player/Config/Walk/Config_OP_Walk.lua

- Jika sekiranya pergerakan robot ketika jalan sudah stabil, anda dapat menguji coba dengan menjalankan robot dengan jarak 9 meter untuk jalan maju, dan jarak 6 meter untuk jalan samping. Lakukan uji coba tersebut sebanyak 20 kali bolak-balik.

- Tuning jalan dapat dikatakan berhasil apabila:
  
    a. Ketika berdiri, posisi badan robot seimbang.
  
    b. Ketika jalan ditempat, robot tidak berpindah dari posisi awal.

    c. Ketika dilakukan uji coba sebanyak 20 kali bolak-balik, robot berjalan lurus dan tidak terjatuh sekalipun.

    d. Ketika berjalan, robot mampu menahan sedikit tekanan baik dari depan maupun belakang tanpa terjatuh.

- Setelah selesai melakukan tuning tendang, salin program yang ada didalam file bfc_ros2/src/Player/run_setup.lua ke dalam file bfc_ros2/src/Player/walk_server.lua.

## 2. Tutorial Tuning Tendangan

TODO: Dimas

## 3. Tutorial Kalibrasi Kamera

Kalibrasi kamera pada kamera logitech c930 dan kamera eCons see3cam:

- Pastikan device telah terinstall ros2 foxy, usb_cam ros2 foxy rqt, dan image pipeline.
  
![alt text](<images/Screenshot from 2024-10-29 18-46-26.png>)
- Jika anda memiliki device dengan spesifikasi berbeda, maka diperlukan penyesuaian lebih lanjut
- Kemudian anda install package ros2 foxy untuk kalibrasi kamera dengan command
```bash
sudo apt install ros-foxy-camera-calibration
```
- Buka terminal anda, saya sarankan anda menggunakan terminator sebagai terminal anda
- Di terminal anda buat menjadi dua tab, kemudian di tab pertama anda masukkan command
```bash
ros2 run usb_camera usb_camera_node_exe --ros-args --params-file /home/alamat_file_config.yaml 
```
- Di terminal kedua masukkan command
```bash
ros2 run camera_calibration cameracalibrator --size 7x11 --square 0.030 --ros-args -r image:=/image_raw
```
- Perlu diketahui bahwa ukuran chessboard menentukan parameter kalibrasi kamera
- Penetuan ukuran adalah sebagai berikut
![alt text](<images/WhatsApp Image 2024-10-31 at 16.55.23.jpeg>)
Kita harus menghitung sudut kotak hitam dari sisi lebar dan panjang, pada gambar sisi panjang memiliki 11 sudut, sedangkan sudut lebar adalah 7. Untuk ukuran kotak adalah 30 milimeter sehingga penulisan adalah 0.03. Pastikan anda memanggil topic gambar pada kamera.
- Jika sudah berhasil maka tampilannya akan seperti ini
![alt text](<images/Screenshot from 2024-10-29 19-29-37.png>)
- Anda harus mengambil kalibrasi minimal sampai tombol calibrate bisa ditekan
![alt text](<images/Screenshot from 2024-10-29 19-30-51.png>)
- Selanjutnya anda tekan calibrate dan hasilnya bisa anda lihat di terminal kamera kalibrasi
![alt text](<images/Screenshot from 2024-10-29 19-31-21.png>)
- Selanjutnya anda save dengan menekan tobol save di GUI kamera kalibrasi
- Alamat save hasil kalibrasi berada di /tmp/
![alt text](<images/Screenshot from 2024-10-29 19-48-19.png>)
- Folder kamera kalibrasi terdapat foto kalibrasi, file ost.txt, dan file ost.yaml. File yang paling penting adalah file yaml karena berisi parameter kamera hasil kalibrasi
![alt text](<images/Screenshot from 2024-10-29 19-49-42.png>)
- Untuk kamera econs memiliki cara kalibrasi yang persis dengan kalibrasi kamera logitech. Akan tetapi, anda harus membuka image pipeline di terminal yang sama ketika anda sedang membuka usb cam. Hal tersebut terjadi agar usb cam bisa menerapkan konfigurasi hasil kalibrasi yang telah kita lakukan. 

selesai sampai disini

## 4. Tutorial Kalibrasi Odometry

TODO: Choirul
