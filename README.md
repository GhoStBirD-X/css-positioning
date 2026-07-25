# README — 7.2 CSS Positioning

## Deskripsi Singkat

Folder ini berisi materi dan contoh terkait "CSS Positioning" (cara memposisikan elemen menggunakan CSS). README ini ditulis untuk membantu pemula dalam web development memahami konsep positioning di CSS dengan bahasa yang sopan, jelas, dan praktis.

## Siapa yang Dituju

- Pemula yang baru belajar HTML dan CSS
- Siswa yang ingin memahami perbedaan tipe-tipe posisi
- Siapa saja yang membutuhkan ringkasan cepat beserta contoh

## Isi yang Akan Dipelajari

1. Konsep dasar positioning
2. Tipe posisi: static, relative, absolute, fixed, sticky
3. Containing block dan posisi relatif terhadap ancestor
4. z-index dan tumpukan elemen
5. Contoh kode sederhana
6. Kesalahan umum dan tips praktis
7. Latihan singkat
8. Sumber belajar lanjut

## 1) Konsep Dasar

Positioning adalah cara menentukan di mana sebuah elemen ditempatkan dalam halaman web. Selain alur normal dokumen (flow), CSS menyediakan beberapa mode posisi yang memberi kontrol lebih: memindahkan elemen, menimpanya di atas elemen lain, atau membuat elemen tetap terlihat saat menggulir halaman.

## 2) Tipe Posisi

### static (default)
- Elemen berada di alur normal dokumen
- Properti top/right/bottom/left dan z-index tidak berlaku pada elemen static

### relative
- Tetap mengisi ruang di alur dokumen
- Menggunakan top/right/bottom/left akan memindahkan elemen relatif terhadap posisinya semula
- Cocok untuk penyesuaian kecil tanpa mengubah layout sekitar secara drastis

### absolute
- Dikeluarkan dari alur dokumen; elemen lain berperilaku seolah elemen absolute tidak ada
- Posisi dihitung relatif terhadap "containing block" (ancestor yang memiliki posisi selain static; biasanya parent terdekat dengan position: relative/absolute/fixed/sticky). Jika tidak ada ancestor berposisi, posisi dihitung terhadap viewport
- Sering digunakan untuk tooltip, menu pop-up, atau menempatkan ikon di dalam container

### fixed
- Mirip dengan absolute, tetapi selalu relatif terhadap viewport (area tampilan browser)
- Tetap pada tempatnya ketika halaman digulir
- Cocok untuk header/footer atau tombol "back to top"

### sticky
- Perilaku gabungan antara relative dan fixed
- Berperilaku seperti relative sampai mencapai posisi tertentu saat digulir, lalu menjadi fixed
- Berguna untuk header tabel atau navigasi kecil yang harus selalu terlihat setelah melewati titik tertentu

## 3) Containing Block dan Aturan Penting

- Containing block untuk elemen absolute/fixed menentukan titik referensi untuk top/right/bottom/left
- Untuk absolute: jika ada ancestor dengan position selain static, gunakan ancestor tersebut sebagai referensi
- Untuk fixed: umumnya selalu relatif ke viewport, kecuali beberapa konteks (mis. transform pada ancestor) yang dapat mengubahnya
- Perhatikan bahwa transform, filter, atau perspective pada parent dapat membuat fixed/absolute berperilaku berbeda — jika hasilnya mengejutkan, periksa style pada ancestor

## 4) z-index dan Tumpukan Elemen

- z-index mengontrol urutan tumpukan (stacking order). Nilai lebih besar muncul di atas nilai lebih kecil
- z-index hanya berlaku pada elemen yang memiliki posisi selain static (relative/absolute/fixed/sticky) atau pada elemen dengan transform
- Perhatikan konteks stacking (stacking context): beberapa properti (mis. position dengan z-index, opacity < 1, transform, filter) membuat konteks tumpukan baru yang memengaruhi bagaimana elemen dibandingkan

## 5) Contoh Kode Sederhana

### HTML:

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Contoh Positioning</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <div class="container">
      <div class="box">Box 1 (relative)</div>
      <div class="overlay">Overlay (absolute)</div>
    </div>
  </body>
</html>
```

### CSS (style.css):

```css
.container {
  position: relative; /* membuat containing block untuk .overlay */
  width: 300px;
  height: 150px;
  background: #f3f3f3;
  border: 1px solid #ccc;
}

.box {
  position: relative;
  padding: 12px;
  background: #fff;
}

.overlay {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgba(0,0,0,0.7);
  color: white;
  padding: 6px 8px;
  border-radius: 4px;
}
```

### Penjelasan Singkat:

`.overlay` akan diposisikan relatif terhadap `.container` karena `.container` memiliki `position: relative`. Tanpa posisi pada `.container`, `.overlay` akan terikat ke viewport (atau ancestor lain yang berposisi).

## 6) Kesalahan Umum & Tips Praktis

- Jangan terlalu sering gunakan `position: absolute` untuk layout utama — itu bisa membuat layout sulit dirawat dan tidak responsif
- Gunakan `position: relative` pada parent container sebagai "anchor" untuk elemen absolute di dalamnya
- Untuk sticky bekerja, pastikan elemen tidak berada di dalam container yang terlalu pendek dan beri nilai top
- Jika z-index tidak berfungsi, periksa apakah elemen berada di stacking context yang berbeda
- Gunakan Developer Tools di browser (Inspect Element) untuk melihat box model, posisi, dan ancestor yang memengaruhi

## 7) Latihan Singkat (Coba Sendiri)

- **Latihan 1:** Buat kotak 400x200, letakkan badge di pojok kanan atas menggunakan absolute. Badge harus tetap berada di pojok saat ukuran ikon berubah
- **Latihan 2:** Buat header yang sticky: ketika halaman digulir, header menempel di atas
- **Latihan 3:** Buat modal sederhana: overlay gelap fixed + kotak dialog di tengah halaman dengan absolute/fixed

### Contoh Solusi Singkat untuk Latihan 1:

```css
.parent { 
  position: relative; 
  width: 400px; 
  height: 200px; 
}

.badge { 
  position: absolute; 
  top: 8px; 
  right: 8px; 
}
```

## 8) Cara Melihat Hasil di Browser

- Buka file HTML yang relevan (mis. index.html) di browser
- Untuk pengembangan yang lebih nyaman, gunakan extension Live Server (VS Code) atau jalankan web server lokal sederhana
- Gunakan Inspect Element (klik kanan → Inspect) untuk memeriksa gaya dan posisi

## Sumber Belajar Lanjut

- [MDN Web Docs — Positioning](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- CSS-Tricks — A Complete Guide to Flexbox & Grid (untuk layout modern)
- YouTube tutorial (cari CSS positioning basics)

## Penutup

Semoga README ini membantu. Jika ada bagian yang ingin dijelaskan lebih rinci atau contoh tambahan yang diinginkan, beri tahu saja — dengan senang hati membantu lebih lanjut.

## Lisensi

Bebas digunakan untuk pembelajaran. Jika proyek ini akan dipublikasikan, tambahkan lisensi formal sesuai kebutuhan.

---

README dibuat untuk materi "7.2 CSS Positioning". Tetap semangat belajar! Salam hormat.
