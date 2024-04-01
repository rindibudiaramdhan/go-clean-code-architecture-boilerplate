# Karakteristik Utama

Berikut adalah beberapa karakteristik utama dari arsitektur Clean Code:

## 1. Readability
Kode harus mudah dibaca dan dipahami oleh pengembang lain. Ini termasuk penggunaan nama variabel yang deskriptif, struktur kode yang terorganisir, serta menghindari kode yang ambigu atau sulit dipahami.

```go
package main

import (
	"fmt"
	"math"
)

// Circle represents a circle with a radius.
type Circle struct {
	Radius float64 // Radius of the circle
}

// Area calculates the area of the circle.
func (c Circle) Area() float64 {
	return math.Pi * c.Radius * c.Radius
}

// Circumference calculates the circumference of the circle.
func (c Circle) Circumference() float64 {
	return 2 * math.Pi * c.Radius
}

func main() {
	// Create a circle object with a radius of 3
	circle := Circle{Radius: 3.0}

	// Calculate and print the area of the circle
	area := circle.Area()
	fmt.Printf("Area of the circle: %.2f\n", area)

	// Calculate and print the circumference of the circle
	circumference := circle.Circumference()
	fmt.Printf("Circumference of the circle: %.2f\n", circumference)
}
```

Prinsip ini mengemukakan bahwa kode seharusnya ditulis sedemikian rupa sehingga mirip dengan membaca teks prosa. Ini membuatnya lebih mudah bagi pengembang lain untuk memahami tujuan dan alur dari kode tersebut.

### Key Points:
- Menggunakan nama variabel yang deskriptif dan menambahkan komentar untuk kejelasan.
- Menulis kode dengan gaya bahasa yang jelas dan mudah dimengerti.

## 2. Simplicity
Prinsip kesederhanaan menyatakan bahwa kode harus sederhana dan tidak rumit. Ini berarti menghindari pembuatan kode yang terlalu kompleks atau menggunakan konstruksi yang tidak diperlukan. Prinsip ini membantu mencegah terjadinya "over-engineering" atau "gold-plating" di mana fitur atau struktur yang tidak diperlukan ditambahkan ke kode.

Berikut adalah contoh kode sederhana yang membedakan antara *simplicity* (kesederhanaan) dan *over-engineering*:

Contoh *Over-Engineering*
```go
package main

import "fmt"

// Struct untuk menyimpan slice dan method-method yang berhubungan
type SliceManager struct {
	slice []int
}

// Fungsi untuk membuat instance baru dari SliceManager
func NewSliceManager(slice []int) *SliceManager {
	return &SliceManager{slice: slice}
}

// Method untuk menghitung jumlah elemen dalam slice
func (sm *SliceManager) CountElements() int {
	count := 0
	for range sm.slice {
		count++
	}
	return count
}

func main() {
	numbers := []int{1, 2, 3, 4, 5}
	// Membuat instance SliceManager
	sliceManager := NewSliceManager(numbers)
	// Menghitung jumlah elemen menggunakan method CountElements
	fmt.Println("Jumlah elemen:", sliceManager.CountElements())
}
```

Contoh *simplicity*
```go
package main

import "fmt"

// Fungsi untuk menghitung jumlah elemen dalam sebuah slice
func CountElements(slice []int) int {
	count := 0
	for range slice {
		count++
	}
	return count
}

func main() {
	numbers := []int{1, 2, 3, 4, 5}
	fmt.Println("Jumlah elemen:", CountElements(numbers))
}
```

Perbedaan antara kedua contoh tersebut adalah pada tingkat kompleksitas dan kebutuhan desain yang berlebihan. contoh pertama adalah contoh *over-engineering*. Meskipun akhirnya mencapai tujuan yang sama dengan contoh kedua, namun struktur kode yang dibuat jauh lebih kompleks. Kita membuat sebuah struct `SliceManager` dengan *method* untuk menghitung jumlah elemen dalam *slice*. Meskipun hal ini meningkatkan struktur dan keterbacaan kode, namun bisa dianggap sebagai *over-engineering* karena fungsi yang ditambahkan terlalu rumit untuk kebutuhan sederhana tersebut.

