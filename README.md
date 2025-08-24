# Foundational JavaScript

## Pengenalan

JavaScript adalah bahasa pemrograman yang fleksibel (dinamik), tidak seperti bahasa pemrograman lain pada umumnya. Pada sesi ini kita akan mempelajari lebih mendalam apa itu JavaScript dan perbedaannya dengan NodeJs. Mengapa ada perbedaan? Bukankah NodeJs menggunakan bahasa pemrograman JavaScript juga?

Dalam konteks web, kita tahu bahwa JavaScript itu dijalankan pada client-side atau browser. Browser modern saat ini pasti dilengkapi dengan **JavaScript Engine** yang menterjemahkan bahasa JavaScript menjadi bahasa mesin yang dapat dieksekusi mesin. Yang paling umum dikenal adalah **V8 JavaScript Engine** yang dikembangkan Google. Browser yang berbasis *chromium* (Google chrome, ms Edge, Opera) menggunakan V8 engine ini. Yang perlu digaris bawahi disini adalah, **JavaScript engine ini adalah sebuah program C++**. Bahkan NodeJs sendiri juga sebuah program C++ yang memanfaatkan V8 Engine untuk menghadirkan fitur-fitur pengembangan back-end. JavaScript sendiri adalah bahasa pemrograman yang *high level* untuk memudahkan developer mengembangkan interaktif web.

Untuk dipahami bahwa NodeJs itu mengekstensi fitur-fitur yang ada dari V8 Engine. Artinya ruang lingkup NodeJs lebih besar dari ruang lingkup JavaScript/ECMAscript. Pada sesi ini kita tidak akan membahas fitur yang khusus dimiliki NodeJs saja seperti `FileSystem`. Kita akan mempelajari dasar-dasar JavaScript yang diperlukan untuk pengembangan back-end dengan NodeJs.


## I. Variable, Data Type, and Operators

### Deklarasi Variabel
Terdapat 3 kata kunci untuk deklarasi variable dalam JavaScript: `var`, `let`, dan `const`.
- `var` sudah ada sejak awal mula JavaScript. Deklarasi variabel dengan `var` memiliki *scope* (ruang lingkup) global, atau function. Artinya hanya dapat diakses didalam fungsi dimana variable `var` dideklarasikan, atau dapat diakses secara global jika dideklarasikan diluar fungsi.
- `let` diperkenalkan sejak ES6. Deklarasi variable dengan `let` memiliki *block scope*. Artinya hanya dapat diakses dalam ruang lingkup sebuah blok (dalam lingkup `if`, atau lingkup `for`, atau dalam lingkup tanda `{ }`).
- `const` mirip dengan `let`. Digunakan untuk deklarasi variabel yang bersifat *read-only* (isi variabel tidak dapat diubah).

Contoh-1
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

Contoh-2
```javascript
// Imagine we are tracking quiz attempts
var attempts = 1;
var attempts = 2; // allowed with var

let score = 10;
// let score = 20; ❌ Not allowed (will cause error)

const maxAttempts = 3;
// const maxAttempts = 4; ❌ Not allowed (will cause error)

// ✅ Re-assignment check
attempts = 5;  // works
score = 15;    // works
// maxAttempts = 2; ❌ Not allowed

console.log("attempts:", attempts);     // 5
console.log("score:", score);           // 15
console.log("maxAttempts:", maxAttempts); // 3
```
- `var` dapat dideklarasi ulang
- `let` dapat tidak dapat dideklarasi ulang, namun bisa di-assign ulang
- `const` tidak dapat dideklarasi ulang atau di-assign ulang

#### Tugas
1. Buatlah variabel global `studentName`, variabel blok `subject` dan variabel konstan `maxScore`
2. Dari tugas pertama, buatlah sebuah block scope. Deklarasi ulang ketiga variabel dengan nilai berbeda dan tampilkan hasilnya dengan `console.log()`
3. Dari tugas kedua, tampilkan nilai dari ketiga variabel 

