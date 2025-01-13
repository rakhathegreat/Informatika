---
cssclasses:
  - h1-center
  - indent
tags:
  - laravel
  - webdeveloper
Tanggal: 2025-01-09
---
# Route Model Binding
---
> [!tip]- Sumber
> -

### Apa itu Route Model Binding?

Route Model Binding adalah fitur Laravel yang secara otomatis:
1. Menerima parameter dari URL.
2. Mencari data di database berdasarkan parameter tersebut.
3. Mengubah data menjadi objek model yang siap digunakan.

Fitur ini menghemat Anda dari menulis kode manual seperti ini di setiap rute:

```php
Route::get('/jobs/{id}', function ($id) {
    $job = Job::findOrFail($id); // Mencari data secara manual
    return $job;
});
```

Dengan Route Model Binding, kode di atas disederhanakan menjadi:

```php
Route::get('/jobs/{job}', function (Job $job) {
    return $job; // Laravel menangani pencarian data secara otomatis
});
```

### Bagaimana Cara Kerjanya?

Ketika mendefinisikan rute seperti ini:

```php
Route::get('/jobs/{job}', function (Job $job) {
    return $job;
});
```

Laravel membaca `{job}` sebagai **parameter dinamis** dari URL. Misalnya, jika pengguna mengakses:

```
http://example.com/jobs/123
```

Maka `123` adalah nilai untuk parameter `{job}`.

Ketika menambahkan tipe model (`Job $job`) pada parameter fungsi, Laravel akan:

1. Menganggap parameter `{job}` sebagai ID untuk model `Job` secara default.
2. Mencari data di tabel `jobs` dengan kolom `id` yang cocok dengan nilai parameter (dalam contoh ini, `123`).
3. Jika data ditemukan, Laravel akan mengubahnya menjadi **objek model `Job`** dan memberikannya ke fungsi rute.
4. Jika data tidak ditemukan, Laravel akan secara otomatis mengembalikan halaman 404.