Sementara itu, Contoh kedua adalah contoh kesederhanaan, di mana kita hanya membuat sebuah fungsi sederhana untuk menghitung jumlah elemen dalam sebuah *slice*. Fungsinya langsung, mudah dipahami, dan tidak memerlukan struktur data tambahan.

### Key Point:
- Menjaga struktur kode tetap sederhana tanpa kompleksitas yang tidak perlu.

## 3. Separation of Concerns
Prinsip pemisahan kepentingan (*separation of concerns*) membagi kode ke dalam bagian-bagian yang berbeda sesuai dengan fungsinya masing-masing. Ini termasuk pemisahan antara logika bisnis, tampilan pengguna, dan akses data.

Contoh Tanpa *Separation of Concerns*
```go
package main

import "fmt"

// Fungsi untuk menghitung dan mencetak luas dan keliling lingkaran
func CalculateAndPrintCircleProperties(radius float64) {
	area := 3.14 * radius * radius
	circumference := 2 * 3.14 * radius
	fmt.Printf("Luas lingkaran: %.2f\n", area)
	fmt.Printf("Keliling lingkaran: %.2f\n", circumference)
}

func main() {
	radius := 5.0
	CalculateAndPrintCircleProperties(radius)
}
```

Contoh Dengan *Separation of Concerns*

```go
package main

import "fmt"

// Fungsi untuk menghitung luas lingkaran
func CalculateCircleArea(radius float64) float64 {
	return 3.14 * radius * radius
}

// Fungsi untuk menghitung keliling lingkaran
func CalculateCircleCircumference(radius float64) float64 {
	return 2 * 3.14 * radius
}

// Fungsi untuk mencetak hasil perhitungan lingkaran
func PrintCircleProperties(area, circumference float64) {
	fmt.Printf("Luas lingkaran: %.2f\n", area)
	fmt.Printf("Keliling lingkaran: %.2f\n", circumference)
}

func main() {
	radius := 5.0
	area := CalculateCircleArea(radius)
	circumference := CalculateCircleCircumference(radius)
	PrintCircleProperties(area, circumference)
}
```

Perbedaan antara kedua contoh tersebut adalah dalam pemisahan kepentingan atau *concern*. Pada contoh pertama, semua logika terkait perhitungan dan pencetakan luas dan keliling lingkaran disatukan dalam satu fungsi `CalculateAndPrintCircleProperties()`. Hal ini menyebabkan fungsi tersebut bertanggung jawab atas dua hal yang berbeda: perhitungan dan pencetakan, sehingga melanggar prinsip `Separation of Concerns`.

Sementara itu, pada contoh kedua, kita memisahkan setiap tugas ke dalam fungsi-fungsi terpisah: satu untuk menghitung luas lingkaran (`CalculateCircleArea()`), satu untuk menghitung keliling lingkaran (`CalculateCircleCircumference()`), dan satu lagi untuk mencetak hasil perhitungan (`PrintCircleProperties()`). Ini menciptakan pemisahan yang jelas antara logika perhitungan dan logika pencetakan, sehingga mematuhi prinsip `Separation of Concerns`.

### Key Point:
- Memisahkan logika perhitungan luas dan keliling ke dalam metode terpisah.

## 4. Reliability
Kode harus dapat diandalkan dan berfungsi sebagaimana mestinya. Ini berarti menghindari adanya bug dan kesalahan, serta memastikan bahwa kode dapat mengatasi situasi-situasi yang tidak terduga dengan baik.

Contoh Tanpa Prinsip Reliability
```go
package main

import (
	"fmt"
	"math"
)

// Fungsi untuk menghitung akar kuadrat dari sebuah bilangan
func CalculateSquareRoot(number float64) float64 {
	if number < 0 {
		return -1 // Penanganan kasus khusus
	}
	return math.Sqrt(number)
}

func main() {
	// Menghitung akar kuadrat dari bilangan
	result := CalculateSquareRoot(16)
	fmt.Println("Akar kuadrat dari 16 adalah:", result)

	// Kasus khusus: Menghitung akar kuadrat dari bilangan negatif
	specialResult := CalculateSquareRoot(-16)
	fmt.Println("Akar kuadrat dari -16 adalah:", specialResult)
}
```