### Tipe-Tipe Data
JavaScript memiliki tipe data dinamis atau disebut juga _weakly typed_. Sifat dinamis ini membuat suatu variabel dapat diberi nilai dengan tipe data apapun. Ketika suatu operasi melibatkan tipe data yang berbeda, konversi tipe data akan dilakukan secara implisit (otomatis).

Beberapa tipe data primitif JavaScript:
- **Undefined**: Ketiadaan nilai. JavaScript menggunakan `Undefined` ketika variabel belum ada nilai sama  sekali
- **Null**: Ketiadaan object (kosong)
- **Boolean**: Nilai logika `true` atau `false`.
- **Number**: Angka, baik bilangan bulat maupun desimal. Ada juga tipe `BigInt`
- **String**: Teks yang diapit oleh tanda kutip ('' atau "" atau ``)

Dan tipe data non-primitif (reference) JavaScript:
- **Object**: sebuah koleksi pasangan key-value. Ada object yang built-in dan yg didefinisikan user sendiri.
- **Array**: juga berupa `object` yang berguna untuk menyimpan kumpulan data.
- **Function**: ya benar, ini juga berupa `object`. Function dalam JavaScript disebut juga *First-Class Function* yang merupakan ciri khas JavaScript.

#### Contoh Penggunaan:
```javascript
let job; // Undefined
let email = null; // Null
let isStudent = true; // Boolean
let age = 25; // Number
const name = "John"; // String
const person = { firstName: "Alice", lastName: "Doe" }; // Object
const numbers = [1, 2, 3, 4, 5]; // Array
```

Tipe data primitif bersifat _immutable_ sedangkan tipe object bersifat _mutable_. 

### Hoisting
Hoisting (pengangkatan) adalah perilaku default javascript yang secara otomatis memindahkan deklarasi variabel ke bagian paling atas/awal dalam scope deklarasinya (scope global atau function) pada saat kompilasi, sebelum kode dijalankan. 
```javascript
    myFunction(); // This works!
    function myFunction() {
      console.log("Hello from myFunction!");
    }
```
- Deklarasi dengan `var` akan di-hoisted ke awal scope. Tetapi inisialisasi variabel itu tetap sesuai dimana baris ditulis.
```javascript
    console.log(myVar); // Outputs: undefined
    var myVar = "Hello";
    console.log(myVar); // Outputs: Hello
```
- Deklarasi dengan `let` dan `const` juga seperti `var`, tetapi variabel tidak dapat diakses sampai inisialisasi dilakukan
```javascript
    // console.log(myLet); // ReferenceError: Cannot access 'myLet' before initialization
    let myLet = "Hello";

    // console.log(myConst); // ReferenceError: Cannot access 'myConst' before initialization
    const myConst = "World";
```

#### Tugas
1. Buatlah variabel string `studentName`, number `score`, bool `isPassed`.
2. Tampilkan pada konsol per baris, "Nama murid: {studentName}", "Nilai: {score}", "Lulus: {isPassed}"

### Operator Dasar JavaScript

Beberapa operator **aritmatika**:
- Tambah `+`, kurang `-`, kali `*`, bagi `/`
- Sisa pembagian, atau disebut modulus `%`
- Eksponen `**`
- `++` Increment, `--` decrement

Operator **perbandingan**:
- Kesamaan nilai `==`
- Kesamaan nilai dan tipe data, atau disebut strict equality `===`
- Ketidaksamaan `!=`
- Ketidaksamaan nilai dan tipe data `!==`
- Lebih dari `>`, kurang dari `<`
- Sama atau lebih dari `>=`, sama atau kurang dari `<=`

Operator **logika**:
- Logika AND `&&`
- Logika OR `||`
- Logika NOT `!`

Kondisional (**Ternary**) Operator, adalah oeprator yg membutuhkan 3 operand yang berguna sebagai cara singkat menulis `if...else`, sintaks: `condition ? expressionIfTrue : expressionIfFalse`

Operator string:
- `+` menyambung string
- `+=` juga menyambung string, sekaligus assignment ke variabel

