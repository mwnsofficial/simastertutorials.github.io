---
layout: post
title: "membuat config mode script OpenClash"
categories: [ script ]
image: assets/images/
---
Untuk membuat config mode script OpenClash, Anda dapat mengikuti langkah-langkah berikut:

1. Siapkan perangkat yang menjalankan OpenClash, seperti router atau sistem operasi seperti OpenWRT atau DD-WRT.

2. Pastikan OpenClash sudah terinstal di perangkat Anda. Jika belum, ikuti panduan instalasi yang disediakan oleh OpenClash.

3. Buka file konfigurasi OpenClash menggunakan editor teks seperti Notepad++ atau Sublime Text.

4. Pilih mode Script pada konfigurasi OpenClash dengan menambahkan baris berikut:

   ```
   mode: script
   ```

5. Selanjutnya, Anda perlu menentukan skrip mode untuk memuat konfigurasi OpenClash.

6. Buat file skrip mode dengan ekstensi .sh, contohnya `openclash_script.sh`.

7. Buka file `openclash_script.sh` menggunakan editor teks dan tambahkan kode berikut:

   ```bash
   #!/bin/sh
   path="/etc/openclash/"
   config_file="/etc/openclash/config.yaml"

   while inotifywait -e modify "$path"; do
       openclash -c "$config_file" -d
   done
   ```

   Kode di atas memeriksa perubahan pada direktori `/etc/openclash/` menggunakan `inotifywait`. Jika ada perubahan, maka proses OpenClash akan dijalankan menggunakan perintah `openclash -c "$config_file" -d`.

8. Simpan file `openclash_script.sh`.

9. Buka terminal atau SSH ke perangkat dan berikan izin eksekusi ke file skrip dengan menjalankan perintah:

   ```bash
   chmod +x openclash_script.sh
   ```

10. Terakhir, ubah file konfigurasi OpenClash untuk mengarahkan pada file skrip mode yang baru saja dibuat dengan menambahkan baris berikut pada file konfigurasi:

    ```
    script_path: /path/to/openclash_script.sh
    ```

11. Simpan perubahan pada file konfigurasi OpenClash.

12. Restart OpenClash untuk memuat konfigurasi mode skrip dengan menjalankan perintah:

    ```bash
    /etc/init.d/openclash restart
    ```

13. Sekarang konfigurasi OpenClash Anda akan menggunakan mode skrip untuk memuat konfigurasi. Setiap kali ada perubahan pada file konfigurasi, OpenClash akan dimuat ulang secara otomatis melalui skrip.

Pastikan untuk mengganti "/etc/openclash/" dan "/path/to/openclash_script.sh" dengan direktori yang sesuai pada perangkat Anda. Juga, pastikan file konfigurasi serta file skrip berada pada direktori yang benar.

Semoga tutorial ini dapat membantu Anda dalam membuat config mode script OpenClash!