Contoh Dengan Prinsip Reliability

```go
package main

import (
	"fmt"
	"math"
)

// Fungsi untuk menghitung akar kuadrat dari sebuah bilangan
func CalculateSquareRoot(number float64) (float64, error) {
	if number < 0 {
		return 0, fmt.Errorf("Tidak dapat menghitung akar kuadrat dari bilangan negatif: %f", number)
	}
	return math.Sqrt(number), nil
}

func main() {
	// Menghitung akar kuadrat dari bilangan
	result, err := CalculateSquareRoot(16)
	if err != nil {
		fmt.Println("Error:", err)
	} else {
		fmt.Println("Akar kuadrat dari 16 adalah:", result)
	}

	// Menghitung akar kuadrat dari bilangan negatif
	specialResult, specialErr := CalculateSquareRoot(-16)
	if specialErr != nil {
		fmt.Println("Error:", specialErr)
	} else {
		fmt.Println("Akar kuadrat dari -16 adalah:", specialResult)
	}
}
```

Perbedaan antara kedua contoh tersebut adalah dalam penanganan error atau kesalahan. Pada contoh pertama, ketika fungsi `CalculateSquareRoot()` menerima bilangan negatif, ia mengembalikan nilai -1 sebagai tanda kasus khusus, tanpa memberikan informasi lebih lanjut tentang kesalahan yang terjadi.

Sementara itu, pada contoh kedua, kita menggunakan prinsip Reliability dengan menambahkan pengembalian nilai bertipe error (`error`) bersamaan dengan nilai hasil perhitungan. Jika terjadi kesalahan, kita mengembalikan error yang mengandung pesan yang jelas tentang jenis kesalahan yang terjadi. Dengan demikian, pengguna kode dapat dengan mudah memahami masalah yang terjadi dan mengatasinya dengan lebih baik.

### Key Point:
- Menggunakan fungsi matematika yang teruji dari pustaka standar Go.

## 5. Testing
Arsitektur Clean Code mendorong penggunaan pengujian otomatis (automated testing) untuk memastikan bahwa kode berfungsi sebagaimana diharapkan dan bahwa perubahan kode tidak mempengaruhi fungsi-fungsi yang sudah ada.

```go
package main

import (
	"math"
	"testing"
)

func TestHitungLuasLingkaran(t *testing.T) {
	lingkaran := Circle{Radius: 3.0}
	luasYangDiHarapkan := math.Pi * 3.0 * 3.0
	luasAktual := lingkaran.Area()

	if luasAktual != luasYangDiHarapkan {
		t.Errorf("Perhitungan luas tidak tepat. Harapannya: %.2f, Hasilnya: %.2f", luasYangDiHarapkan, luasAktual)
	}
}

func TestHitungKelilingLingkaran(t *testing.T) {
	lingkaran := Circle{Radius: 3.0}
	kelilingYangDiHarapkan := 2 * math.Pi * 3.0
	kelilingAktual := lingkaran.Circumference()

	if kelilingAktual != kelilingYangDiHarapkan {
		t.Errorf("Perhitungan keliling tidak tepat. Harapannya: %.2f, Hasilnya: %.2f", kelilingYangDiHarapkan, kelilingAktual)
	}
}
```

### Key Point:
- Menambahkan pengujian unit untuk memastikan kebenaran perhitungan luas dan keliling.

## 6. Expressive Code
Kode seharusnya diekspresikan secara jelas dan langsung. Hal ini mencakup penggunaan struktur dan pola yang sesuai dengan paradigma pemrograman yang digunakan serta menghindari kode yang ambigu atau membingungkan.

Contoh Tanpa Prinsip Expressive Code
```go
package main

import "fmt"

// Fungsi untuk menghitung jumlah bilangan ganjil dalam sebuah slice
func CountOddNumbers(numbers []int) int {
	count := 0
	for _, num := range numbers {
		if num%2 != 0 {
			count++
		}
	}
	return count
}

func main() {
	numbers := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	oddCount := CountOddNumbers(numbers)
	fmt.Println("Jumlah bilangan ganjil:", oddCount)
}
```