#### Tugas
1. Buatlah variabel `jumlahBenar` dan `bobotNilai`. Kalikan lalu tampilkan hasilnya pada konsol!
2. Dari hasil tugas-1, buatlah variabel `passingGrade`. Gunakan operator perbandingan. Tampilkan teks "Lulus" jika mencapai passing grade!
3. Buatlah variabel `isKehadiranCukup` dan `isTugasSelesai`. Gunakan operator logika yang menghasilkan output variabel `isLayakUjian` jika kedua variabel sebelumnya bernilai `true`.
4. Dari hasil tugas-2, tampilkan teks "Nama {nama} - nilai: {nilai}". Gunakan operator string untuk menyambungkan teks!

#### Tautan
- [JavaScript data types and data structures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Data_structures)
- [First-Class Function](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function)

---

## II. Control Flow (Conditionals & Looping)
### Control Flow 1: Conditionals
Alur kontrol digunakan untuk menentukan bagaimana kode dijalankan berdasarkan kondisi tertentu.

#### Struktur Control Flow:
1. **if, else if, else** - Untuk menjalankan kode berdasarkan kondisi tertentu.
2. **switch** - Alternatif dari `if...else` untuk banyak kondisi.
3. **ternary operator** - Sintaks singkat untuk `if...else`.

#### Contoh Penggunaan:
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

#### Truthy & Falsy values
Dalam konteks boolean (true/false) JavaScript menganggap beberapa nilai sebagai `true`, dan kebalikannya sebagai `false`. Berikut nilai-nilai yang dianggap **falsy**:
```javascript
if (false) {
  // Not reachable
}
if (null) {
  // Not reachable
}
if (undefined) {
  // Not reachable
}
if (0) {
  // Not reachable
}
if (-0) {
  // Not reachable
}
if (0n) {
  // Not reachable
}
if (NaN) {
  // Not reachable
}
if ("") {
  // Not reachable
}
```
Maka nilai-nilai yang tidak termasuk falsy, adalah truthy. Lebih mudah mengingat nilai apa saja yang dianggap `false`, dan kebalikannya otomatis adalah `true`.

#### Tugas
1. Buat program yang meminta pengguna memasukkan angka, lalu cetak apakah angka tersebut positif, negatif, atau nol.
2. Buatlah program perhitungan nilai huruf Binus dari sebuah nilai angka. A (90-100), A- (85-89), B+ (80-84), B (75-79), B- (70-74), C (65-69), D(50-64), E (0-49)

---

## Control Flow 2: Looping
Loop digunakan untuk menjalankan blok kode berulang kali.

#### Jenis Loop dalam JavaScript:
1. **for** - Perulangan dengan jumlah iterasi yang sudah diketahui.
2. **for...in**  - Perulangan terhadap key dari sebuah koleksi.
3. **for...of** - Perulangan terhadap nilai dari sebuah koleksi.
4. **forEach** - Khusus untuk array.
5. **while** - Perulangan selama kondisi tertentu masih bernilai `true`.
6. **do...while** - Mirip dengan `while`, tetapi dijalankan minimal sekali sebelum pengecekan kondisi.


#### Contoh Penggunaan:
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

Contoh perbedaan scope variabel dalam perulangan
```javascript
// Suppose we loop through quiz questions
for (var i = 1; i <= 3; i++) {
    setTimeout(() => console.log("var i:", i), 100);
}

for (let j = 1; j <= 3; j++) {
    setTimeout(() => console.log("let j:", j), 100);
}
```

#### Assignment:
1. Buat perulangan `for` yang mencetak angka 1 sampai 10.
2. Gunakan `while` untuk mencetak angka 10 sampai 1.
3. Buat array berisi 5 nama buah, lalu cetak semua elemen menggunakan `forEach`.

---

## III. Functions
Function adalah blok kode yang dirancang untuk melakukan tugas tertentu. Function memungkinkan kita untuk menulis kode yang dapat digunakan kembali, sehingga meningkatkan efisiensi dan mengurangi duplikasi kode.

Dalam JavaScript, ada beberapa cara untuk mendefinisikan function:

1. **Function Declaration**: Function yang dideklarasikan dengan kata kunci `function`.
2. **Function Expression**: Function yang disimpan dalam sebuah variabel.
3. **Arrow Function**: Bentuk ringkas dari function expression.

