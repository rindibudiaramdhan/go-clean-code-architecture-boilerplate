# Golang Clean Code Architecture Boilerplate
oleh Rindi Budiaramdhan @rindibudiaramdhan

# Deskripsi

Ini adalah boilerplate yang berbasis pada bahasa pemrograman Golang yang mengimplementasikan arsitektur Clean Code.

## Arsitektur Clean Code
Arsitektur Clean Code adalah sebuah pendekatan dalam pengembangan perangkat lunak yang bertujuan untuk menciptakan kode yang mudah dipahami, mudah dipelihara, dan mudah diubah. Ini merupakan sebuah filosofi yang mempromosikan prinsip-prinsip seperti kejelasan, kesederhanaan, dan keterbacaan dalam penulisan kode.

## Karakteristik Clean Code

Karakteristik Clean Code bisa dilihat [disini](CLEANCODE_CHARACTERISTICS.md)

# Status Project

Masih terus dalam pengembangan.

# Struktur Folder

```
project-name/
├── cmd/
│   └── main.go
├── internal/
│   ├── app/
│   │   ├── domain/
│   │   │   ├── entity1.go
│   │   │   └── entity2.go
│   │   ├── usecase/
│   │   │   ├── usecase1.go
│   │   │   └── usecase2.go
│   │   └── delivery/
│   │       ├── handler/
│   │       │   └── handler.go
│   │       ├── presenter/
│   │       │   └── presenter.go
│   │       └── middleware/
│   │           └── middleware.go
│   └── platform/
│       ├── repository/
│       │   ├── db/
│       │   │   └── db_repository.go
│       │   └── mock/
│       │       └── mock_repository.go
│       ├── service/
│       │   └── service.go
│       └── config/
│           └── config.go
├── configs/
│   └── config.yaml
├── scripts/
│   └── ...
├── tests/
│   ├── unit/
│   │   └── ...
│   └── integration/
│       └── ...
├── docs/
│   └── ...
└── README.md
```

Penjelasan struktur folder:

- `cmd/`: Berisi kode yang berfungsi sebagai entry point dari aplikasi. Ini biasanya hanya terdiri dari file main.go yang menginisialisasi aplikasi.
- `internal/`: Berisi kode internal aplikasi yang tidak harus diakses oleh aplikasi lain. Terdiri dari tiga subdirektori utama:
- `app/`: Berisi domain aplikasi, termasuk definisi entity dan use case aplikasi.
- `delivery/`: Berisi kode yang berkaitan dengan pengiriman (delivery) seperti HTTP handler, middleware, dan presenter.
- `platform/`: Berisi kode yang berkaitan dengan implementasi teknis aplikasi, seperti repository untuk akses database, service untuk logika bisnis tambahan, dan konfigurasi aplikasi.
- `configs/`: Berisi file konfigurasi untuk aplikasi, seperti file YAML, JSON, atau TOML.
- `scripts/`: Berisi skrip utilitas untuk memfasilitasi pengembangan dan pemeliharaan proyek.
- `tests/`: Berisi kode untuk pengujian aplikasi, terbagi menjadi pengujian unit dan pengujian integrasi.
- `docs/`: Berisi dokumentasi proyek, termasuk dokumentasi kode, spesifikasi API, dan instruksi penggunaan.
- `README.md`: Berkas README untuk proyek, memberikan informasi tentang proyek, cara instalasi, penggunaan, dan lain-lain.

Struktur ini memisahkan peran-peran berbeda dalam aplikasi, seperti domain logic, kode pengiriman, dan implementasi teknis. Ini juga memungkinkan untuk mengikuti prinsip-prinsip Clean Architecture dengan jelas, sehingga memudahkan pemeliharaan, pengujian, dan pengembangan aplikasi secara keseluruhan.

# Instalasi

Untuk menjalankan proyek ini secara lokal, pastikan Anda telah menginstal Go (minimal versi 1.20) di sistem Anda. Ikuti langkah-langkah di bawah ini untuk menginstal dan menjalankan proyek:

## 1. Clone Repository

```bash
git clone https://github.com/rindibudiaramdhan/go-clean-code-architecture-boilerplate.git
```

## 2. Pindah ke Direktori Proyek

```bash
cd go-clean-code-architecture-boilerplate
```

## 3. Instal Dependensi

```bash
go mod tidy
```

## 4. Konfigurasi Environment

Salin file `.env.example` ke `.env` dan sesuaikan dengan konfigurasi Anda:

```bash
cp .env.example .env
```

## 5. Bangun dan Jalankan Proyek
```bash
go build -o namaproject cmd/namaproject/main.go
./namaproject
```

## 6. Akses API

Setelah proyek berhasil berjalan, Anda dapat mengakses API di `http://localhost:8080`.

Pastikan untuk memeriksa dokumentasi lebih lanjut untuk detail tambahan dan panduan penggunaan lebih lanjut.

Dengan mengikuti langkah-langkah di atas, Anda akan dapat menjalankan proyek secara lokal dan mulai mengembangkan dengan arsitektur Clean Code yang disediakan. Jika Anda mengalami kesulitan atau memiliki pertanyaan, jangan ragu untuk menghubungi tim pengembangan melalui tautan kontak yang tersedia di bawah.

# Cara Penggunaan

TBA

# Kontribusi

TBA

# Lisensi

TBA

# Pengembang

TBA

# Dukungan

TBA

# Tautan Penting

TBA

# FAQ

TBA

# Versi dan Riwayat Perubahan

TBA

# Tautan Kontributor

TBA
