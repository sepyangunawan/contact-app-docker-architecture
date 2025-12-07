# Full-Stack Multi-Container Application with Docker Compose

Proyek ini merupakan implementasi aplikasi full-stack berbasis arsitektur multi-container menggunakan Docker Compose. Seluruh komponen — REST API, frontend, CMS, dan database — dikemas dalam layanan terpisah yang saling terintegrasi dalam satu ekosistem.

## Komponen Utama

### 1. RESTful API (Golang)
Layanan API dibangun menggunakan Golang dengan pendekatan microservice. Fokusnya pada:
- Perancangan endpoint REST yang efisien.
- Struktur modular untuk skala dan maintainability.
- Manajemen request–response secara optimal.

### 2. Frontend Web (React Next.js)
Antarmuka pengguna dikembangkan menggunakan React dengan Next.js.  
Integrasi dengan API dilakukan melalui mekanisme fetch/axios, dengan fokus pada:
- Responsivitas UI.
- Pengelolaan state yang bersih.
- Optimasi rendering sisi server (SSR) bila diperlukan.

### 3. CMS (Laravel)
CMS digunakan untuk mengelola konten aplikasi. Komponen ini menyediakan:
- CRUD data berbasis Laravel.
- Middleware untuk autentikasi/perizinan.
- Integrasi langsung dengan database.

### 4. Database (MariaDB)
Database utama aplikasi. Meliputi:
- Perancangan skema database.
- Optimasi query dasar.
- Persistensi data dari API maupun CMS.

---

## Arsitektur Multi-Container

Seluruh layanan berjalan dalam container terisolasi, kemudian dikelola melalui `docker-compose`.  
Setiap service memiliki konteks dan konfigurasi masing-masing, namun saling terhubung melalui internal network Docker.

Contoh layanan dalam `docker-compose.yml`:
- `api-service` — Golang REST API  
- `client-web` — React Next.js frontend  
- `cms-service` — Laravel CMS  
- `db` — MariaDB  

Tujuan arsitektur ini:
- Isolasi komponen
- Pengembangan modular
- Kemudahan scaling
- Deployment yang konsisten

---

## Struktur Folder
(Struktur ini sesuaikan dengan repo kamu. Placeholder berikut asumsi umum.)

```
project/
│
├── api-service/          # Golang REST API
├── client-web/           # Next.js frontend
├── cms-service/          # Laravel CMS
└── docker-compose.yml
```

---

## Cara Menjalankan Proyek

### 1. Pastikan dependensi utama sudah terpasang
- Docker
- Docker Compose

### 2. Jalankan semua layanan
```
docker compose up -d
```

### 3. Akses aplikasi
- API: http://localhost:<api_port>  
- Frontend: http://localhost:<frontend_port>  
- CMS: http://localhost:<cms_port>  

(Port menyesuaikan konfigurasi `docker-compose.yml`.)

---

## Pengembangan dan Workflow

### Menjalankan satu layanan saja
```
docker compose up <service-name>
```

### Melihat logs
```
docker compose logs -f <service-name>
```

### Build ulang tanpa cache
```
docker compose build --no-cache
```

---
