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
<img width="545" alt="iny" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/14141d15-f6f3-4ce2-91bb-59b057ba0ce0">

<img width="431" alt="iny1" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/39cb1c21-54d4-4559-b40a-01732020aa33">

# Menampilkan nama Manager tiap Departemen

```
SELECT d.nama AS departemen, k.nama AS manager
    -> FROM departemen d
    -> LEFT JOIN karyawan k ON d.manager_nik = k.nik;
```

<img width="437" alt="Screenshot 2023-06-20 223949" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/7fff5e03-7a66-4c22-b3a3-7daf1cd398d9">

# Menampilkan nama Supervisor tiap Karyawan

```
SELECT k.nik, k.nama, d.nama departemen, s.nama supervisor
    -> FROM karyawan k
    -> LEFT JOIN karyawan s ON s.nik = k.sup_nik
    -> LEFT JOIN departemen d ON d.id_dept = k.id_dept;
```

<img width="471" alt="Screenshot 2023-06-20 224328" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/c09dc49e-83ee-46b9-a934-4453b1efab4a">

# Menampilkan daftar Karyawan yang bekerja pada project A
```
SELECT k.nik, k.nama
    -> FROM karyawan k
    -> JOIN project_detail pj_d ON pj_d.nik = k.nik
    -> JOIN project pj ON pj.id_proj = pj_d.id_proj
    -> WHERE pj.nama = 'A';
```

<img width="434" alt="iny4" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/be6fc3f6-ad03-4f7a-8bcf-12210283179d">


# Menyambungkan Tabel
```
ALTER TABLE departemen ADD CONSTRAINT FOREIGN KEY (id_p) REFERENCES perusahaan (id_p);

ALTER TABLE karyawan ADD CONSTRAINT FOREIGN KEY  (id_dept) REFERENCES departemen (id_dept);

ALTER TABLE departemen ADD CONSTRAINT FOREIGN KEY (manager_nik) REFERENCES karyawan (nik);

ALTER TABLE karyawan ADD CONSTRAINT FOREIGN KEY (sup_nik) REFERENCES karyawan (nik);

ALTER TABLE project_detail ADD CONSTRAINT FOREIGN KEY (nik) REFERENCES karyawan (nik);

ALTER TABLE project_detail ADD CONSTRAINT FOREIGN KEY (id_proj) REFERENCES project (id_proj);
```

<img width="960" alt="2023-06-20" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/82986867-cf35-4ea0-9604-4d265f4b41c6">

## LATIHAN PAKTIKUM
Qurey untuk menampilkan:

1. Departemen apa saja yang terlibat dalam tiap-tiap project?

 ```
    SELECT p.nama AS project, d.nama AS departemen
FROM project p
INNER JOIN project_detail pd ON p.id_proj = pd.id_proj
INNER JOIN karyawan k ON pd.nik = k.nik
INNER JOIN departemen d ON k.id_dept = d.id_dept
ORDER BY p.nama, d.nama;
```
<img width="446" alt="iny3" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/d7fa865a-c5f4-4b2e-8056-18dd50d9ab25">

2. Jumlah Karyawan tiap departemen yang bekerja pada tiap-tiap project

```
SELECT p.nama AS project, d.nama AS departemen, COUNT(k.nik) AS jumlah_karyawan
FROM project p
INNER JOIN project_detail pd ON p.id_proj = pd.id_proj
INNER JOIN karyawan k ON pd.nik = k.nik
INNER JOIN departemen d ON k.id_dept = d.id_dept
GROUP BY p.nama, d.nama
ORDER BY p.nama, d.nama;
```
<img width="475" alt="iny5" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/63d011d5-d495-4379-b55e-b8005b8f1510">


3. Ada berapa project yang sedang dikerjakan oleh depertemen RnD? (ket:project berjalan adalah yang statusnya 1)!

```
SELECT COUNT(p.id_proj) AS jumlah_proyek
    -> FROM project p
    -> INNER JOIN project_detail pd ON p.id_proj = pd.id_proj
    -> INNER JOIN karyawan k ON pd.nik = k.nik
    -> INNER JOIN departemen d ON k.id_dept = d.id_dept
    -> WHERE d.nama = 'RnD' AND p.status = 1;
```

<img width="401" alt="iny6" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/78919835-0e38-4b63-9294-f7b15cda2a3d">

4. Berapa banyak yang sedang dikerjakan oleh Ari?
```
SELECT COUNT(p.id_proj) AS jumlah_proyek
    -> FROM project p
    -> INNER JOIN project_detail pd ON p.id_proj = pd.id_proj
    -> INNER JOIN karyawan k ON pd.nik = k.nik
    -> WHERE k.nama = 'Ari';
```

<img width="397" alt="iny7" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/59aa279f-aad2-40c5-ab42-ff7c6a824b4d">

5. siapa saja yang mengerjakan project B?

```
SELECT k.nama AS nama_karyawan
    -> FROM karyawan k
    -> INNER JOIN project_detail pd ON k.nik = pd.nik
    -> INNER JOIN project p ON pd.id_proj = p.id_proj
    -> WHERE p.nama = 'B';
```

<img width="412" alt="iny8" src="https://github.com/inayy12/PERTEMUAN13/assets/115867315/ff7d176d-ce1b-4853-b6ec-65d3fa098ce4">
