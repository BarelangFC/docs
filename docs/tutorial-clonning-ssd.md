# Tutorial Clonning SSD

## Berikut cara menggandakan SSD dengan hasil yang identik:

1. Pasang SD card di tempat card reader, posisi di bawah kipas jetson, disitu ada tempat khusus SD card tapi ga semua jetson ada. 
2. Buka terminal jetson, ketik df -h, pastikan SD card terdeteksi, cari aja keterangan penyimpanan yang sesuai dengan size SD card yang dipakai. 
3. Selanjutnya ketik sudo cp -ax / /media/<nama jetson>/<nama SD card>
4. Tunggu sampai selesai.
   
![github](./images/github.png)

5. Jika sudah selesai, buka penyimpanan SD card, lalu cek bagian home folder apakah sudah semua ter copy. Jika belum maka copy manual.
6. Jika sudah semua ter copy ke SD card, buka folder boot yang ada di SD card, lalu buka extlinux, buka terminal di alamat itu, kemudian ketik sudo gedit extlinux.conf.
7. Edit bagian boot supaya bisa booting di SD card, caranya ada di video menit akhir, pastikan nama booting nya sama dengan nama SD card.
8. Jika gagal booting maka anda harus install ulang jetson dan SD card.