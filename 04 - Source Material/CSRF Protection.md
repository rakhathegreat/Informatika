---
cssclasses:
  - h1-center
  - indent
tags:
  - laravel
  - webdeveloper
Tanggal: 2025-01-09
---
# CSRF Protection
---

> [!tip]- Sumber
> - [[Cross Site Request Forgery (CSRF)]]
### Bagaimana Laravel Melindungi dari CSRF?

Laravel menggunakan **CSRF token** untuk memastikan bahwa hanya pengguna yang sah dapat mengirimkan permintaan berbahaya. Berikut adalah langkah-langkah bagaimana Laravel menangani CSRF:

1. **Token Generasi Otomatis**:
    
    - Setiap sesi pengguna mendapatkan CSRF token unik yang disimpan di sisi server.
    - Token ini dikirimkan ke aplikasi front-end sebagai bagian dari setiap permintaan form.
2. **Validasi Token**:
    
    - Setiap kali formulir dikirim, token CSRF yang dikirimkan akan divalidasi terhadap token yang ada di sesi server.
    - Jika token tidak cocok, Laravel akan menolak permintaan tersebut.

### Implementasi

Laravel secara otomatis melindungi form dengan middleware `VerifyCsrfToken`. Untuk memastikan form Anda aman, Anda perlu menyertakan token CSRF.

Contoh penggunaan di Blade template:
```html
<form method="POST" action="/submit-form">
    @csrf
    <input type="text" name="name" placeholder="Enter your name">
    <button type="submit">Submit</button>
</form>
```

**`@csrf`**: Directive Blade untuk menyisipkan token CSRF secara otomatis ke dalam formulir.

```html
<input type="hidden" name="_token" value="csrf_token_value">
```