Contoh Dengan Prinsip Expressive Code

```go
package main

import "fmt"

// Fungsi untuk menghitung jumlah bilangan ganjil dalam sebuah slice
func CountOddNumbers(numbers []int) int {
	oddCount := 0
	for _, num := range numbers {
		if isOdd(num) {
			oddCount++
		}
	}
	return oddCount
}

// Fungsi untuk memeriksa apakah sebuah bilangan ganjil atau tidak
func isOdd(num int) bool {
	return num%2 != 0
}

func main() {
	numbers := []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
	oddCount := CountOddNumbers(numbers)
	fmt.Println("Jumlah bilangan ganjil:", oddCount)
}
```

Perbedaan antara kedua contoh tersebut adalah dalam ekspresivitas kode. Pada contoh pertama, meskipun fungsinya bekerja dengan benar, namun kurang ekspresif dan sulit untuk dipahami. Penggunaan logika langsung dalam perulangan untuk memeriksa bilangan ganjil memperumit pembacaan kode.

Sementara itu, pada contoh kedua, kita menggunakan prinsip Expressive Code dengan memisahkan logika pengecekan bilangan ganjil ke dalam fungsi terpisah `isOdd()`. Dengan cara ini, kode menjadi lebih ekspresif dan mudah dipahami, karena niat atau tujuan dari setiap bagian kode menjadi lebih jelas.

### Key Point:
- Menulis kode yang jelas dan ringkas.

## 7. Dependency Management
Arsitektur Clean Code memperhatikan bagaimana *Dependency* antara komponen-komponen dalam sistem dikelola. Ini termasuk penggunaan prinsip-prinsip seperti *Dependency Injection* untuk mengurangi *Dependency* yang ketat antara komponen-komponen.

### Prinsip-Prinsip Dependency Injection (DI)
**Inversion of Control (IoC)**

Prinsip ini menyatakan bahwa kendali atas pembuatan dan pengelolaan objek tidak ada di tangan objek itu sendiri, melainkan di tangan sebuah mekanisme eksternal. Dalam konteks DI, IoC diterapkan dengan mendelegasikan pembuatan dan penyediaan dependency kepada objek-objek yang berada di luar kelas yang membutuhkan dependency tersebut.

Contoh:
```go
package main

import "fmt"

type Greeter struct {
	dependency Dependency
}

type Dependency struct {
	Name string
}

func NewGreeter(dep Dependency) Greeter {
	return Greeter{
		dependency: dep,
	}
}

func (g Greeter) Greet() string {
	return fmt.Sprintf("Hello, %s!", g.dependency.Name)
}

func main() {
	dependency := Dependency{Name: "John"}
	greeter := NewGreeter(dependency)
	fmt.Println(greeter.Greet())
}
```
Dalam contoh ini, kita memiliki sebuah struct `Greeter` yang memiliki metode `Greet` untuk menyapa seseorang. Namun, metode `Greet` memerlukan sebuah dependency untuk memperoleh nama orang yang disapa. Dependency tersebut disediakan melalui fungsi `NewGreeter`.

**Dependency Abstrak**

Kode seharusnya bergantung pada abstraksi daripada implementasi spesifik. Dengan menggunakan abstraksi, kita bisa lebih mudah mengganti atau memperbarui komponen-komponen tanpa mempengaruhi bagian-bagian lain dari kode.
package main

contoh:
```go
import "fmt"

type GreeterInterface interface {
	Greet() string
}

type Greeter struct {
	dependency GreeterInterface
}

type Dependency struct {
	Name string
}

func NewGreeter(dep GreeterInterface) Greeter {
	return Greeter{
		dependency: dep,
	}
}

func (g Greeter) Greet() string {
	return g.dependency.Greet()
}

type EnglishGreeter struct {
	Name string
}

func (eg EnglishGreeter) Greet() string {
	return fmt.Sprintf("Hello, %s!", eg.Name)
}

func main() {
	dependency := EnglishGreeter{Name: "John"}
	greeter := NewGreeter(dependency)
	fmt.Println(greeter.Greet())
}
```

