package main
import "fmt"

const NMAX int = 1000
type asetKripto struct {

	namaAset string
	harga float64
	nilaiAset float64
 
}
type arrKripto [NMAX]asetKripto
var saldo float64 = 1000000


func main() {

	var kripto arrKripto
	var jumlahAset int
	var option int
	jumlahAset = 0
	fmt.Scan(&option) //Gk ngerti kenapa harus klik beberapa angka dlu baru keluar opsi
	
	for option != 0 {
		fmt.Println("===== Menu =====")
        fmt.Println("1. Tambah Aset Kripto")
        fmt.Println("2. Ubah Aset Kripto")
        fmt.Println("3. Hapus Aset Kripto")
        fmt.Println("4. Beli Aset Kripto")
        fmt.Println("5. Jual Aset Kripto")
        fmt.Println("6. Lihat Riwayat")
        fmt.Println("0. Keluar")
        fmt.Print("Option: ")
		fmt.Scan(&option)
		
		switch option {
		case 1:
			tambahAset(&kripto, &jumlahAset)
		case 2:
			ubahAset(&kripto, jumlahAset)
		case 3:
			hapusAset(&kripto, &jumlahAset)
		case 4:
			beliAset(&kripto, jumlahAset)
		case 5:
			jualAset(&kripto, jumlahAset)
		case 0:
			fmt.Println("Keluar dari program.")
			return
		default:
			fmt.Println("Pilihan tidak valid.")
		}
	}
}

func tambahAset(kripto *arrKripto, jumlahAset *int) {

	var nama string
	var harga float64
	var nilai float64
	var find bool
	find = false 
	
	fmt.Print("Isi nama, harga dan nilai pasar")
	fmt.Scan(&nama, &harga, &nilai)
	for i := 0; i < *jumlahAset; i++ {
		if (*kripto)[i].namaAset == nama {
			fmt.Println("Aset sudah ada, tidak bisa ditambahkan.")
			find = true
		}
	}
	if !find { 
		(*kripto)[*jumlahAset].namaAset = nama
		(*kripto)[*jumlahAset].harga = harga
		(*kripto)[*jumlahAset].nilaiAset = nilai
		*jumlahAset++
		fmt.Println("Aset berhasil ditambahkan.")
	}
}

func ubahAset(kripto *arrKripto, jumlahAset int) {

	var nama, namaBaru string
	var hargaBaru float64
	var nilaiBaru float64
	var find bool
	find = false
	
	fmt.Println("Masukkan nama aset yang ingin diubah:")
	fmt.Scan(&nama)

	for i := 0; i < jumlahAset; i++ {
		if kripto[i].namaAset == nama {

			fmt.Println("Masukkan nama baru:")
			fmt.Scanln(&namaBaru)
			fmt.Println("Masukkan harga baru:")
			fmt.Scanln(&hargaBaru)
			fmt.Println("Masukkan nilai pasar baru:")
			fmt.Scanln(&nilaiBaru)

			kripto[i].namaAset = namaBaru
			kripto[i].harga = hargaBaru
			kripto[i].nilaiAset = nilaiBaru

			fmt.Println("Aset berhasil diubah.")
			find = true
		}
	}
	if !find {
		fmt.Println("Aset tidak ditemukan.")
	}
}

func hapusAset(kripto *arrKripto, jumlahAset *int) {

	var nama string
	var find bool
	
	fmt.Println("Masukkan nama aset yang ingin dihapus:")
	fmt.Scanln(&nama)

	for i := 0; i < *jumlahAset; i++ {
		if kripto[i].namaAset == nama {
			find = true
			for j := i; j < *jumlahAset-1; j++ {
				kripto[j] = kripto[j+1]
			}
			*jumlahAset -= 1
			fmt.Println("Aset berhasil dihapus.")
			
		}
	}
	if !find {
		fmt.Println("Aset tidak ditemukan.")
	}
}

func beliAset(kripto *arrKripto, jumlahAset int) {

	var namaBeli string
	var jumlah, totalHarga float64
	var find bool
	find = false
	
	fmt.Print("Masukkan nama aset yang ingin dibeli")
	fmt.Scan(&namaBeli)
	fmt.Print("Masukkan jumlah aset yang ingin dibeli")
	fmt.Scan(&jumlah)
	
	for i := 0; i < jumlahAset; i++ {
		if (*kripto)[i].namaAset == namaBeli {
			find = true
			totalHarga = jumlah * kripto[i].harga
			if saldo >= totalHarga {
				saldo -= totalHarga
				fmt.Printf("Berhasil membeli %.2f unit %s dengan total harga %.2f", jumlah, namaBeli, totalHarga)
			} else {
				fmt.Println("Saldo tidak mencukupi")
			}
		}
	}
	if !find {
		fmt.Println("Aset tidak ditemukan.")
	}
}

func jualAset(kripto *arrKripto, jumlahAset int) {

	var namaJual string
	var jumlah, totalHarga float64
	var find bool
	find = false
	
	fmt.Print("Masukkan nama aset yang ingin dijual")
	fmt.Scan(&namaJual)
	fmt.Print("Masukkan jumlah aset yang ingin dijual")
	fmt.Scan(&jumlah)
	
	for i := 0; i < jumlahAset; i++ {
		if (*kripto)[i].namaAset == namaJual {
			find = true
			totalHarga = jumlah * kripto[i].harga 
			saldo += totalHarga
			fmt.Printf("Berhasil menjual %.2f unit %s dengan total harga %.2f", jumlah, namaJual, totalHarga)
		}
	}
	if !find {
		fmt.Println("Aset tidak ditemukan.")
	}
}
