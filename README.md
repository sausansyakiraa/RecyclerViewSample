# RecyclerView Sample - PAM (Pengembangan Aplikasi Mobile)

Aplikasi sampel Android berbasis Kotlin yang mengimplementasikan **RecyclerView** untuk menampilkan daftar item secara dinamis.

---

## 📌 Mengapa Blok Ungu (ActionBar / App Bar) Tidak Muncul?

Jika hasil tampilan aplikasi Anda **tidak memiliki blok ungu (ActionBar/Top App Bar)** di bagian atas layar seperti pada panduan modul, penyebab utamanya adalah **Tema (Theme) Bawaan Proyek**.

Pada templat Android Studio versi terbaru, tema default yang digunakan adalah:
```xml
parent="Theme.Material3.DayNight.NoActionBar"
```
Variasi `NoActionBar` secara otomatis menyembunyikan ActionBar/Toolbar di bagian atas layar.

### 🛠️ Solusi untuk Memunculkan Blok Ungu (ActionBar)

Ada 2 cara yang bisa dipilih:

#### Cara 1: Mengubah Tema Aplikasi di `themes.xml` (Rekomendasi Tercepat)
1. Buka file `app/src/main/res/values/themes.xml` dan `app/src/main/res/values-night/themes.xml`.
2. Ubah `NoActionBar` menjadi tema yang memiliki ActionBar, contohnya menggunakan **MaterialComponents** atau **AppCompat**:

   ```xml
   <resources xmlns:tools="http://schemas.android.com/tools">
       <!-- Ubah parent tema di bawah ini -->
       <style name="Base.Theme.RecyclerViewSample" parent="Theme.MaterialComponents.DayNight.DarkActionBar">
           <!-- Kustomisasi warna jika diperlukan -->
       </style>

       <style name="Theme.RecyclerViewSample" parent="Base.Theme.RecyclerViewSample" />
   </resources>
   ```

3. Jalankan kembali (*Re-run*) aplikasi. Blok ungu di bagian atas akan muncul secara otomatis.

---

#### Cara 2: Menambahkan `Toolbar` Manual di `activity_main.xml`
Jika ingin tetap memakai tema `NoActionBar` (Material 3), Anda bisa menambahkan `MaterialToolbar` atau `Toolbar` secara manual pada `res/layout/activity_main.xml`:

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- Top App Bar / Blok Ungu Manual -->
    <com.google.android.material.appbar.MaterialToolbar
        android:id="@+id/toolbar"
        android:layout_width="match_parent"
        android:layout_height="?attr/actionBarSize"
        android:background="?attr/colorPrimary"
        app:title="RecyclerViewSample"
        app:titleTextColor="@android:color/white"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <!-- RecyclerView di bawah Toolbar -->
    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/recyclerview"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        app:layout_constraintTop_toBottomOf="@id/toolbar"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        tools:itemCount="5"
        tools:listitem="@layout/card_view_design" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

---

## 📁 Struktur Proyek & Komponen Utama

- **`MainActivity.kt`**: Controller utama yang menginisialisasi `RecyclerView`, membuat 20 item data dummy, dan menyambungkan adapter.
- **`ItemsViewModel.kt`**: Model data sederhaan (`data class ItemsViewModel(val text: String)`).
- **`CustomAdapter.kt`**: Adapter kustom turunan `RecyclerView.Adapter` yang mengatur cara data dimasukkan ke dalam elemen tampilan.
- **`card_view_design.xml`**: Layout untuk tiap-tiap baris/kartu item di dalam list.
- **`activity_main.xml`**: Layout utama yang memuat komponen `RecyclerView`.

---

## 🚀 Cara Menjalankan Proyek

1. Buka proyek ini di **Android Studio**.
2. Pastikan emulator Android atau perangkat fisik (*physical device*) sudah terhubung.
3. Klik tombol **Run** (`Shift + F10` atau tombol hijau `Play`) di toolbar Android Studio.
