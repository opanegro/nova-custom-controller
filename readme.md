# Laravel Nova Custom Controller

[![GitHub issues](https://img.shields.io/github/issues/opanegro/nova-custom-controller)](https://github.com/opanegro/nova-custom-controller/issues)
[![GitHub forks](https://img.shields.io/github/forks/opanegro/nova-custom-controller)](https://github.com/opanegro/nova-custom-controller/network)
[![GitHub stars](https://img.shields.io/github/stars/opanegro/nova-custom-controller)](https://github.com/opanegro/nova-custom-controller/stargazers)
[![GitHub license](https://img.shields.io/github/license/opanegro/nova-custom-controller)](https://github.com/opanegro/nova-custom-controller/blob/master/LICENSE)

**Package Nova Custom Controller** berfungsi untuk mengolah request tanpa perlu membuat controller baru, karna fitur ini sudah otomatis meng-override controller pada Laravel Nova anda.

### Required:

1. PHP Version >= 7.1
2. Laravel >= 5.8
3. Laravel Nova >= 2.0

### Cara Install:

1. Kemudian jalankan command:
```
composer require opanegro/nova-custom-controller
```
2. Selesai

### Cara Penggunaan:

1. Daftarkan `trait` di file `app/Nova/Resource.php`

```php
...
use Opanegro\NovaCustomController\Traits\NovaCustomEvents;

abstract class Resource extends NovaResource
{
    use NovaCustomEvents;
    
    ...
}
```

2. Tambahkan method yang anda butuhkan di resources, contoh pada resource `app/Nova/User.php`

```php
class User extends Resource
{
    ...
    
    /**
     * Before updated in controller
     *
     * @param \Illuminate\Http\Request $request
     * @param \Illuminate\Database\Eloquent\Model $model
     */
    public static function beforeUpdated(Request $request, Model $model)
    {
        // your codes
    }
}
```

#### Create Controller with command

`php artisan nova:custom-controller User --event=store --custom-uri-key=users`

- `User`: is the name of resource
- `--event`: is event if you want, available `store`, `update`
- `--custom-uri-key`: if you set the resource with custom uri key
 
#### Daftar method yang bisa digunakan:

| Method Name | Type | Return | Description |
|---|---|---|---|
| `beforeCreated()` | `static function` | | Proses sebelum melakukan penyimpanan data baru |
| `afterCreated()` | `static function` | | Proses setelah melakukan penyimpanan data baru |
| `beforeUpdated()` | `static function` | | Proses sebelum melakukan penyimpanan data lama |
| `afterUpdated()` | `static function` | | Proses setelah melakukan penyimpanan data lama |
| `afterSave()` | `static function` | | Proses setelah melakukan penyimpanan data baru & lama |
| `beforeSave()` | `static function` | | Proses sebelum melakukan penyimpanan data baru & lama |
| `customStoreController()` | `static function` | | Custom full store process controller |
| `customUpdateController()` | `static function` | | Custom full update process controller |
| `$unsetCustomFields` | `static variable` | `array` | Unset model jika terdapat nama custom field yang tidak tersedia di `fillable` |
| `$setCustomRequests` | `static variable` | `array` | Menambah request baru untuk melakukan process pada model |

### Contribute:
- If you help us, translate to english
- Add your request or bug in issue

#### Terima kasih buat:
- DOT Mas Ardi
- DOT Mas Didik
- DOT Mas Haris
- DOT Team Projek
- DOT Rangers
