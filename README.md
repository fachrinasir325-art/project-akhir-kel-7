#include <iostream>
using namespace std;

const int MAX_RIWAYAT = 200;

struct MataUang {
    string nama;
    double kurs;
};

void tampilkanMenu() {
    cout << "\nPilih mata uang:\n";
    cout << "1. USD (Dolar Amerika)\n";
    cout << "2. EUR (Euro)\n";
    cout << "3. JPY (Yen Jepang)\n";
    cout << "4. MYR (Ringgit Malaysia)\n";
    cout << "5. WON (Won Korea)\n";
    cout << "0. Kembali\n";
    cout << "Pilihan: ";
}

double konversiDariRupiah(double rupiah, double kurs) {
    return rupiah / kurs;
}

double konversiKeRupiah(double nilaiAsing, double kurs) {
    return nilaiAsing * kurs;
}

double konversiAntarAsing(double nilaiAsing, double kursAsal, double kursTujuan) {
    return (nilaiAsing * kursAsal) / kursTujuan;
}

void tampilkanRiwayat(string riwayat[], int jumlah) {
    if (jumlah == 0) {
        cout << "\nBelum ada riwayat konversi.\n";
        return;
    }

    cout << "\n======= RIWAYAT KONVERSI =======\n";
    for (int i = 0; i < jumlah; i++) {
        cout << i + 1 << ". " << riwayat[i] << endl;
    }
}

int main() {


    MataUang data[5] = {
        {"USD", 16712},
        {"EUR", 19421},
        {"JPY", 108},
        {"MYR", 4044},
        {"WON", 11.53}
    };

    string riwayat[MAX_RIWAYAT];
    int jumlahRiwayat = 0;

    int pilihanMenu, asal, tujuan;
    double jumlah, hasil;

    cout << "========== PROGRAM KONVERSI MATA UANG ==========\n";

    while (true) {
        cout << "\nMenu Utama:\n";
        cout << "1. Rupiah ke Mata Uang Asing\n";
        cout << "2. Mata Uang Asing ke Rupiah\n";
        cout << "3. Mata Uang Asing ke Mata Uang Asing\n";
        cout << "4. Lihat Riwayat Konversi\n";
        cout << "0. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihanMenu;

        if (pilihanMenu == 0) {
            cout << "\nTerima kasih telah menggunakan program ini!\n";
            break;
        }


        if (pilihanMenu == 1) {
            cout << "\nMasukkan jumlah Rupiah: ";
            cin >> jumlah;

            tampilkanMenu();
            cin >> tujuan;

            if (tujuan == 0) continue;
            if (tujuan < 1 || tujuan > 5) {
                cout << "Pilihan tidak valid!\n";
                continue;
            }

            hasil = konversiDariRupiah(jumlah, data[tujuan - 1].kurs);

            cout << "\nHasil: " << hasil << " " << data[tujuan - 1].nama << endl;

            riwayat[jumlahRiwayat++] =
                "Rupiah " + to_string(jumlah) +
                " ke " + data[tujuan - 1].nama + " = " + to_string(hasil);
        }


        else if (pilihanMenu == 2) {

            tampilkanMenu();
            cin >> asal;

            if (asal == 0) continue;
            if (asal < 1 || asal > 5) {
                cout << "Pilihan tidak valid!\n";
                continue;
            }

            cout << "\nMasukkan jumlah " << data[asal - 1].nama << ": ";
            cin >> jumlah;

            hasil = konversiKeRupiah(jumlah, data[asal - 1].kurs);

            cout << "\nHasil: " << hasil << " Rupiah\n";

            riwayat[jumlahRiwayat++] =
                data[asal - 1].nama + string(" ") + to_string(jumlah) +
                " ke Rupiah = " + to_string(hasil);
        }


        else if (pilihanMenu == 3) {

            cout << "\n--- Pilih Mata Uang Asal ---\n";
            tampilkanMenu();
            cin >> asal;

            cout << "\n--- Pilih Mata Uang Tujuan ---\n";
            tampilkanMenu();
            cin >> tujuan;

            if (asal == tujuan) {
                cout << "\nMata uang tidak boleh sama!\n";
                continue;
            }

            if (asal == 0 || tujuan == 0) continue;
            if (asal < 1 || asal > 5 || tujuan < 1 || tujuan > 5) {
                cout << "Pilihan tidak valid!\n";
                continue;
            }

            cout << "\nMasukkan jumlah " << data[asal - 1].nama << ": ";
            cin >> jumlah;

            hasil = konversiAntarAsing(jumlah, data[asal - 1].kurs, data[tujuan - 1].kurs);

            cout << "\nHasil: " << hasil << " " << data[tujuan - 1].nama << endl;

            riwayat[jumlahRiwayat++] =
                data[asal - 1].nama + string(" ") + to_string(jumlah) +
                " ke " + data[tujuan - 1].nama + " = " + to_string(hasil);
        }


        else if (pilihanMenu == 4) {
            tampilkanRiwayat(riwayat, jumlahRiwayat);
        }

        else {
            cout << "Pilihan tidak valid!\n";
        }
    }

    return 0;
}