Dalam contoh ini, kita membuat sebuah *interface* `GreeterInterface` sebagai abstraksi untuk komponen yang menyapa. Kemudian, kita menggunakan *interface* ini sebagai *dependency* di dalam struct `Greeter`.

**Pisahkan Pembuatan dari Penggunaan**

Objek-objek yang membutuhkan *dependency* sebaiknya tidak membuat *dependency* tersebut sendiri, melainkan menerimanya dari luar. Ini memisahkan peran pembuatan objek (*creation*) dari peran penggunaan objek (*consumption*).

Contoh:
```go
package main

import "fmt"

type Greeter struct {
	dependency Dependency
}

type Dependency struct {
	Name string
}

func NewGreeter(dep Dependency) Greeter {
	return Greeter{
		dependency: dep,
	}
}

func (g Greeter) Greet() string {
	return fmt.Sprintf("Hello, %s!", g.dependency.Name)
}

func main() {
	dependency := Dependency{Name: "John"}
	greeter := NewGreeter(dependency)
	fmt.Println(greeter.Greet())
}
```

Dalam contoh ini, pembuatan *dependency* (objek *Dependency*) dipisahkan dari penggunaannya dalam *struct* `Greeter`. Pembuatan *Dependency* dilakukan di luar *struct* `Greeter` dan kemudian diberikan ke dalam *struct* tersebut melalui fungsi `NewGreeter`.

**Dependency Injection Container**

Sebuah wadah atau kontainer DI adalah sebuah entitas yang bertanggung jawab atas pembuatan dan pengelolaan *dependency* dalam sebuah aplikasi. Kontainer ini menyediakan mekanisme untuk mendaftarkan *dependency* dan kemudian menyediakannya kepada komponen-komponen yang membutuhkannya.

Contoh:
```go
package main

import "fmt"

type Dependency struct {
	Name string
}

type Greeter struct {
	dependency Dependency
}

func NewGreeter(dep Dependency) Greeter {
	return Greeter{
		dependency: dep,
	}
}

func (g Greeter) Greet() string {
	return fmt.Sprintf("Hello, %s!", g.dependency.Name)
}

type Container struct {
	dependency Dependency
}

func NewContainer() Container {
	return Container{
		dependency: Dependency{Name: "John"},
	}
}

func (c Container) ProvideGreeter() Greeter {
	return NewGreeter(c.dependency)
}

func main() {
	container := NewContainer()
	greeter := container.ProvideGreeter()
	fmt.Println(greeter.Greet())
}
```

Dalam contoh ini, kita menggunakan sebuah *container* sederhana (*Container*) untuk mendaftarkan dan menyediakan *dependency*. Kemudian, *dependency* tersebut diberikan kepada *struct* `Greeter` melalui fungsi `NewGreeter`.

**Pengujian yang Lebih Baik**

Dengan menggunakan DI, kita dapat dengan mudah mengganti *dependency* dengan *stub* atau *mock* saat melakukan pengujian unit. Hal ini memungkinkan kita untuk mengisolasi komponen-komponen dan menguji mereka secara terpisah tanpa bergantung pada *dependency* nyata.

contoh:
```go
package main

import (
	"fmt"
	"testing"
)

type Greeter struct {
	dependency Dependency
}

type Dependency struct {
	Name string
}

func NewGreeter(dep Dependency) Greeter {
	return Greeter{
		dependency: dep,
	}
}

func (g Greeter) Greet() string {
	return fmt.Sprintf("Hello, %s!", g.dependency.Name)
}

type MockDependency struct{}

func (m MockDependency) Greet() string {
	return "Mocked Greeting"
}

func TestGreeterGreet(t *testing.T) {
	mockDependency := MockDependency{}
	greeter := NewGreeter(mockDependency)

	expected := "Hello, John!"
	actual := greeter.Greet()

	if actual != expected {
		t.Errorf("Expected: %s, Got: %s", expected, actual)
	}
}
```

Dalam contoh ini, kita dapat dengan mudah mengganti dependency dengan mock saat melakukan pengujian unit pada struct Greeter.

