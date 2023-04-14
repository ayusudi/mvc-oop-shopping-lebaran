# Shopping Lebaran

## Outcome 

- Student memahmi konsep OOP sesuai studi kasus soal dengan mengimplementasikan 
   OOP Characteristic, Relasi antar Class dan mengimplementasikan design pattern  Factory
- Student dapat memanipulasi JSON dengan fs secara Asynchronous melalui CLI.
- Student dapat membuat aplikasi MVC dan memahami konsep MVC.


Kita akan menciptakan apalikasi CRUD dengan CLI (Command Line)
Dengan data JSON (data.json)


## Release 0 OOP

Buatlah class dengan property-nya pada file class.js pada folder models, 
sesuai requirement dibawah ini: 

1. Store
    - id
    - name
    - type
    - since (private, by default tahun saat ini)
    - catalogues (by default array kosong)
2. DepartementStore
    - memiliki property yang sama dengan Store namun type sudah pasti “DepartementStore”
3. BoutiqueStore
    - memiliki property yang sama dengan Store namun type sudah pasti “BoutiqueStore”
4. Catalogue
    - name
    - price
    - madeIn (private)
    

## Release 1 READ ALL

Implementasikan fitur READ dengan Factory Method dan tentukan juga relasi antar class adalah Composition atau Aggregation?

Berikut cara menjalankan programnya dan outputnya 

```bash
$ node index.js readStore

[
  BoutiqueStore {
    id : 1,
    name: "This is June",
    type : "BoutiqueStore", 
    catalogues: [
      Catalogue { name : "Black Dress", price: 100000 },
      Catalogue { name : "Red Dress", price: 100000 },
    ]
  },
  DepartementStore {
    id : 2,
    name: "H8 Go",
    type : "DepartementStore",
    catalogues: [
      Catalogue { name: "Black Jacket", price: 180000 },
      Catalogue { name: "Blue Dress", price: 100000 },
    ]
  }
]
```

## RELEASE 2 CREATE (addCatalogue)

Implemetasikan fitur create dengan validasi tidak boleh memiliki nama yang sama dari satu toko.

Pastikan saat mengimplementasikan ini format JSON sebelumnya tetap sama.

Berikut cara menjalankan programnya dan outputnya 

```bash
$ node index.js addCatalogue <idStore> <catalogueName> <price> <madeIn>
```

Contoh berhasil :

```bash
$ node index.js addCatalogue 2 "Black Shirt" 100000 Indonesia

Berhasil menambahkan Black Shirt ke DepartementStore H8 Go.
```

Contoh gagal :

```bash
$ node index.js addCatalogue 2 "Black Shirt" 100000 Indonesia

Gagal menambahkan Black Shirt ke DepartementStore H8 Go 
karena nama tersebut telah ada.
```

Contoh gagal karena tidak ditemukan id storenya :

```bash
$ node index.js addCatalogue 20 "Black Shirt" 100000 Indonesia

ID store 20 tidak ditemukan!.
```

## RELEASE 3  READ & FILTER

Implementasikan membaca data berdasarkan id dan mencari catalogue berdasarkan nama.

Dengan command line berikut 

```bash
$ node index.js storeSearch <catalogueName> <idStore>
```

Contoh seperti berikut:

```bash
$ node index.js storeSeach Black 2 

STORE #2 
Name : H8 Go
Type : DepartementStore
This store has been running since 3 years ago.

Catalogue Result 
┌─────────┬────────────────┬────────┐
│ (index) │      name      │ price  │
├─────────┼────────────────┼────────┤
│    0    │ 'Black Jacket' │ 180000 │
│    1    │ 'Black Shirt'  │ 100000 │
└─────────┴────────────────┴────────┘
```

Contoh tidak ditemukan : 

```bash
$ node index.js storeSeach Hitam 2 

STORE #2 
Name : H8 Go
Type : DepartementStore
This store has been running since 3 years ago.

Catalogue Result 
-- NOT FOUND --
```

Contoh tidak ditemukan id store : 

```bash
$ node index.js storeSeach Hitam 20

STORE #20
-- NOT FOUND --

Catalogue Result 
-- NOT FOUND --
```
