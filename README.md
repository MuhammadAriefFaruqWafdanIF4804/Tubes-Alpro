# Tubes-Alpro
package main
import "fmt"

#Variabel Global
const NMAX int = 1000

type asetKripto struct { 

	namaAset string
	harga int
	nilaiAset float64
}
type arrKripto [NMAX]asetKripto

func main() {

	var kripto arrKripto
	var jumlahAset int
	var option int
	fmt.Scan(&option)
 
	for option != 0 {
	fmt.Println("===== Menu =====")
        fmt.Println("1. Kelola Aset Kripto")
        fmt.Println("2. Beli Aset")
        fmt.Println("3. Jual Aset")
        fmt.Println("4. Lihat Riwayat Transaksi")
        fmt.Println("5. Cari Aset")
        fmt.Println("6. Urutkan Aset")
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
	var harga int
	var nilai float64
	var find bool
	find = false 
	fmt.Print("Isi nama, harga dan nilai pasar")
	fmt.Scan(&nama, &harga, &nilai)
	for i := 0; i < *jumlahAset; i++ {
		if (*kripto)[i].namaPasar == nama {
			fmt.Println("Aset sudah ada, tidak bisa ditambahkan.")
			find = true
		}
	}
	if !find { //Gk ngerti pake AI aja deh
		(*kripto)[*jumlahAset].namaAset = nama
		(*kripto)[*jumlahAset].harga = harga
		(*kripto)[*jumlahAset].nilaiAset = nilai
		*jumlahAset++
		fmt.Println("Aset berhasil ditambahkan.")
	}
}

func ubahAset(kripto *arrKripto, jumlahAset int) {

	var nama, namaBaru string
	var hargaBaru int
	var nilaiBaru float64
	fmt.Println("Masukkan nama aset yang ingin diubah:")
	fmt.Scan(&nama)

	for i := 0; i < jumlahAset; i++ {
		if kripto[i].namaPasar == nama {
			var namaBaru string
			var hargaBaru int
			var nilaiBaru float64

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
			
		}
	}
	fmt.Println("Aset tidak ditemukan.")
}

func hapusAset(kripto *arrKripto, jumlahAset *int) {
	
	var nama string
	fmt.Println("Masukkan nama aset yang ingin dihapus:")
	fmt.Scanln(&nama)
	
	for i := 0; i < jumlahAset; i++ {
		if kripto[i].namaAset == nama {
			// Geser elemen setelahnya ke kiri
			for j := i; j < jumlahAset-1; j++ {
				kripto[j] = kripto[j+1]
			}
			jumlahAset--
			fmt.Println("Aset berhasil dihapus.")
			
		}
	}
	fmt.Println("Aset tidak ditemukan.")
 	//Gk ngerti juga, jadinya pake AI
}

func beli() {
	
}

func jual() {
	
}
