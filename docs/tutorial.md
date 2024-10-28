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

TODO: Dani

## 4. Tutorial Kalibrasi Odometry

TODO: Choirul