### Contoh Penggunaan

#### Function Declaration

```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
console.log(greet("Alice")); // Output: Hello, Alice!
```

#### Function Expression

```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};
console.log(greet("Bob")); // Output: Hello, Bob!
```

#### Arrow Function

```javascript
const greet = (name) => `Hello, ${name}!`;
console.log(greet("Charlie")); // Output: Hello, Charlie!
```
---

## IV. Closures, IIFE, `this` keyword
### Closures
Closures adalah istilah yang menggambarkan gabungan fungsi-fungsi yang membentuk ruang tertutup sendiri (enclosed), dimana fungsi yang lebih didalam (nesting) dapat mengakses member diluar lingkup/scope-nya sendiri.

```javascript
function createProgressTracker(courseName) {
    let completedLessons = 0;

    return {
        completeLesson: function () {
            completedLessons++;
            console.log(`You have completed ${completedLessons} lesson(s) in ${courseName}.`);
        },
        getProgress: function () {
            return completedLessons;
        }
    };
}

// For a JavaScript course
const jsCourseProgress = createProgressTracker("JavaScript Essentials");

jsCourseProgress.completeLesson(); // You have completed 1 lesson(s) in JavaScript Essentials.
jsCourseProgress.completeLesson(); // You have completed 2 lesson(s)...

console.log(jsCourseProgress.getProgress()); // 2

```
Jika anda ingat, sebuah function juga merupakan sebuah object. Sehingga `createProgressTracker()` dapat ditampung dalam sebuah variable `jsCourseProgress`. Sebuah ruang lingkup tertutup (closures) yang bernama `createProgressTracker` terbentuk. Dari luar lingkup, kita hanya dapat memanggil `completeLesson()` dan `getProgress()`, namun variabel `completedLessons` tidak dapat diakses dari luar lingkup (dapat dianggap sebuah **enkapsulasi**). Selama didalam ruang tertutup itu, variabel `completedLessons` dapat diakses dimana saja, baik didalam fungsi `completeLesson()` atau fungsi `getProgress()`.

### Immediately Invoked Function Expresssion (IIFE)
Adalah deklarasi fungsi yang langsung tereksekusi ketika dideklarasikan. Sering dijumpai  bentuk IIFE ini pada modul/library eksternal karena ini adalah pola modular. IIFE membentuk scope-nya sendiri sehingga terbentuk enkapsulasi (private scope). Berikut bentuk dari IIFE:
```javascript
    (function() {
        // Function body
    })(); // ← IIFE: defined and invoked immediately
```
Contoh sebuah modul `CourseModule.js`:
```javascript
// CourseModule.js

const CourseApp = (() => {
  const courses = [
    { id: 1, title: "JavaScript Fundamentals", level: "Beginner" },
    { id: 2, title: "Node.js for Web Developers", level: "Intermediate" },
    { id: 3, title: "React in Practice", level: "Advanced" },
  ];

  function renderCourses() {
    console.log("Available Courses:");
    courses.forEach(course => {
      console.log(`- ${course.title} [${course.level}]`);
    });
  }

  function findCourseById(id) {
    return courses.find(course => course.id === id);
  }

  // Public API
  return {
    render: renderCourses,
    find: findCourseById
  };
})(); // ← IIFE: defined and invoked immediately

// Usage
CourseApp.render(); // Initializes and prints course list
const selected = CourseApp.find(2);
console.log("Selected course:", selected.title);
```
Kegunaan IIFE:
- IIFE menjaga variabel courses tidak dapat diakses dari luar (global scope)
- Variabel dan fungsi langsung terinisialisasi
- Hanya menampakkan interface yang diperlukan saja (`render()` dan `find()`)

### The `this` keyword
🧠 Concept Summary of `this`:
| Skenario | `this` mengacu kepada |
| --- | --- |
| Dalam Fungsi | Objek Global (`window` pada browser) |
| Dalam Method | Objek dimana method itu berada |
| Dalam Arrow Function | Reference `this` dalam scope |
| Dalam Event Listener | Element terkait event |
| Penggunaan `call`,`apply`,`bind`| diatur secara eksplisit |