Dengan menerapkan prinsip-prinsip DI, kode menjadi lebih modular, fleksibel, dan mudah diuji. Hal ini juga memungkinkan pengembang untuk dengan mudah melakukan perubahan pada dependency tanpa harus memodifikasi banyak bagian dari kode yang ada.

### Key Point:
- Mengelola *Dependency* secara efektif tanpa memperkenalkan kompleksitas yang tidak perlu.

# Prioritas
Prioritas implementasi karakteristik utama dari arsitektur Clean Code dapat bervariasi tergantung pada konteks dan kebutuhan proyek tertentu. Namun, secara umum, berikut adalah urutan prioritas yang disarankan dari yang paling tinggi:

```
1. Readable Code
2. Simplicity
3. Separation of Concerns
4. Reliability
5. Testing
6. Expressive Code
7. Dependency Management
```

# Tools Otomasi Pengecekan Karakteristik Clean Code
Berikut adalah beberapa rekomendasi tools yang dapat membantu dalam otomatisasi dan penerapan karakteristik utama dari arsitektur Clean Code:

## GolangCI-Lint
GolangCI-Lint adalah alat linter dan analisis statis untuk Go. Ini dapat membantu dalam mendeteksi dan memperbaiki pelanggaran aturan gaya, penulisan kode yang buruk, dan masalah kualitas kode lainnya. GolangCI-Lint juga mendukung integrasi dengan berbagai alat CI/CD dan editor kode populer.

## SonarQube
SonarQube adalah platform yang menyediakan analisis statis kode untuk berbagai bahasa pemrograman, termasuk Go. SonarQube dapat mengidentifikasi masalah seperti kode yang kompleks, duplikasi kode, kerentanan keamanan, dan lainnya. Ini membantu dalam memantau dan meningkatkan kualitas kode secara kontinu.

## CodeClimate
CodeClimate adalah platform yang menyediakan analisis kode otomatis untuk berbagai bahasa pemrograman, termasuk Go. CodeClimate dapat membantu dalam mendeteksi masalah kualitas kode seperti kompleksitas yang tinggi, pelanggaran aturan gaya, dan duplikasi kode. Ini juga menyediakan integrasi dengan alat-alat pengembangan lainnya.

## gocyclo
gocyclo adalah alat sederhana untuk menghitung kompleksitas siklomatik dalam kode Go. Ini dapat membantu dalam mengidentifikasi fungsi-fungsi yang terlalu kompleks dan memerlukan perhatian lebih lanjut untuk disederhanakan.

## GoReportCard
GoReportCard adalah layanan online yang memberikan laporan tentang kualitas kode Go berdasarkan beberapa metrik seperti penutupan tes, kompleksitas siklomatik, dan duplikasi kode. Ini memberikan tinjauan cepat tentang kualitas keseluruhan dari proyek Go.

## GoLint
GoLint adalah linter yang mencari pelanggaran aturan gaya Go. Ini membantu dalam memastikan bahwa kode Go mengikuti konvensi penulisan yang direkomendasikan dan mempromosikan konsistensi dalam kode.

## GoTest
GoTest adalah alat bawaan untuk menjalankan dan mengotomatiskan pengujian unit dalam Go. Dengan menulis tes yang komprehensif, kita dapat memastikan bahwa kode berperilaku seperti yang diharapkan dan memenuhi persyaratan fungsionalitas.

## Dependabot
Dependabot adalah alat yang secara otomatis memantau dependensi proyek dan memberikan pembaruan secara otomatis ketika ada pembaruan yang tersedia. Dengan menjaga dependensi tetap terkini, kita dapat memastikan keamanan dan keterandalan aplikasi.

Dengan menggunakan kombinasi dari alat-alat ini, pengembang dapat secara efektif menerapkan dan memelihara karakteristik utama dari arsitektur Clean Code dalam proyek Go mereka.

# Kesimpulan
Dengan menerapkan prinsip-prinsip tersebut, pengembang dapat menciptakan kode yang lebih bersih, lebih mudah dipelihara, dan lebih mudah diubah, sehingga mempercepat proses pengembangan dan mengurangi risiko kesalahan.