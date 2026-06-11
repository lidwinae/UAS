# Rangkuman Lengkap UAS Pengembangan Aplikasi Mobile Terapan

> Rangkuman belajar berdasarkan bagian **KISI KISI MATERI UAS** dan **40 latihan soal essay** pada modul dosen.

## Daftar Isi

- [Cara Menggunakan Rangkuman](#cara-menggunakan-rangkuman-ini)
- [Peta Besar Aplikasi Android Modern](#peta-besar-aplikasi-android-modern)
- [Bab 1: Jetpack Compose, State, dan Recomposition](#bab-1-jetpack-compose-state-dan-recomposition)
- [Bab 2: State Hoisting dan Stateless Composable](#bab-2-state-hoisting-dan-stateless-composable)
- [Bab 3: MVVM, ViewModel, Repository, dan UI State](#bab-3-mvvm-viewmodel-repository-dan-ui-state)
- [Bab 4: StateFlow, Lifecycle, dan Status UI](#bab-4-stateflow-lifecycle-dan-status-ui)
- [Bab 5: Coroutine, Dispatcher, dan viewModelScope](#bab-5-coroutine-dispatcher-dan-viewmodelscope)
- [Bab 6: Navigation Compose](#bab-6-navigation-compose)
- [Bab 7: Retrofit dan REST API](#bab-7-retrofit-dan-rest-api)
- [Bab 8: Supabase, RLS, dan JWT](#bab-8-supabase-rls-dan-jwt)
- [Bab 9: Room Database](#bab-9-room-database)
- [Bab 10: Lazy Layout dan Performa](#bab-10-lazy-layout-dan-performa)
- [Bank Jawaban 40 Soal](#bank-jawaban-40-soal-kisi-kisi)
- [Ringkasan Hafalan Terakhir](#ringkasan-hafalan-terakhir)

---

> **Fokus dokumen:** Disusun langsung dari bagian KISI KISI MATERI UAS dan 40 latihan essay pada modul dosen. Gunakan bagian materi inti untuk memahami konsep, lalu latih jawaban pada bagian bank soal.

## Cara Menggunakan Rangkuman Ini

1. Baca peta besar arsitektur agar setiap teknologi terlihat sebagai satu alur.
1. Pelajari 10 bab materi inti dan pahami alasan penggunaan setiap komponen.
1. Tutup materi, lalu jawab 40 soal essay dengan kalimat sendiri.
1. Bandingkan jawaban dengan jawaban model dan cek kata kuncinya.
1. Ulangi contoh kode pendek sampai dapat menulis pola dasarnya tanpa melihat.

### Peta Besar Aplikasi Android Modern

```kotlin
User action
    -> Composable UI mengirim event
    -> ViewModel menjalankan logika presentasi
    -> Repository memilih sumber data
    -> Retrofit / Supabase / Room memproses data
    -> ViewModel memperbarui StateFlow
    -> UI mengumpulkan state dengan collectAsStateWithLifecycle()
    -> perubahan state memicu recomposition pada bagian UI yang membaca state
```

> **Kalimat penghubung terpenting:** UI menampilkan state dan mengirim event; ViewModel mengelola state dan logika presentasi; Repository mengelola akses sumber data.

### Cakupan Kisi-Kisi

| Bab | Topik | Target pemahaman |
| --- | --- | --- |
| 1 | Compose dan State | State, remember, rememberSaveable, recomposition |
| 2 | State Hoisting | Stateless Composable, value dan callback |
| 3 | MVVM | View, ViewModel, Repository, UI pasif |
| 4 | UI State dan StateFlow | Immutable state, lifecycle-aware collection |
| 5 | Coroutine | suspend, dispatcher, viewModelScope, launch/async |
| 6 | Navigation | NavController, NavHost, route, back stack |
| 7 | Retrofit | REST, annotation, converter, interceptor |
| 8 | Supabase | RLS dan JWT |
| 9 | Room | Entity, DAO, Flow, Repository |
| 10 | Lazy Layout | LazyColumn, LazyRow, Grid, key, optimasi |

## BAB 1. Jetpack Compose, State, dan Recomposition

> **Inti bab:** Compose membangun UI secara deklaratif: tampilan merupakan hasil dari state saat ini.

### 1.1 UI Deklaratif dan @Composable

Jetpack Compose adalah toolkit UI modern Android berbasis Kotlin. Pada pendekatan deklaratif, developer mendeskripsikan seperti apa UI untuk suatu kondisi state, bukan mengubah View satu per satu secara imperatif.

```kotlin
@Composable
fun Greeting(name: String) {
    Text(text = "Halo, $name")
}
```

- @Composable menandai fungsi yang dapat ikut membentuk UI Compose.
- Composable dapat menerima parameter dan memanggil Composable lain.
- Fungsi Composable dapat dijalankan ulang; karena itu hindari side effect sembarangan.

### 1.2 State

State adalah data yang memengaruhi hasil tampilan. Contohnya teks input, jumlah item, status loading, pesan error, atau data produk. Compose mengamati state yang dibaca oleh Composable. Ketika nilainya berubah, Compose menjadwalkan pembaruan UI.

```kotlin
var count by remember { mutableStateOf(0) }
Text("Count: $count")
```

### 1.3 Mengapa Variabel Biasa Tidak Tepat

Variabel lokal biasa tidak observable oleh Compose dan dapat dibuat ulang ketika fungsi Composable direkomposisi. Mengubah var count = 0 juga tidak otomatis memberi tahu Compose bahwa UI harus digambar ulang.

| Bentuk | Sifat | Dampak |
| --- | --- | --- |
| var count = 0 | Bukan state observable | UI tidak terjamin ikut diperbarui |
| remember { mutableStateOf(0) } | State observable selama composition | Perubahan nilai dapat memicu recomposition |

### 1.4 remember dan rememberSaveable

remember mempertahankan objek atau state selama Composable masih berada dalam composition. rememberSaveable menambahkan penyimpanan untuk state yang dapat disimpan, sehingga umumnya bertahan ketika Activity dibuat ulang akibat perubahan konfigurasi seperti rotasi.

| Aspek | remember | rememberSaveable |
| --- | --- | --- |
| Recomposition | Bertahan | Bertahan |
| Configuration change | Umumnya hilang | Dapat dipulihkan |
| Cocok untuk | State UI sementara | Input sederhana yang perlu dipertahankan |
| Batasan | Terikat composition | Tipe harus saveable atau memakai Saver |

### 1.5 Recomposition

Recomposition adalah eksekusi ulang Composable yang membaca state berubah untuk menghasilkan UI terbaru. Ini bukan restart aplikasi dan tidak selalu menjalankan ulang seluruh layar. Compose berusaha memperbarui bagian yang relevan.

- State dibaca oleh Composable.
- Nilai state berubah.
- Compose menandai pembaca state untuk direkomposisi.
- UI baru dihitung dan perubahan diterapkan secara efisien.

> **Kesalahan umum:** Jangan menjalankan request API langsung di badan Composable tanpa pengendalian side effect, karena recomposition dapat menyebabkan pemanggilan berulang.

## BAB 2. State Hoisting dan Stateless Composable

> **Inti bab:** State dipindahkan ke pemilik yang tepat agar komponen anak hanya menerima value dan mengirim event.

### 2.1 Prinsip State Hoisting

State hoisting berarti menaikkan state dari Composable anak ke parent atau state holder. Pola umumnya adalah value turun ke anak, sedangkan event naik ke parent.

```kotlin
State turun sebagai value
Event naik sebagai callback
```

### 2.2 Pola value dan onValueChange

```kotlin
@Composable
fun NameInput(
    value: String,
    onValueChange: (String) -> Unit
) {
    TextField(
        value = value,
        onValueChange = onValueChange
    )
}

@Composable
fun FormScreen() {
    var name by rememberSaveable { mutableStateOf("") }
    NameInput(
        value = name,
        onValueChange = { name = it }
    )
}
```

### 2.3 Stateless dan Stateful

| Jenis | Ciri | Kegunaan |
| --- | --- | --- |
| Stateless | Tidak memiliki state internal utama; menerima value dan callback | Reusable, mudah diuji, mudah dipreview |
| Stateful | Memiliki atau mengambil state | Bertindak sebagai state holder dan menghubungkan ViewModel |

### 2.4 Keuntungan

- Single source of truth: satu pemilik menentukan nilai state.
- Reusable: anak dapat dipakai dengan sumber state berbeda.
- Testable: output dan callback dapat diuji tanpa menyiapkan banyak state internal.
- Kontrol parent lebih jelas, termasuk validasi dan koordinasi beberapa field.
- Lebih mudah dihubungkan dengan ViewModel dan UI state.

> **Rumus jawaban essay:** Definisikan pemindahan state, jelaskan value turun dan event naik, lalu sebutkan manfaat reusable, testable, dan single source of truth.

## BAB 3. MVVM, ViewModel, Repository, dan UI State

> **Inti bab:** MVVM memisahkan tampilan, pengelolaan state/logika presentasi, dan akses sumber data.

### 3.1 Tanggung Jawab Setiap Lapisan

| Lapisan | Tanggung jawab | Tidak seharusnya |
| --- | --- | --- |
| View / Compose | Menampilkan state dan mengirim event | Query database atau request API langsung |
| ViewModel | Mengelola UI state dan logika presentasi | Menyimpan referensi Activity |
| Repository | Mengelola dan mengabstraksi sumber data | Mengatur detail tampilan |
| Data source | Retrofit, Supabase, Room, cache | Menentukan perilaku UI |

### 3.2 ViewModel

- Menyimpan state layar selama lifecycle ViewModel.
- Menangani event seperti login, refresh, simpan, dan hapus.
- Memanggil Repository untuk memperoleh atau mengubah data.
- Mengubah hasil data menjadi UI state: loading, success, error.
- Bertahan terhadap configuration change selama scope pemiliknya sama.
```kotlin
@Composable
fun LoginRoute(
    viewModel: LoginViewModel = viewModel()
) {
    val uiState by viewModel.uiState.collectAsStateWithLifecycle()
    LoginScreen(
        uiState = uiState,
        onLogin = viewModel::login
    )
}
```

### 3.3 Repository Tetap Diperlukan

ViewModel tidak sebaiknya mengetahui detail apakah data berasal dari Retrofit, Room, Supabase, atau cache. Repository menjadi mediator dan menyediakan API data yang stabil. Pemisahan ini memudahkan pengujian, penggantian sumber data, caching, dan penerapan offline-first.

```kotlin
Composable -> ViewModel -> Repository -> Retrofit / Supabase / Room
```

### 3.4 UI Layer Pasif

Activity, Fragment, atau Composable idealnya fokus pada rendering dan event. Jika UI mengakses Repository atau Retrofit langsung, coupling meningkat, lifecycle lebih sulit dikelola, pengujian menjadi berat, dan logika mudah tersebar.

### 3.5 UI State Terpusat

```kotlin
data class LoginUiState(
    val email: String = "",
    val password: String = "",
    val isLoading: Boolean = false,
    val errorMessage: String? = null,
    val isLoggedIn: Boolean = false
)
```

- Satu snapshot menggambarkan kondisi layar secara konsisten.
- Lebih mudah melakukan update immutable dengan copy().
- Loading, data, error, dan input tidak tersebar dalam banyak variabel.
- Testing cukup membandingkan state sebelum dan sesudah event.

## BAB 4. StateFlow, Lifecycle, dan Status UI

> **Inti bab:** StateFlow menyimpan nilai state terbaru dan mengalirkannya secara reaktif dari ViewModel ke UI.

### 4.1 MutableStateFlow Private, StateFlow Public

```kotlin
private val _uiState = MutableStateFlow(LoginUiState())
val uiState: StateFlow<LoginUiState> = _uiState

fun setLoading(value: Boolean) {
    _uiState.value = _uiState.value.copy(isLoading = value)
}
```

MutableStateFlow dibuat private untuk menjaga enkapsulasi. Hanya ViewModel yang boleh mengubah state, sedangkan UI menerima StateFlow read-only. Dengan demikian alur perubahan state dapat diprediksi dan tidak ada komponen luar yang mengubah state secara sembarangan.

### 4.2 Update dengan copy() atau update

```kotlin
_uiState.value = _uiState.value.copy(isLoading = true)

// Alternatif yang aman untuk pembaruan atomik:
_uiState.update { current ->
    current.copy(errorMessage = null)
}
```

### 4.3 collectAsStateWithLifecycle()

Di Compose, collectAsStateWithLifecycle() mengubah Flow/StateFlow menjadi State Compose dan mengoleksi data sesuai lifecycle. Ketika UI tidak berada pada lifecycle aktif yang ditentukan, koleksi dapat dihentikan sehingga lebih hemat dan aman.

```kotlin
val uiState by viewModel.uiState.collectAsStateWithLifecycle()
```

### 4.4 Memodelkan Loading, Success, Error

```kotlin
sealed interface ProductUiState {
    data object Loading : ProductUiState
    data class Success(val products: List<Product>) : ProductUiState
    data class Error(val message: String) : ProductUiState
}
```

- Sealed type membatasi kemungkinan status sehingga when dapat dibuat exhaustive.
- Data class UI state cocok bila satu layar memiliki banyak properti yang hidup bersamaan.
- Sealed status cocok ketika layar berada pada salah satu kondisi eksklusif.

## BAB 5. Coroutine, Dispatcher, dan viewModelScope

> **Inti bab:** Coroutine menjalankan pekerjaan asynchronous tanpa memblokir main thread.

### 5.1 Konsep Dasar Coroutine

Coroutine adalah unit kerja ringan yang dapat ditangguhkan dan dilanjutkan. Coroutine membantu menulis kode asynchronous dengan gaya sekuensial untuk request network, query database, upload/download, dan pekerjaan background.

### 5.2 Dispatcher

| Dispatcher | Kegunaan utama | Contoh |
| --- | --- | --- |
| Main | Interaksi dan pembaruan UI | Mengubah state yang dirender UI |
| IO | Operasi blocking I/O | File, database blocking, network blocking |
| Default | Perhitungan berat berbasis CPU | Sorting besar, parsing berat |
| Unconfined | Kasus khusus; jarang dipakai | Bukan pilihan default aplikasi |

> **Catatan penting:** Fungsi suspend Retrofit dan Room umumnya sudah mengelola thread yang tepat. Dispatchers.IO terutama diperlukan ketika Anda membungkus operasi blocking sendiri.

### 5.3 viewModelScope

```kotlin
fun loadProducts() {
    viewModelScope.launch {
        _uiState.value = ProductUiState.Loading
        _uiState.value = try {
            ProductUiState.Success(repository.getProducts())
        } catch (e: Exception) {
            ProductUiState.Error(e.message ?: "Terjadi kesalahan")
        }
    }
}
```

Coroutine dalam viewModelScope otomatis dibatalkan ketika ViewModel di-clear. Hal ini mengurangi pekerjaan sia-sia dan risiko leak. Scope juga membuat kepemilikan pekerjaan asynchronous jelas.

### 5.4 suspend

Keyword suspend menandai fungsi yang dapat menangguhkan coroutine tanpa memblokir thread. suspend bukan berarti fungsi otomatis berjalan di background; konteks eksekusinya tetap ditentukan oleh coroutine dan implementasi fungsi.

### 5.5 launch vs async

| Builder | Hasil | Gunakan ketika |
| --- | --- | --- |
| launch | Job | Menjalankan pekerjaan tanpa membutuhkan nilai langsung |
| async | Deferred<T> | Menjalankan pekerjaan yang hasilnya akan di-await |

> **Kesalahan umum:** Jangan memakai async hanya untuk memanggil satu fungsi lalu langsung await; pemanggilan suspend biasa lebih sederhana. async bermanfaat untuk pekerjaan paralel.

## BAB 6. Navigation Compose

> **Inti bab:** Navigation Compose mengelola destination, route, perpindahan layar, dan back stack.

### 6.1 NavController, NavHost, dan Route

| Komponen | Fungsi |
| --- | --- |
| NavController | Menjalankan navigate, popBackStack, dan mengelola back stack |
| NavHost | Wadah graph yang memetakan route ke Composable destination |
| Route | Identifier destination, dapat memiliki argumen |
| Back stack | Tumpukan destination yang merekam riwayat navigasi |

```kotlin
val navController = rememberNavController()

NavHost(
    navController = navController,
    startDestination = "login"
) {
    composable("login") { LoginScreen() }
    composable("home") { HomeScreen() }
    composable("detail/{id}") { backStackEntry ->
        val id = backStackEntry.arguments?.getString("id")
        DetailScreen(id = id)
    }
}
```

### 6.2 Menghapus Login dari Back Stack

```kotlin
navController.navigate("home") {
    popUpTo("login") {
        inclusive = true
    }
    launchSingleTop = true
}
```

popUpTo menentukan destination sampai titik mana back stack dibersihkan. inclusive = true juga menghapus destination login itu sendiri, sehingga tombol Back tidak kembali ke layar login setelah autentikasi berhasil.

### 6.3 Argumen Route

Kirim data kecil dan stabil seperti id, bukan seluruh object kompleks. Object dapat besar, sulit dienkode, berisiko melewati batas ukuran, dan mudah menjadi tidak sinkron. Destination penerima sebaiknya mengambil data terbaru berdasarkan id melalui ViewModel dan Repository.

```kotlin
navController.navigate("detail/${product.id}")
```

## BAB 7. Retrofit dan REST API

> **Inti bab:** Retrofit mengubah deklarasi interface Kotlin menjadi client HTTP untuk REST API.

### 7.1 Operasi REST dan Interface Retrofit

- GET mengambil resource.
- POST membuat atau mengirim resource.
- PUT/PATCH memperbarui resource.
- DELETE menghapus resource.
```kotlin
interface UserApi {
    @GET("users")
    suspend fun getUsers(): List<User>

    @GET("users/{id}")
    suspend fun getUser(@Path("id") id: Int): User

    @POST("users")
    suspend fun createUser(@Body user: User): User
}
```

### 7.2 Annotation Penting

| Annotation | Fungsi |
| --- | --- |
| @Body | Menjadikan object sebagai request body, biasanya JSON |
| @Path | Mengganti placeholder pada URL path |
| @Query | Menambahkan query parameter pada URL |
| @Header | Mengirim header tertentu untuk satu request |

### 7.3 GsonConverterFactory

Converter melakukan serialisasi object Kotlin menjadi JSON untuk request dan deserialisasi JSON response menjadi data class Kotlin. Tanpa converter yang sesuai, Retrofit tidak mengetahui cara memetakan body JSON ke object aplikasi.

```kotlin
val retrofit = Retrofit.Builder()
    .baseUrl("https://api.example.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .client(okHttpClient)
    .build()
```

### 7.4 Authorization Interceptor

```kotlin
val client = OkHttpClient.Builder()
    .addInterceptor { chain ->
        val request = chain.request().newBuilder()
            .addHeader("Authorization", "Bearer $token")
            .build()
        chain.proceed(request)
    }
    .build()
```

Interceptor cocok untuk header yang harus dikirim konsisten pada banyak endpoint. Token sebaiknya diperoleh dari penyimpanan/session provider yang terkontrol, bukan ditulis permanen di source code.

### 7.5 Integrasi dengan MVVM dan Coroutine

```kotlin
UI event
    -> ViewModel: viewModelScope.launch
    -> Repository: getUsers()
    -> Retrofit API: suspend fun getUsers()
    -> hasil / error
    -> ViewModel memperbarui StateFlow
    -> Compose merender state terbaru
```

> **Rotasi dan request ulang:** Jangan memicu fetch tanpa pengendalian dari badan Composable. Simpan hasil di ViewModel dan panggil fetch dari init atau side effect dengan key yang benar.

## BAB 8. Supabase, RLS, dan JWT

> **Inti bab:** Keamanan client langsung ke Supabase bergantung pada autentikasi JWT dan kebijakan Row Level Security.

### 8.1 Alur Keamanan

```kotlin
Android client mengirim request + JWT
    -> Supabase memverifikasi identitas/claim
    -> RLS policy mengevaluasi operasi dan baris
    -> akses diizinkan atau ditolak
```

JWT membawa identitas dan claim user yang telah login. RLS adalah aturan pada database yang menentukan baris mana yang boleh dibaca, ditambah, diubah, atau dihapus oleh user tersebut. Kunci anon bukan rahasia yang menggantikan RLS; keamanan harus ditegakkan oleh policy database.

- Aktifkan RLS pada tabel yang diakses client.
- Buat policy SELECT, INSERT, UPDATE, dan DELETE sesuai kebutuhan.
- Gunakan identitas user, misalnya auth.uid(), dalam policy kepemilikan data.
- Jangan menaruh service role key di aplikasi Android.
- Validasi hak akses di server/database, bukan hanya menyembunyikan tombol di UI.

## BAB 9. Room Database

> **Inti bab:** Room menyediakan abstraksi SQLite yang type-safe melalui Entity, DAO, dan RoomDatabase.

### 9.1 Komponen Utama

| Komponen | Fungsi |
| --- | --- |
| Entity | Mendefinisikan tabel dan kolom melalui data class |
| DAO | Mendefinisikan operasi query, insert, update, delete |
| RoomDatabase | Titik akses database dan DAO |
| Repository | Menyediakan data Room kepada ViewModel dan dapat menggabungkan network |

```kotlin
@Entity(tableName = "user_table")
data class UserEntity(
    @PrimaryKey(autoGenerate = true)
    val id: Int = 0,
    val name: String
)

@Dao
interface UserDao {
    @Query("SELECT * FROM user_table ORDER BY name")
    fun observeUsers(): Flow<List<UserEntity>>

    @Insert
    suspend fun insert(user: UserEntity)
}
```

### 9.2 @Query dan Flow

@Query berisi SQL kustom dan diverifikasi Room saat kompilasi. Jika query mengembalikan Flow, Room dapat memancarkan daftar baru ketika tabel terkait berubah. Fungsi Flow tidak perlu suspend karena hasilnya adalah stream asynchronous; operasi satu kali seperti insert biasanya suspend.

### 9.3 TypeConverter

SQLite hanya mendukung tipe dasar tertentu. TypeConverter mengubah tipe seperti Date, enum, atau object menjadi tipe yang dapat disimpan, lalu mengembalikannya ketika dibaca.

```kotlin
class Converters {
    @TypeConverter
    fun fromDate(value: Date?): Long? = value?.time

    @TypeConverter
    fun toDate(value: Long?): Date? = value?.let(::Date)
}
```

### 9.4 Inisialisasi dan Scope

Database sebaiknya berupa singleton berbasis application context. Dengan demikian instance tidak terikat pada satu Activity dan tidak dibuat berulang. Dependency Injection dapat menyediakan database, DAO, Repository, dan ViewModel secara konsisten.

```kotlin
DAO -> Repository -> ViewModel -> StateFlow -> Compose UI
```

## BAB 10. Lazy Layout dan Performa

> **Inti bab:** Lazy layout hanya menyusun item yang diperlukan viewport sehingga cocok untuk data berjumlah banyak.

### 10.1 Memilih Komponen

| Komponen | Arah / bentuk | Contoh |
| --- | --- | --- |
| LazyColumn | Daftar vertikal | Feed, daftar transaksi |
| LazyRow | Daftar horizontal | Kategori produk, carousel |
| LazyVerticalGrid | Grid yang scroll vertikal | Katalog produk |
| LazyHorizontalGrid | Grid yang scroll horizontal | Koleksi berbasis baris |

### 10.2 item(), items(), dan key

```kotlin
LazyColumn {
    item {
        Text("Daftar Produk")
    }
    items(
        items = products,
        key = { product -> product.id }
    ) { product ->
        ProductCard(product)
    }
}
```

item() menambahkan satu elemen khusus, sedangkan items() mengulang koleksi. key yang stabil membantu Compose mempertahankan identitas item ketika daftar berubah, sehingga state item dan animasi lebih benar serta recomposition lebih efisien.

### 10.3 Grid Adaptif dan Arrangement

```kotlin
LazyVerticalGrid(
    columns = GridCells.Adaptive(minSize = 160.dp),
    horizontalArrangement = Arrangement.spacedBy(8.dp),
    verticalArrangement = Arrangement.spacedBy(8.dp)
) {
    items(products, key = { it.id }) { product ->
        ProductCard(product)
    }
}
```

### 10.4 UI State di Lazy Layout

```kotlin
when (val state = uiState) {
    ProductUiState.Loading -> CircularProgressIndicator()
    is ProductUiState.Success -> LazyColumn {
        items(state.products, key = { it.id }) {
            ProductCard(it)
        }
    }
    is ProductUiState.Error -> Text(state.message)
}
```

### 10.5 Optimasi dan Infinite Scroll

- Pindahkan kalkulasi berat dan format data dari item Composable ke ViewModel.
- Gunakan key stabil, bukan posisi indeks jika item dapat berubah urutan.
- Pantau posisi list dengan derivedStateOf dan trigger fetch melalui side effect.
- Jangan memanggil ViewModel langsung dari dalam blok items() untuk setiap item.
- Hindari LazyVerticalGrid di dalam Column.verticalScroll karena dapat menghasilkan unbounded height.
- Gunakan arrangement untuk jarak konsisten daripada margin manual pada setiap item.

## BANK JAWABAN 40 SOAL KISI-KISI

> **Cara berlatih:** Jawab dengan pola definisi -> alasan/mekanisme -> contoh atau dampak. Jawaban model berikut dapat dipersingkat saat ujian, tetapi kata kuncinya jangan hilang.

### A. Jetpack Compose, State, dan Recomposition

#### 1. Mengapa var count = 0 kurang tepat untuk perubahan UI?

Variabel lokal biasa bukan state observable Compose. Nilainya dapat dibuat ulang saat recomposition dan perubahan nilainya tidak otomatis memberi tahu Compose untuk memperbarui UI. Gunakan mutableStateOf yang diingat dengan remember atau rememberSaveable agar perubahan dapat diamati dan UI yang membaca nilai tersebut direkomposisi.

**Kata kunci:** bukan observable, dibuat ulang, mutableStateOf, recomposition

#### 2. Apa fungsi remember bersama mutableStateOf?

mutableStateOf membuat wadah state yang dapat diamati Compose, sedangkan remember mempertahankan wadah tersebut selama Composable masih berada dalam composition. Kombinasi keduanya membuat nilai tidak kembali ke nilai awal pada setiap recomposition dan perubahan nilai memicu pembaruan UI yang membacanya.

**Kata kunci:** state observable, bertahan dalam composition

```kotlin
var count by remember { mutableStateOf(0) }
```

#### 3. Apa perbedaan remember dan rememberSaveable?

Keduanya mempertahankan state saat recomposition. remember umumnya hilang ketika Activity dibuat ulang, sedangkan rememberSaveable menyimpan state yang saveable agar dapat dipulihkan pada configuration change seperti rotasi. rememberSaveable cocok untuk input sederhana; object kompleks membutuhkan Saver atau sebaiknya dikelola ViewModel.

**Kata kunci:** recomposition, configuration change, saveable

#### 4. Apa yang dimaksud recomposition?

Recomposition adalah proses Compose menjalankan ulang Composable yang bergantung pada state berubah untuk menghitung dan menampilkan UI terbaru. Proses ini bukan restart seluruh aplikasi; Compose berusaha memperbarui hanya bagian yang relevan.

**Kata kunci:** state berubah, Composable dijalankan ulang, bukan restart

#### 5. Bagaimana hubungan state dan recomposition?

Composable mencatat state yang dibacanya. Ketika nilai state tersebut berubah, Compose menjadwalkan recomposition pada pembacanya. Hasil Composable dihitung kembali dan perubahan UI diterapkan. Karena itu state menjadi sumber kebenaran tampilan.

**Kata kunci:** state dibaca, perubahan memicu recomposition, source of truth

### B. State Hoisting dan Stateless Composable

#### 6. Apa yang dimaksud state hoisting?

State hoisting adalah memindahkan state ke parent atau state holder agar anak menerima nilai melalui parameter dan mengirim perubahan melalui callback. Polanya adalah state turun sebagai value dan event naik sebagai callback.

**Kata kunci:** parent, value turun, event naik, single source of truth

#### 7. Bagaimana penerapan state hoisting pada input teks?

Parent menyimpan teks, kemudian memberikan value dan onValueChange kepada Composable input. Anak menampilkan value dan meneruskan input user melalui callback tanpa menyimpan state utama sendiri.

**Kata kunci:** value, onValueChange, parent menyimpan state

```kotlin
fun NameInput(value: String, onValueChange: (String) -> Unit) {
    TextField(value = value, onValueChange = onValueChange)
}
```

#### 8. Apa yang dimaksud Stateless Composable?

Stateless Composable adalah Composable yang tidak memiliki state internal utama untuk perilakunya. Nilai ditentukan oleh parameter dan aksi user dikirim melalui callback, sehingga parent atau ViewModel menjadi pemilik state.

**Kata kunci:** tanpa state internal utama, parameter, callback

#### 9. Apa keuntungan Composable stateless?

Composable menjadi lebih reusable, mudah diuji, mudah dipreview, lebih fleksibel, dan mudah dikontrol parent. State juga memiliki single source of truth sehingga sinkronisasi antarkomponen lebih sederhana.

**Kata kunci:** reusable, testable, fleksibel, single source of truth

### C. MVVM, ViewModel, Repository, dan UI State

#### 10. Apa tugas utama ViewModel dalam MVVM?

ViewModel mengelola UI state dan logika presentasi, memproses event user, memanggil Repository, serta mengubah hasil menjadi kondisi loading, success, atau error. ViewModel bertahan terhadap configuration change dan tidak seharusnya memegang referensi langsung ke Activity.

**Kata kunci:** UI state, logika presentasi, Repository, configuration change

#### 11. Bagaimana mengambil ViewModel di Composable?

Cara umum adalah menggunakan viewModel() dari lifecycle-viewmodel-compose. Jika proyek memakai Hilt, gunakan hiltViewModel(). ViewModel kemudian sebaiknya diambil pada Route/screen tingkat atas dan state serta callback diteruskan ke Composable stateless.

**Kata kunci:** viewModel(), hiltViewModel(), Route

```kotlin
val viewModel: LoginViewModel = viewModel()
```

#### 12. Bagaimana UI berkomunikasi dengan ViewModel?

UI membaca state read-only dari ViewModel dan mengirim event melalui fungsi atau callback, misalnya onLoginClick(). UI tidak mengubah MutableStateFlow dan tidak mengakses database langsung. Alur satu arah ini membuat perubahan state mudah dilacak.

**Kata kunci:** UI membaca state, mengirim event, unidirectional data flow

#### 13. Mengapa Repository diperlukan walaupun ada ViewModel?

Repository memisahkan detail akses data dari ViewModel dan menjadi mediator untuk Retrofit, Supabase, Room, cache, atau DataStore. Repository mengurangi coupling, memudahkan testing dan penggantian sumber data, serta menjaga separation of concerns.

**Kata kunci:** abstraksi sumber data, mediator, separation of concerns

#### 14. Mengapa Activity/Fragment tidak langsung mengakses Repository atau Retrofit?

UI layer seharusnya fokus menampilkan state dan menangani event. Akses data langsung membuat UI terlalu banyak tanggung jawab, coupling tinggi, lifecycle sulit dikelola, dan testing lebih sulit. Akses data sebaiknya melalui ViewModel lalu Repository.

**Kata kunci:** UI pasif, coupling, ViewModel -> Repository

#### 15. Apa manfaat LoginUiState?

LoginUiState menyatukan seluruh kondisi layar seperti email, password, loading, error, dan status login dalam satu snapshot immutable. State terpusat mencegah nilai tidak konsisten, mudah di-copy untuk pembaruan, mudah diamati, dan mudah diuji.

**Kata kunci:** snapshot UI, immutable, copy(), mudah diuji

### D. StateFlow, Lifecycle, dan Coroutine

#### 16. Mengapa StateFlow cocok untuk state ViewModel?

StateFlow selalu memiliki dan menyimpan nilai terbaru, dapat diamati secara reaktif, dan cocok diekspos sebagai state read-only. Collector baru langsung menerima nilai terakhir sehingga UI dapat merender kondisi terkini.

**Kata kunci:** nilai terbaru, reaktif, hot flow

#### 17. Mengapa MutableStateFlow dibuat private?

Agar hanya ViewModel yang dapat mengubah state. UI menerima StateFlow read-only, sehingga enkapsulasi terjaga, alur data satu arah, dan perubahan state tidak dilakukan sembarangan dari luar ViewModel.

**Kata kunci:** enkapsulasi, read-only, satu arah

#### 18. Bagaimana memperbarui StateFlow?

Untuk data class, ambil state lama lalu gunakan copy() untuk mengganti properti tertentu, atau gunakan update untuk pembaruan atomik. Cara ini mempertahankan properti lain dan menghasilkan snapshot baru.

**Kata kunci:** copy(), update, immutable snapshot

```kotlin
_uiState.update { it.copy(isLoading = true) }
```

#### 19. Apa fungsi collectAsStateWithLifecycle()?

Fungsi ini mengoleksi Flow/StateFlow sebagai State Compose dengan memperhatikan lifecycle. UI hanya aktif mengoleksi ketika berada pada lifecycle yang sesuai, sehingga mengurangi pekerjaan yang tidak perlu dan lebih aman daripada koleksi yang mengabaikan lifecycle.

**Kata kunci:** Flow menjadi State Compose, lifecycle-aware, hemat resource

#### 20. Untuk apa coroutine digunakan?

Coroutine digunakan untuk pekerjaan asynchronous atau lama seperti network request, query database, upload/download, dan proses background tanpa memblokir main thread. Hasilnya UI tetap responsif.

**Kata kunci:** asynchronous, tidak memblokir main thread, network/database

#### 21. Dispatcher apa untuk database atau network?

Dispatchers.IO digunakan untuk operasi input/output yang blocking seperti file, database blocking, atau network blocking. Namun fungsi suspend Retrofit dan Room biasanya telah mengelola eksekusi thread internal, sehingga tidak selalu perlu membungkus semuanya dengan withContext(IO).

**Kata kunci:** Dispatchers.IO, blocking I/O

#### 22. Mengapa memakai viewModelScope?

viewModelScope mengikat coroutine pada lifecycle ViewModel. Coroutine otomatis dibatalkan saat ViewModel di-clear, sehingga kepemilikan pekerjaan jelas, mencegah pekerjaan sia-sia, dan mengurangi risiko leak.

**Kata kunci:** lifecycle ViewModel, otomatis dibatalkan, structured concurrency

#### 23. Apa arti keyword suspend?

suspend menandai fungsi yang dapat menangguhkan eksekusi coroutine dan dilanjutkan kemudian tanpa memblokir thread. Fungsi suspend harus dipanggil dari coroutine atau fungsi suspend lain dan tidak otomatis berarti berjalan pada background thread.

**Kata kunci:** menangguhkan, tidak memblokir, dipanggil dari coroutine

#### 24. Apa perbedaan launch dan async?

launch mengembalikan Job dan cocok untuk menjalankan pekerjaan yang tidak memerlukan nilai langsung. async mengembalikan Deferred<T> dan dipakai ketika hasil perlu diambil dengan await(), terutama untuk pekerjaan paralel. Keduanya tetap harus berada dalam scope yang terstruktur.

**Kata kunci:** Job, Deferred, await

### E. Navigation Compose

#### 25. Apa fungsi NavController?

NavController mengelola aksi navigasi dan back stack. Melalui objek ini aplikasi memanggil navigate(), popBackStack(), dan opsi seperti popUpTo.

**Kata kunci:** navigate, back stack, popBackStack

#### 26. Apa fungsi NavHost?

NavHost adalah wadah graph navigasi yang menghubungkan NavController, startDestination, dan daftar composable destination. Ia menentukan Composable mana yang ditampilkan untuk route aktif.

**Kata kunci:** navigation graph, startDestination, destination

#### 27. Contoh route sederhana?

Route sederhana berupa string identifier seperti home. Route tersebut didaftarkan pada composable di dalam NavHost, lalu dibuka dengan navController.navigate("home").

**Kata kunci:** string route, composable, navigate

```kotlin
composable("home") { HomeScreen() }
```

#### 28. Bagaimana login ke home tanpa kembali ke login?

Navigasikan ke home sambil menghapus login dari back stack menggunakan popUpTo("login") dan inclusive = true. Setelah itu tombol Back tidak menemukan login sebagai destination sebelumnya.

**Kata kunci:** popUpTo, inclusive = true, hapus back stack

```kotlin
navController.navigate("home") {
    popUpTo("login") { inclusive = true }
}
```

#### 29. Apa yang dimaksud back stack?

Back stack adalah tumpukan riwayat destination. Destination terbaru berada di atas. Ketika tombol Back ditekan, destination teratas dikeluarkan dan aplikasi kembali ke destination sebelumnya.

**Kata kunci:** tumpukan riwayat, LIFO, tombol Back

#### 30. Mengapa object kompleks tidak dikirim langsung lewat route?

Object kompleks sulit dienkode, dapat besar, berisiko melewati batas ukuran, dan dapat menjadi stale. Route lebih aman membawa identifier sederhana; destination penerima mengambil data terbaru dari Repository atau database berdasarkan id.

**Kata kunci:** kirim id, ukuran, data terbaru

### F. Retrofit, REST API, dan Supabase

#### 31. Apa fungsi utama Retrofit?

Retrofit adalah HTTP client type-safe yang memudahkan konsumsi REST API dengan mendefinisikan endpoint sebagai interface Kotlin. Retrofit menangani pembuatan request, parameter, body, dan konversi response melalui converter.

**Kata kunci:** HTTP client, REST API, interface Kotlin

#### 32. Annotation apa untuk JSON request body POST?

@Body digunakan pada parameter fungsi Retrofit. Converter kemudian melakukan serialisasi object Kotlin menjadi JSON request body.

**Kata kunci:** @Body, serialisasi, POST

```kotlin
@POST("users")
suspend fun create(@Body user: User): User
```

#### 33. Apa fungsi @Path("id")?

@Path mengganti placeholder {id} pada URL endpoint dengan nilai parameter saat request dibuat. Misalnya id 5 menghasilkan URL users/5.

**Kata kunci:** placeholder URL, dinamis

```kotlin
@GET("users/{id}")
suspend fun getUser(@Path("id") id: Int): User
```

#### 34. Apa fungsi GsonConverterFactory?

GsonConverterFactory mengonversi JSON response menjadi object/data class Kotlin dan object Kotlin menjadi JSON request bila diperlukan. Converter menghubungkan format body HTTP dengan model aplikasi.

**Kata kunci:** serialisasi, deserialisasi, JSON

#### 35. Mengapa fungsi Retrofit bersama coroutine memakai suspend?

suspend memungkinkan request dipanggil secara natural dari coroutine tanpa memblokir thread pemanggil. Coroutine dapat ditangguhkan sampai response tersedia lalu dilanjutkan untuk memproses hasil atau error.

**Kata kunci:** coroutine, non-blocking, response

#### 36. Bagaimana Supabase menjaga keamanan akses client Android?

Supabase memverifikasi JWT untuk mengetahui identitas dan claim user, kemudian Row Level Security mengevaluasi policy pada setiap operasi dan baris. Akses hanya diberikan jika policy mengizinkan. Service role key tidak boleh ditanam di aplikasi client.

**Kata kunci:** JWT, RLS, policy, jangan pakai service role key

#### 37. Di mana API Service Retrofit dikelola dalam MVVM?

API Service dikelola pada data layer, biasanya disediakan melalui dependency injection dan digunakan oleh Repository. ViewModel hanya memanggil fungsi Repository, sedangkan UI tidak mengetahui detail Retrofit.

**Kata kunci:** data layer, Repository, dependency injection

### G. Room dan Lazy Layout

#### 38. Apa fungsi Entity dalam Room?

Entity mendefinisikan struktur tabel Room melalui data class: nama tabel, kolom, primary key, index, dan relasi tertentu. Setiap instance Entity mewakili satu baris data.

**Kata kunci:** tabel, data class, primary key, baris

#### 39. Apa fungsi @Query pada DAO?

@Query mendefinisikan SQL kustom untuk operasi baca atau perubahan data pada DAO. Room memeriksa sintaks dan kecocokan hasil query saat kompilasi, sehingga banyak kesalahan ditemukan lebih awal.

**Kata kunci:** SQL kustom, DAO, compile-time verification

#### 40. Lazy Layout apa untuk kategori produk horizontal?

Gunakan LazyRow karena ia menyusun daftar secara horizontal dan hanya mengomposisi item yang diperlukan viewport. Data sebaiknya berasal dari UI state dan item menggunakan key stabil bila memiliki id.

**Kata kunci:** LazyRow, horizontal, lazy composition

## RINGKASAN HAFALAN TERAKHIR

| Jika ditanya... | Jawaban inti |
| --- | --- |
| State Compose | mutableStateOf menyimpan state observable; perubahan memicu recomposition |
| remember | Mempertahankan state selama composition |
| rememberSaveable | Memulihkan state saveable setelah configuration change |
| State hoisting | State di parent; value turun, event naik |
| ViewModel | Mengelola UI state dan logika presentasi |
| Repository | Mediator dan abstraksi sumber data |
| StateFlow | Menyimpan nilai terbaru dan dipantau secara reaktif |
| viewModelScope | Coroutine mengikuti lifecycle ViewModel |
| Navigation | NavController mengelola navigasi; NavHost memetakan route |
| Retrofit | HTTP client type-safe untuk REST API |
| Supabase security | JWT memberikan identitas; RLS menegakkan policy data |
| Room Entity | Data class yang mendefinisikan tabel |
| Room DAO | Interface akses database; @Query untuk SQL kustom |
| LazyRow | Daftar horizontal |

### Template Jawaban Essay yang Aman

1. Mulai dengan definisi satu kalimat.
1. Jelaskan mekanisme atau alasan penggunaannya.
1. Sebutkan dampak/manfaat arsitektural.
1. Tambahkan contoh kode atau alur singkat jika diminta.
1. Gunakan istilah teknis tepat: state, lifecycle, back stack, Repository, dan lainnya.

> **Checklist sebelum UAS:** Mampu menjelaskan 40 jawaban tanpa membaca, menulis pola state hoisting, StateFlow, Navigation popUpTo, Retrofit annotation, Room Entity/DAO, dan memilih LazyRow untuk daftar horizontal.
