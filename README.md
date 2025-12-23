<h1 align="center">
  Full-Stack Multi-Container Application with Docker
</h1>

<p align="center">
  <em>Proyek ini merupakan implementasi aplikasi full-stack berbasis arsitektur multi-container menggunakan Docker. Seluruh komponen — REST API, frontend, CMS, dan database — dikemas dalam layanan terpisah yang saling terintegrasi dalam satu ekosistem.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/github/last-commit/sepyangunawan/contact-app-docker-architecture" />
  <img src="https://img.shields.io/github/languages/top/sepyangunawan/contact-app-docker-architecture" />
  <img src="https://img.shields.io/github/languages/count/sepyangunawan/contact-app-docker-architecture" />
</p>

---

<p align="center">
  <strong>Built with the tools and technologies:</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/JSON-black?style=for-the-badge&logo=json&logoColor=white" />
  <img src="https://img.shields.io/badge/Markdown-000000?style=for-the-badge&logo=markdown" />
  <img src="https://img.shields.io/badge/npm-CB3837?style=for-the-badge&logo=npm" />
  <img src="https://img.shields.io/badge/Autoprefixer-DD3735?style=for-the-badge" />
  <img src="https://img.shields.io/badge/PostCSS-DD3A0A?style=for-the-badge&logo=postcss" />
  <img src="https://img.shields.io/badge/Composer-885630?style=for-the-badge&logo=composer" />
  <img src="https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black" />
  <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs" />
  <img src="https://img.shields.io/badge/Go-00ADD8?style=for-the-badge&logo=go&logoColor=white" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Gin-00ADD8?style=for-the-badge&logo=gin&logoColor=white" /> 
  <img src="https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=mariadb" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/XML-005FAD?style=for-the-badge&logo=xml&logoColor=white" />
  <img src="https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white" />
  <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" />
  <img src="https://img.shields.io/badge/Axios-5A29E4?style=for-the-badge&logo=axios&logoColor=white" />
  <img src="https://img.shields.io/badge/Bootstrap-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white" />
  <img src="https://img.shields.io/badge/YAML-CB171E?style=for-the-badge&logo=yaml&logoColor=white" />
</p>

---

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

## Konfigurasi Environment

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

