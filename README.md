# Full-Stack Multi-Container Application with Docker

Proyek ini merupakan implementasi aplikasi full-stack berbasis arsitektur multi-container menggunakan Docker. Seluruh komponen — REST API, frontend, CMS, dan database — dikemas dalam layanan terpisah yang saling terintegrasi dalam satu ekosistem.

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

Layanan dalam `docker-compose.yml`:
- `api-service` — Golang REST API  
- `client-web` — React Next.js frontend  
- `cms-service` — Laravel CMS  
- `db` — MariaDB  

Tujuan arsitektur ini:
- Isolasi per service 
- Pengembangan modular
- Kemudahan scaling
- Deployment yang konsisten

---

## Struktur Folder

```
contact-app-docker-architecture/
│── README.md
│── docker-compose.yaml
│── .env
└── app/
    ├── api-service/      # Golang REST API
    ├── client-web/       # Next.js frontend
    └── cms-service/      # Laravel CMS
```

## Konfigurasi Lingkungan

File `.env` berada di root repository.  
Gunakan file ini untuk menyimpan:

- credential database
- port service
- konfigurasi masing-masing container

Contoh variabel (sesuaikan kebutuhan):

```
API_PORT=8080
CLIENT_PORT=3000
CMS_PORT=8000

DB_USER=root
DB_PASSWORD=root
DB_NAME=projectdb
DB_PORT=3306
```

---

## Cara Menjalankan Proyek

### 1. Build dan jalankan seluruh service
```
docker compose up -d --build
```

### 2. Menghentikan semua service
```
docker compose down
```

### 3. Akses aplikasi
- API → `http://localhost:${API_PORT}`
- Frontend → `http://localhost:${CLIENT_PORT}`
- CMS → `http://localhost:${CMS_PORT}`

(Port menyesuaikan konfigurasi `docker-compose.yml`.)

---

## Workflow Pengembangan

Menjalankan service tertentu saja:
```
docker compose up <service-name>
```

Melihat log service:
```
docker compose logs -f <service-name>
```

Build ulang tanpa cache:
```
docker compose build --no-cache
```

---

## Catatan Penting

- Setiap service wajib memiliki Dockerfile masing-masing di dalam foldernya.
- Internal communication menggunakan hostname service Docker, bukan `localhost`.
- Setelah perubahan struktur folder, pastikan path context pada `docker-compose.yaml` sudah sesuai.

---
