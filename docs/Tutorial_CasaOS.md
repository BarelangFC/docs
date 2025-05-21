# Tutorial Install CasaOS Server BFC

## Panduan Instalasi Xubuntu

Dokumen ini memberikan langkah-langkah untuk menginstal Xubuntu, salah satu varian ringan dari Ubuntu yang menggunakan lingkungan desktop XFCE.

## Persyaratan Sistem Minimum

- **CPU:** 1 GHz
- **RAM:** 1 GB (minimal), 2 GB atau lebih disarankan
- **Penyimpanan:** 8 GB (minimal), 20 GB atau lebih disarankan
- **USB Drive:** 4 GB atau lebih untuk media instalasi

## Langkah 1: Unduh ISO Xubuntu

1. Kunjungi situs resmi Xubuntu:  
   [https://xubuntu.org/download](https://xubuntu.org/download)
2. Pilih versi terbaru LTS (Long Term Support) untuk stabilitas jangka panjang.
3. Unduh file `.iso`.

## Langkah 2: Buat USB Bootable

Gunakan salah satu software berikut:

### Windows
- **Rufus**
  1. Unduh dari [https://rufus.ie](https://rufus.ie)
  2. Masukkan USB drive
  3. Pilih ISO Xubuntu yang diunduh
  4. Klik "Start" dan tunggu proses selesai

### Linux
- **Balena Etcher**
  ```bash
  sudo apt install balena-etcher-electron
  ```
  Atau unduh dari [https://www.balena.io/etcher](https://www.balena.io/etcher)

## Langkah 3: Boot dari USB

1. Masukkan USB ke komputer target
2. Nyalakan ulang dan masuk ke BIOS/UEFI (biasanya dengan menekan `F2`, `F12`, `Del`, atau `Esc`)
3. Atur urutan boot agar USB drive berada di urutan pertama
4. Simpan perubahan dan keluar

## Langkah 4: Instalasi Xubuntu

1. Pilih **"Install Xubuntu"** saat menu boot muncul
2. Pilih bahasa dan layout keyboard
3. Pilih opsi instalasi:
   - "Erase disk and install Xubuntu" (untuk instalasi bersih)
   - "Install alongside" (jika ingin dual boot)
4. Atur zona waktu
5. Buat akun pengguna dan password
6. Tunggu hingga proses instalasi selesai
7. Setelah selesai, klik **Restart Now** dan cabut USB saat diminta

## Langkah 5: Pasca Instalasi (Opsional)

### Update sistem
```bash
sudo apt update && sudo apt upgrade -y
```

### Instal software tambahan
```bash
sudo apt install git curl build-essential gnome-software
```

---

## Troubleshooting

- Jika instalasi gagal, pastikan:
  - ISO tidak korup (verifikasi checksum)
  - USB tidak bermasalah
  - RAM dan penyimpanan cukup
- Coba boot dengan mode **"safe graphics"** jika tampilan bermasalah

---

## Panduan Instalasi CasaOS

**CasaOS** adalah sistem operasi berbasis web untuk pengelolaan server rumah (home server) yang ringan, open-source, dan mudah digunakan. Cocok dijalankan di perangkat seperti Raspberry Pi, mini PC, atau server lama.

## Persyaratan Sistem

- **OS:** Ubuntu/Debian (direkomendasikan Ubuntu 20.04+ atau Debian 11+) _*note: Kita menggunakan Xubuntu_
- **CPU:** 64-bit (x86_64 atau ARM64)
- **RAM:** Minimal 2 GB
- **Storage:** Minimal 16 GB ruang kosong
- **Akses:** Internet dan hak akses root/sudo

## Langkah 1: Update Sistem

```bash
sudo apt update && sudo apt upgrade -y
```

## Langkah 2: Instalasi CasaOS

Jalankan perintah berikut:

```bash
curl -fsSL https://get.casaos.io | sudo bash
```

Skrip ini akan:
- Menginstal dependensi
- Menyiapkan Docker & Docker Compose
- Menjalankan layanan CasaOS

## Langkah 3: Akses Web UI

1. Setelah instalasi selesai, buka browser
2. Akses alamat IP lokal perangkat Anda, contoh:
   ```
   http://localhost/
   ```
3. Ikuti wizard pengaturan awal

## Langkah 4: Pengelolaan Aplikasi

CasaOS menyediakan antarmuka web untuk:
- Menambah/menghapus aplikasi berbasis Docker
- Menyimpan data (file manager, Samba share, dll)
- Memantau performa sistem

## Langkah 5: Instal Aplikasi Tambahan

Buka tab **App Store** di UI CasaOS dan instal aplikasi populer seperti:
- Cloudflared _#ini untuk publish server_
- FileBrowser _#ini untuk akses file via browser_
- ttydBridge _#ini untuk akses terminal via browser_

## Uninstall CasaOS (Opsional)

```bash
sudo /opt/casaos/uninstall.sh
```

## Troubleshooting

- Pastikan port **80** tidak digunakan aplikasi lain
- Gunakan `docker ps` untuk mengecek kontainer berjalan
- Cek log CasaOS:
  ```bash
  journalctl -u casaos -f
  ```


## Panduan Instalasi Screen

**Screen** adalah utilitas terminal yang memungkinkan pengguna untuk menjalankan sesi shell terpisah dan mengelola banyak jendela dalam satu jendela terminal. Ini sangat berguna untuk menjalankan aplikasi di latar belakang dan menjaga aplikasi aktif meskipun sesi SSH terputus.

## Persyaratan Sistem

- **OS:** Ubuntu/Debian (direkomendasikan Ubuntu 20.04+ atau Debian 11+) _*note: Kita menggunakan Xubuntu_
- **Akses:** Internet dan hak akses root/sudo

## Langkah 1: Update Sistem

Pertama, pastikan sistem Anda diperbarui:

```bash
sudo apt update && sudo apt upgrade -y
```

## Langkah 2: Instalasi Screen

Jalankan perintah berikut untuk menginstal **screen**:

```bash
sudo apt install -y screen
```

### Menyimpan dan Menutup Sesi

Untuk menutup sesi **screen**, Anda dapat keluar dengan menggunakan kombinasi tombol:

- Tekan `Ctrl + A`, lalu `D` untuk melepaskan sesi (detach).
  
## Melihat Sesi Screen yang Aktif

Untuk melihat daftar sesi **screen** yang sedang berlangsung, gunakan perintah:

```bash
screen -ls
```

### Mengembalikan Sesi Screen

Untuk kembali ke sesi **screen** yang sudah ada, gunakan perintah:

```bash
screen -r <ID_Sesi>/<Nama_Sesi>
```

Ganti `<ID_Sesi>` dengan ID sesi yang ingin Anda kembalikan.

## Mengakhiri Sesi Screen

Saat Anda dalam sesi **screen**, Anda dapat menutup jendela dengan mengetik:

```bash
exit
```

Jika Anda ingin mengakhiri semua sesi **screen**, cukup ketik perintah ini pada setiap sesi yang sedang berjalan.

## Kombinasi Tombol Penting

| Kombinasi         | Fungsi                               |
|--------------------|--------------------------------------|
| `Ctrl + A`, `D`    | Detach dari sesi                    |
| `Ctrl + A`, `C`    | Buat jendela baru                   |
| `Ctrl + A`, `N`    | Pindah ke jendela berikut           |
| `Ctrl + A`, `P`    | Pindah ke jendela sebelumnya         |
| `Ctrl + A`, `K`    | Tutup jendela saat ini              |

## Troubleshooting

- Jika Anda tidak dapat menemukan sesi **screen**, pastikan sesi tersebut belum terputus. Gunakan `screen -ls` untuk memeriksa sesi aktif.
- Jika **screen** tidak terinstal, pastikan Anda menggunakan perintah instalasi dengan sudo untuk memiliki hak akses yang diperlukan.


## Panduan Instalasi noVNC Menggunakan x11vnc

**noVNC** adalah solusi VNC yang berbasis web yang memungkinkan akses jarak jauh ke desktop Linux Anda melalui browser. Dalam panduan ini, kita akan menggunakan **x11vnc** sebagai server VNC.

## Persyaratan Sistem

- **OS:** Ubuntu/Debian (direkomendasikan Ubuntu 20.04+ atau Debian 11+) _*note: Kita menggunakan Xubuntu_
- **CPU:** 64-bit (x86_64 atau ARM64)
- **RAM:** Minimal 1 GB
- **Storage:** Minimal 1 GB ruang kosong
- **Akses:** Internet dan hak akses root/sudo

## Langkah 1: Update Sistem

Pertama, pastikan sistem Anda diperbarui:

```bash
sudo apt update && sudo apt upgrade -y
```

## Langkah 2: Instalasi x11vnc dan noVNC

Jalankan perintah berikut untuk menginstal x11vnc dan noVNC:

```bash
sudo apt install -y x11vnc novnc
```

## Langkah 3: Konfigurasi x11vnc

1. **Setel Password untuk Akses VNC:**

   Buat password untuk akses VNC:

   ```bash
   x11vnc -storepasswd
   ```

   Ikuti instruksi untuk menyimpan password di `~/.vnc/passwd`.

2. **Jalankan x11vnc:**
   Buat screen baru dengan cara:
   ```bash
   screen -S vnc
   ```

   Jalankan x11vnc dengan perintah berikut menggunakan opsi yang sesuai:

   ```bash
   x11vnc -usepw -forever -display :0 -auth /home/adminn/.Xauthority
   ```
   atau
    ```bash
   x11vnc -usepw -forever -display :0 -auth guess
   ```

   Keluar dari screen
   - Tekan `Ctrl + A`, lalu `D` untuk melepaskan sesi (detach).

   Keterangan:
   - `-display :0` menandakan display X yang digunakan.
   - `-usepw` akan meminta password yang telah Anda atur sebelumnya.
   - `-forever` agar server tetap berjalan meskipun klien terputus.
   - `-display :0` untuk menampilkan display yang pertama.
   - `-auth /home/adminn/.Xauthority` untuk mengakses sistem dengan otoritas adminn.
   - `-auth guess` untuk mengakses sistem dengan mode tamu.

## Langkah 4: Akses noVNC

1. Setelah x11vnc berjalan, lakukan hal ini:
   Buat screen baru dengan cara:
   ```bash
   screen -S vnc1
   ```

   Kemudian jalankan perintah berikut:
   ```bash
   /usr/share/novnc/utils/novnc_proxy --vnc localhost:5900
   ```

   Pastikan Anda mengganti `localhost:5900` sesuai dengan alamat VNC yang Anda gunakan.

2. Buka browser dan akses noVNC:

   ```
   http://localhost:6080/vnc.html
   ```

3. Masukkan password yang telah Anda buat untuk mengakses desktop.

## Troubleshooting

- Pastikan x11vnc berjalan dengan benar tanpa kesalahan.
- Periksa apakah port **5900** digunakan oleh x11vnc:
  ```bash
  netstat -tuln | grep 5900
  ```
- Jika tidak dapat mengakses, pastikan firewall Anda tidak memblokir port yang diperlukan.


# Panduan Setup Cloudflare Tunnel Menggunakan CasaOS

**Cloudflare Tunnel** (sebelumnya dikenal sebagai Argo Tunnel) memungkinkan Anda untuk menghubungkan aplikasi Anda ke Cloudflare secara aman tanpa memerlukan alamat IP publik. Panduan ini menjelaskan cara melakukan setup Cloudflare Tunnel menggunakan **CasaOS**.

## Persyaratan

- **Akun Cloudflare:** Pastikan Anda memiliki akun Cloudflare dan domain yang sudah dikonfigurasi. 
- **CasaOS:** Pastikan Anda telah menginstal CasaOS di server Anda.

## Langkah 1: Masuk ke Dashboard Cloudflare

1. Buka [Dashboard Cloudflare](https://dash.cloudflare.com/).
2. Masuk menggunakan kredensial akun Anda.

## Langkah 2: Pilih Domain

1. Di dashboard, pilih domain yang ingin Anda gunakan untuk setup Cloudflare Tunnel.
2. Anda akan diarahkan ke halaman pengaturan domain.

## Langkah 3: Akses Cloudflare Tunnel

1. Pada menu sebelah kiri, cari opsi **"Access"**.
2. Di dalam sub-menu, klik pada **"Tunnels"**.

## Langkah 4: Buat Tunnel Baru

1. Klik tombol **"Create a Tunnel"**.
2. Berikan nama untuk tunnel Anda, misalnya “MyAppTunnel”. _*note: Kita menggunakan nama **server**_
3. Klik tombol **"Create"** untuk melanjutkan.

## Langkah 5: Salin Token dan Jalankan Cloudflare Tunnel di CasaOS

1. **Salin Token Tunnel:** Setelah tunnel dibuat, Anda akan diberikan token tunnel di dashboard Cloudflare. Token ini akan terlihat seperti ini:

   ```
   eyJ...your_tunnel_token_here...XYZ
   ```

2. **Buka CasaOS:** Masuk ke antarmuka web CasaOS Anda, kemudian buka cloudflare.

3. **Paste token dari cloudflare**

## Langkah 6: Konfigurasi Hostname Tunnel

1. Kembali ke dashboard Cloudflare dan buka tab **"Hostname"** untuk tunnel yang baru saja Anda buat.
2. Klik **"Add a Hostname"**.
3. Masukkan subdomain yang ingin Anda gunakan website yang ingin dipublish, contoh: `server`. _*note: Sesuaikan dengan kebutuhan Anda, dikarenakan untuk website publish CasaOSnya, kita menggunakan subdomain server._
4. Pilih domain yang sebelumnya didaftarkan.
5. Pilih type HTTP. _*note: Sesuaikan dengan kebutuhan Anda, dikarenakan untuk website kita menggunakan HTTP._
6. Masukkan URL dari website yang ingin dipublish, dikarenakan kita mempublish CasaOS masukkan URL: localhost. _*Sesuaikan dengan kebutuhan_
7. Klik **"Save"** untuk menyimpan pengaturan.

## Langkah 7: Uji Tunnel

1. Buka browser Anda dan masukkan domain Anda. _*note : Tambahkan subdomain yang disetting pada hostname, contoh: `server.domain.com`._
2. Anda harus dapat mengakses aplikasi yang terhubung melalui Cloudflare Tunnel.

## Troubleshooting

- **Jika Tunnel Tidak Terhubung:** Pastikan token yang diinput pada cloudflare CasaOS benar.

- **Firewall:** Pastikan firewall tidak menghalangi koneksi yang diperlukan untuk Cloudflare Tunnel.

## Referensi

- [Tutorial youtube yang digunakan sebagai referensi](https://www.youtube.com/watch?v=4YSBZq3NTLQ)
- [Tutorial youtube yang digunakan sebagai referensi](https://www.youtube.com/watch?v=92Hspsqs6MI&t=279s&pp=0gcJCY0JAYcqIYzv)
