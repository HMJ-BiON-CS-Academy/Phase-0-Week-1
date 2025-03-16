# Phase-0-Week-1

# JavaScript - Week 1: Data Type, Loop, dan Control Flow


## 1. Data Type
JavaScript adalah bahasa pemrograman dinamik dengan tipe data dinamis. Sifat dinamis ini membuat suatu variabel dapat diberi nilai dengan tipe data apapun. Selain itu JavaScript juga bersifat _weakly typed_ yang artinya ketika suatu operasi melibatkan tipe data yang berbeda, konversi tipe data akan dilakukan secara implisit (otomatis).

### Tipe Data Primitif
Dalam JavaScript, tipe data primitif bersifat _immutable_ (tidak dapat diubah).
- **Undefined**: Ketiadaan nilai. JavaScript menggunakan `Undefined` ketika variabel belum ada nilai sama  sekali.
- **Null**: Ketiadaan object (kosong).
- **Boolean**: Nilai logika `true` atau `false`.
- **Number**: Angka, baik bilangan bulat maupun desimal.
- **String**: Teks yang diapit oleh tanda kutip (' ' atau " ").

#### Contoh Penggunaan:
```javascript
let job; // Undefined
let address = null; // Null
let isStudent = true; // Boolean
let age = 25; // Number
let name = "John"; // String
let person = { firstName: "Alice", lastName: "Doe" }; // Object
let numbers = [1, 2, 3, 4, 5]; // Array
```

### Objects
Dalam JavaScript, object bersifat _mutable_ (dapat diubah).
- **Object**: Struktur data kompleks yang berisi kumpulan properti dan nilai.
- **Dates**: Representasi suatu waktu dengan format yang independen.
- **Array**: Struktur data berindeks integer (bilangan bulat) yang dapat menyimpan banyak nilai.
- **Map**: Struktur data dengan tipe indeks bebas (primitif atau object).
- **Set**: Struktur data yang hanya dapat menyimpan nilai unik.

#### Tugas
1. Buat variabel dengan masing-masing tipe data di atas.
2. Cetak semua variabel tersebut ke console menggunakan `console.log()`.

#### Tautan
- [JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures)

---

## 2. Loop (Perulangan)
Loop digunakan untuk menjalankan blok kode berulang kali.

### Jenis Loop dalam JavaScript:
1. **for** - Perulangan dengan jumlah iterasi yang sudah diketahui.
2. **while** - Perulangan selama kondisi tertentu masih bernilai `true`.
3. **do...while** - Mirip dengan `while`, tetapi dijalankan minimal sekali sebelum pengecekan kondisi.
4. **forEach** - Khusus untuk array.

### Contoh Penggunaan:
```javascript
// for loop
for (let i = 0; i < 5; i++) {
  console.log("Iterasi ke-" + i);
}

// while loop
let j = 0;
while (j < 5) {
  console.log("Iterasi ke-" + j);
  j++;
}

// do...while loop
let k = 0;
do {
  console.log("Iterasi ke-" + k);
  k++;
} while (k < 5);

// forEach loop untuk array
let fruits = ["Apple", "Banana", "Cherry"];
fruits.forEach(function(fruit) {
  console.log(fruit);
});
```

### Assignment:
1. Buat perulangan `for` yang mencetak angka 1 sampai 10.
2. Gunakan `while` untuk mencetak angka 10 sampai 1.
3. Buat array berisi 5 nama buah, lalu cetak semua elemen menggunakan `forEach`.

---

## 3. Control Flow (Alur Kontrol)
Alur kontrol digunakan untuk menentukan bagaimana kode dijalankan berdasarkan kondisi tertentu.

### Struktur Control Flow:
1. **if, else if, else** - Untuk menjalankan kode berdasarkan kondisi tertentu.
2. **switch** - Alternatif dari `if...else` untuk banyak kondisi.
3. **ternary operator** - Sintaks singkat untuk `if...else`.

### Contoh Penggunaan:
```javascript
// if, else if, else
let score = 85;
if (score >= 90) {
  console.log("A");
} else if (score >= 80) {
  console.log("B");
} else {
  console.log("C");
}

// switch
let day = "Monday";
switch (day) {
  case "Monday":
    console.log("Hari Senin");
    break;
  case "Tuesday":
    console.log("Hari Selasa");
    break;
  default:
    console.log("Hari lainnya");
}

// Ternary operator
let age = 18;
let message = age >= 18 ? "Dewasa" : "Anak-anak";
console.log(message);
```

### Assignment:
1. Buat program yang meminta pengguna memasukkan angka, lalu cetak apakah angka tersebut positif, negatif, atau nol.
2. Buat program menggunakan `switch` yang mencetak nama hari berdasarkan a
