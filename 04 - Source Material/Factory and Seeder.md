---
cssclasses:
  - h1-center
  - indent
tags:
  - "#webdeveloper"
  - "#laravel"
Tanggal: 2025-01-06
---
# **Database Factory dan Seeder**
---
Dalam laravel kedua fitur ini digunakan untuk membantu membuat dan mengisi data dummy ke dalam database dalam wakktu singkat, yang mana biasanya ini sangat di perlukan dalam tahap testing dan production.

![[Pasted image 20250106230132.png|600]]
#### Database factory

Seperti namanya fitur factory ini bisa diartikan seperti pabrik yang berfungsi untuk memproduksi data palsu/dummy dalam jumlah yang besar namun tetap realistis. Jadi fitur ini mendefinisikan bagaimana sebuah model atau tabel harus diisi dengan data.

Fitur ini juga biasanya dibantu dengan fungsi yang bernama Fake. Fungsi ini berfungsi untuk men-generate data palsu/dummy sesuai dengan yang kita inginkan.


> [!info]- Cara Kerja
> Cara kerja factory biasanya diintegrasikan dengan fitur Seeder ataupun menggunakan tinker.
> 
> Contoh kode untuk menggunakan factory:
> User::factory()->count(10)->create();

##### **Command untuk membuat factory:**
```
php artisan make:factory <nama>
```

##### **Penggunaan:**

###### Contoh pembuatan model factory untuk data user
```php
public function definition(): array {
	return [
		'name' => fake()->name(),
		'email' => fake()->unique()->safeEmail(),
		'email_verified_at' => now(),
		'password' => static::$password ??= Hash::make('password'),
		'remember_token' => Str::random(10),
	];
}
```
###### Contoh pembuatan model factory untuk pembuatan data pekerjaan
```php
public function definition(): array
    {
        return [
            'employer_id' => fake()->company(),
            'jobs' => [
                    'title' => fake()->jobTitle(),
                    'description' => fake()->paragraph(),
                    'salary' => "$50.000"
                ]
        ];
    }
```

#### Database Seeder
Digunakan untuk menyisipkan data ke dalam database secara eksplisit, baik data dummy maupun data awal yang spesifik untuk aplikasi. Jadi Seeder berisi logika untuk menyisipkan data ke tabel tertentu. 

> [!info] Cara Kerja
> Seeder dapat memanggil factory untuk menghasilkan data dummy.

##### **Penggunaan:**

###### Command untuk membuat model seeder
```
php artisan make:seeder <nama>
```
###### Contoh pembuatan model seeder
```php
use Illuminate\Database\Seeder;
use App\Models\User;

class UserSeeder extends Seeder
{
    public function run()
    {
        // Membuat data spesifik
        User::create([
            'name' => 'Admin',
            'email' => 'admin@example.com',
            'password' => bcrypt('password'),
        ]);

        // Memanggil factory untuk data dummy
        User::factory()->count(10)->create();
    }
}

```

###### Menjalankan seeder
```
php artisan db:seed --class=<nama model>
```
atau
```
php artisan migrate:fresh --seeder=<nama model>
```