##  PERTEMUAN13
## STUDI KASUS: ERD KARYaWAN
# Nama : Inayatus Sholekhawati
# NIM : 312210200
# Kelas : TI.22.A.2

## Membuat Table

```
CREATE TABLE perusahaan (
    -> id_p VARCHAR (10) PRIMARY KEY,
    -> nama VARCHAR (45),
    -> alamat VARCHAR (45));

CREATE TABLE departemen (
    -> id_dept VARCHAR (10) PRIMARY KEY,
    -> nama VARCHAR (45),
    -> id_p VARCHAR (10),
    -> manager_nik VARCHAR (10));

CREATE TABLE karyawan (
    -> nik VARCHAR (10) PRIMARY KEY,
    -> nama VARCHAR (45),
    -> id_dept VARCHAR (10),
    -> sup_nik VARCHAR (10));

CREATE TABLE project_detail (
    -> id_proj VARCHAR (10),
    -> nik VARCHAR (10));

CREATE TABLE project (
    ->   id_proj VARCHAR(10) PRIMARY KEY,
    ->   nama VARCHAR(45),
    ->   tgl_mulai DATETIME,
    ->   tgl_selesai DATETIME,
    ->   status TINYINT(1));

```

# Input Data

```
INSERT INTO perusahaan (id_p, nama, alamat)
    -> VALUES
    -> ('P01', 'Kantor Pusat', NULL),
    -> ('P02', 'Cabang Bekasi', NULL);

INSERT INTO departemen (id_dept, nama, id_p, manager_nik)
    -> VALUES
    -> ('D01', 'Produksi', 'P02', 'N01'),
    -> ('D02', 'Marketing', 'P01', 'N03'),
    -> ('D03', 'RnD', 'P02', NULL),
    -> ('D04', 'Logistik', 'P02', NULL);

INSERT INTO karyawan (nik, nama, id_dept, sup_nik)
    -> VALUES
    -> ('N01', 'Ari', 'D01', NULL),
    -> ('N02', 'Dina', 'D01', NULL),
    -> ('N03', 'Rika', 'D03', NULL),
    -> ('N04', 'Ratih', 'D01', 'N01'),
    -> ('N05', 'Riko', 'D01', 'N01'),
    -> ('N06', 'Dani', 'D02', NULL),
    -> ('N07', 'Anis', 'D02', 'N06'),
    -> ('N08', 'Dika', 'D02', 'N06');

INSERT INTO project_detail (id_proj, nik)
    -> VALUES
    -> ('PJ01', 'N01'),
    -> ('PJ01', 'N02'),
    -> ('PJ01', 'N03'),
    -> ('PJ01', 'N04'),
    -> ('PJ01', 'N05'),
    -> ('PJ01', 'N06'),
    -> ('PJ01', 'N07'),
    -> ('PJ01', 'N08'),
    -> ('PJ02', 'N01'),
    -> ('PJ02', 'N03'),
    -> ('PJ02', 'N05'),
    -> ('PJ03', 'N03'),
    -> ('PJ03', 'N07'),
    -> ('PJ03', 'N08');

INSERT INTO project (id_proj, nama, tgl_mulai, tgl_selesai, status)
    -> VALUES
    -> ('PJ01', 'A', '2019-01-10', '2019-03-10', '1'),
    -> ('PJ02', 'B', '2019-02-15', '2019-04-10', '1'),
    -> ('PJ03', 'C', '2019-03-21', '2019-05-10', '1');

```
