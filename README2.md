shape data frame :
- Jumlah row 899164
- Jumlah column 27

Data Cleaning
- Duplicated data : no duplicated data
- missing value   : kolom yg missing value di drop
- Handling outliers : dihapus. sebelum dihapus (456239,) sesudah dihapus (387552,)

Handle error value  : 
- Ubah kolom ApprovalDate, DisbursementDate menjadi datetime
- menghapus dolar sign pada kolom DisbursementGross, BalanceGross, ChgOffPrinGr, GrAppv, SBA_Appv dan mengubah data typenya menjadi float
- Hilangkan huruf A pada '1976A' lalu ubah ke int (dari kolom ApprovalFY)
- Mengubah tipe data 'NewExist' menjadi int
- MenguUbah tipe data 'NAICS' dari numeric ke object

Feature Encoding
- feature encoding 'RevLineCr' & LowDoc nilai diubah Y=1, N=0
- membuat kolom baru (default) dan mengubah nilainya menjadi deafult = 1, no deafult = 0

Feature Extraction
- membuat kolom baru (daysdisbursment) = AppDate-DisbDate
- Membuat kolom baru (StateSame) yang menunjukkan peminjam dan Bank berada pada state yang sama
- Membuat feature SBA_AppvPct untuk melihat persentase pinjaman yang dijamin oleh SBA
- Membuat kolom baru industri dengan mengambil 2 digit pertama pada kolom NAICS
- melakukan mapping kolom industri berdasarkan 2 digit pertama pada kolom NAICS

Feature selection
berikut adalah fitur-fitur yang dihapus dan alasannya :
- 'LoanNr_ChkDgt': merupakan primary key
- 'Name' : memiliki kardinalitas yang sangat tinggi dan hanya memuat informasi nama bisnis sehingga tidak dapat dijadikan prediktor target.
- 'City', 'Zip' : memiliki kardinalitas yang sangat tinggi dan telah diwakilkan oleh state.
- 'State' : memiliki kardinalitas yang tinggi dan telah digantikan oleh statesame.
- 'Bank' : memiliki kardinalitas yang sangat tinggi dan hanya memuat informasi nama bank sehingga tidak dapat dijadikan prediktor target.
- 'BankState' : memiliki kardinalitas yang tinggi dan telah digantikan oleh statesame.
- 'NAICS' : digantikan oleh industri.
- 'ApprovalDate' dan 'ApprovalFY' merujuk pada waktu pinjaman ketika disetujui sehingga tidak dapat menjadi preditor target.
- 'FranchiseCode: memiliki kardinalitas yang tinggi dan telah digantikan oleh Franchise
- 'ChgOffDate': 75% data pada feature berisi null value, feature ini menunjukkan tanggal ketika peminjaman dinyatan gagal.
- 'MIS_Status': digantikan Default
- 'GrAppv' dan 'SBA_Appv': digantikan SBAApvPct
- 'Industry': digantikan PctIndustri


Handling Imbalance
Kamimenggunakan random oversampling + undersampling dengan imblearn. Selain untuk menyeimbangkan data kita gunakan random over dan under sampling agar kita bisa meningkatkan sampel kelas,minoritas sama dengan kelas mayoritas lain
