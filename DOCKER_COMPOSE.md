# Bekerja menggunakan docker compose

### Buat folder project

- Buat folder project, contoh: `docker_test`
- Gunakan `cmd`, `PowerShell`, `terminal` atau sejenisnya
- Masuk ke folder `docker_test` yang dibuat sebelumnya

> C:\\...\docker_test>

---

### Buat file docker compose

- Diadalam folder `docker_test` buat file `.yml` dengan nama: `docker-compose.yml`

> C:\\...\docker_test\docker-compose.yml

- Membuat service redis pada file `docker-compose.yml`

```
services:
  redis_ekos:
    image: redis:alpine
    container_name: exaudie_redis_cont
    ports:
      - "6389:6379"
    restart: unless-stopped
    volumes:
      - exaudie_vol:/data_data
    networks:
      - exaudie_net

networks:
  exaudie_net:

volumes:
  exaudie_vol:
    driver: local

```

Note:

- `ports: - "6389:6379"` :
  - port `6379` adalah port container
  - port `6389` adalah port mesin docker yang diekspos keluar
- `restart: unless-stopped` adalah aturan (policy) yang menginstruksikan docker untuk selalu menyalakan kembali container secara otomatis, kecuali jika Anda secara sengaja menghentikannya

---

### Menjalankan docker compose

Sebelum menjalankan docker compose, pastikan posisi kita berada di folder dimana file `docker-compose.yml` disimpan, contoh disini adalah folder `docker_test`

> C:\\...\docker_test><br>

Jalankan perintah berikut

> \> docker compose up <br>

Jalankan perintah berikut jika ingin menjalankan di background

> \> docker compose up -d <br>

Jika ingin menjalankan dengan memilih file mana yang ingin dijalankan maka tambahkan opsi `-f <path file>` seperti berikut

> \> docker compose -f docker-compose-redis.yml up -d <br>
> \> docker compose -f redis/docker-compose.yml up -d

---

### Menghentikan docker compose

Untuk mengkhentikan container docker compose dan sekaligus menghapus container, jalankan perintah

> \> docker compose -f <path_file_docker_compose> down

contoh:

> \> docker compose -f redis/docker-compose.yml down

Jika ingin sekaligus menghapus volumes tambahkan opts `-v`

> \> docker compose -f redis/docker-compose.yml down -v

---

### Masuk ke Redis

Untuk masuk ke redis yang berjalan di docker menggunakan `redis-cli` yang terinstal di container gunakan perintah berikut:

> \> docker exec -it <nama_container> redis-cli<br>

contoh:

> \> docker exec -it redis_exaudie_container redis-cli
