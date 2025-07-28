# Foundational JavaScript

## Pengenalan

JavaScript adalah bahasa pemrograman yang fleksibel (dinamik), tidak seperti bahasa pemrograman lain pada umumnya. Pada sesi ini kita akan mempelajari lebih mendalam apa itu JavaScript dan perbedaannya dengan NodeJs. Mengapa ada perbedaan? Bukankah NodeJs menggunakan bahasa pemrograman JavaScript juga?

Dalam konteks web, kita tahu bahwa JavaScript itu dijalankan pada client-side atau browser. Browser modern saat ini pasti dilengkapi dengan **JavaScript Engine** yang menterjemahkan bahasa JavaScript menjadi bahasa mesin yang dapat dieksekusi mesin. Yang paling umum dikenal adalah **V8 JavaScript Engine** yang dikembangkan Google. Browser yang berbasis *chromium* (Google chrome, ms Edge, Opera) menggunakan V8 engine ini. Yang perlu digaris bawahi disini adalah, **JavaScript engine ini adalah sebuah program C++**. Bahkan NodeJs sendiri juga sebuah program C++ yang memanfaatkan V8 Engine untuk menghadirkan fitur-fitur pengembangan back-end. JavaScript sendiri adalah bahasa pemrograman yang *high level* untuk memudahkan developer mengembangkan interaktif web.

Untuk dipahami bahwa NodeJs itu mengekstensi fitur-fitur yang ada dari V8 Engine. Artinya ruang lingkup NodeJs lebih besar dari ruang lingkup JavaScript/ECMAscript. Pada sesi ini kita tidak akan membahas fitur yang khusus dimiliki NodeJs saja seperti `FileSystem`. Kita akan mempelajari dasar-dasar JavaScript yang diperlukan untuk pengembangan back-end dengan NodeJs.


## I. Variable, Data Type, and Operators

### Deklarasi Variabel
Terdapat 3 kata kunci untuk deklarasi variable dalam JavaScript: `var`, `let`, dan `const`.
- `var` sudah ada sejak awal mula JavaScript. Deklarasi variabel dengan `var` memiliki *scope* (ruang lingkup) global, atau function. Artinya hanya dapat diakses didalam fungsi dimana variable `var` dideklarasikan, atau dapat diakses secara global jika dideklarasikan diluar fungsi.
- `let` diperkenalkan sejak ES6. Deklarasi variable dengan `let` memiliki *block scope*. Artinya hanya dapat diakses dalam ruang lingkup sebuah blok (dalam lingkup `if`, atau lingkup `for`, atau dalam lingkup tanda { }).
- `const` mirip dengan `let`. Digunakan untuk deklarasi variabel yang bersifat *read-only* (isi variabel tidak dapat diubah).

```javascript
function testScope() {
  if (true) {
    var x = 10;
    let y = 20;
  }

  console.log(x); // ✅ Works: var is function-scoped
  console.log(y); // ❌ Error: let is block-scoped
}

testScope();
```

JavaScript adalah bahasa pemrograman dinamik dengan tipe data dinamis. Sifat dinamis ini membuat suatu variabel dapat diberi nilai dengan tipe data apapun. Hal ini membuat JavaScriptc bersifat _weakly typed_ yang artinya ketika suatu operasi melibatkan tipe data yang berbeda, konversi tipe data akan dilakukan secara implisit (otomatis).

### Tipe-Tipe Data
Dalam JavaScript, tipe data primitif bersifat _immutable_ (tidak dapat diubah).
- **Undefined**: Ketiadaan nilai. JavaScript menggunakan `Undefined` ketika variabel belum ada nilai sama  sekali.
- **Null**: Ketiadaan object (kosong).
- **Boolean**: Nilai logika `true` atau `false`.
- **Number**: Angka, baik bilangan bulat maupun desimal.
- **String**: Teks yang diapit oleh tanda kutip (' ' atau " " atau ` `).

#### Contoh Penggunaan:
```javascript
let job; // Undefined
let email = null; // Null
let isStudent = true; // Boolean
let age = 25; // Number
let name = "John"; // String
let person = { firstName: "Alice", lastName: "Doe" }; // Object
let numbers = [1, 2, 3, 4, 5]; // Array
```

### Object
Dalam JavaScript, object bersifat _mutable_ (dapat diubah). Objek adalah sebuah struktur data kompleks yang berisi kumpulan properti dan nilai.
Satu ciri khas yang membedakan JavaScript dengan bahasa lainnya adalah `function` juga merupakan object. Dan karena Function juga merupakan object maka object itu dapat diberi/ditambahkan properti atau method dan dapat dianggap seperti variabel biasa. Konsep ini dalam JavaScript dikenal juga dengan sebutan "*First-Class Function*".

#### Tugas
1. Buat variabel dengan masing-masing tipe data di atas.
2. Cetak semua variabel tersebut ke console menggunakan `console.log()`.

#### Tautan
- [JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures)
- [First-Class Function](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function)

---

## 2. Loop (Perulangan)
Loop digunakan untuk menjalankan blok kode berulang kali.

### Jenis Loop dalam JavaScript:
1. **for** - Perulangan dengan jumlah iterasi yang sudah diketahui.
2. **for...in**  - Perulangan terhadap key dari sebuah koleksi.
3. **for...of** - Perulangan terhadap nilai dari sebuah koleksi.
4. **forEach** - Khusus untuk array.
5. **while** - Perulangan selama kondisi tertentu masih bernilai `true`.
6. **do...while** - Mirip dengan `while`, tetapi dijalankan minimal sekali sebelum pengecekan kondisi.


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
