use master 
go
create database QuanLyPhongTro
on primary(
	name = 'QuanLyPhongTro_dat',
	filename = 'D:\QuanLyPhongTro.mdf',
	size = 10mb,
	maxsize = 100mb,
	filegrowth = 5mb
)
log on(
	name = 'QuanLyPhongTro_log',
	filename = 'D:\QuanLyPhongTro.ldf',
	size = 1mb,
	maxsize = 15mb,
	filegrowth = 20%
)
go 
use QuanLyPhongTro
go
create table NGUOI_DUNG(
    maNguoiDung nchar(10) primary key not null,
	tenNguoiDung nvarchar(30) unique,
	tenDangNhap nvarchar(30) not null,
	matKhau nvarchar(30) not null,
	Email nvarchar(30) unique,
	std nvarchar(20)
)
drop table NGUOI_DUNG
create table NHA_TRO(
	maNhaTro nchar(10) primary key not null,
	tenNhaTro nvarchar(30) not null,
	DienTich decimal(8,2) not null,
	QuanLy nvarchar(30)
)
drop table NHA_TRO
create table PHONG(
	maPhong nchar(10) primary key not null,
	maNhaTro nchar(10),
	tenPhong nvarchar(30),
	Mota ntext,
	tienPhong money,
	constraint fk_NT_P foreign key (maNhaTro) references NHA_TRO(maNhaTro)
)
drop table PHONG
create table NGUOI_THUE_TRO(
	maNguoiThueTro nchar(10) primary key not null,
	maNguoiDung nchar(10) not null,
	maPhong nchar(10) not null,
	tenNguoiThue nvarchar(30) not null,
	Email nchar(30) unique not null,
	std nvarchar(20),
	constraint fk_ND_NTT foreign key (maNguoiDung) references NGUOI_DUNG(maNguoiDung),
	constraint fk_P_NTT foreign key (maPhong) references PHONG(maPhong)
)
drop NGUOI_THUE_TRO
create table CHU_TRO(
	maChuTro nchar(10) not null,
	tenChuTro nvarchar(30) not null,
	soDT nvarchar(20),
	eMail nchar(30)
)
drop table CHU_TRO
create table HOP_DONG (
	maHopDong nchar(10) primary key not null,
	maNguoiDung nchar(10) not null,
	maNguoiThueTro nchar(10) not null,
	NgayBatDau date not null,
	NgayKetThuc date not null,
	SoTienNop money not null,
	constraint fk_ND_HD foreign key(maNguoiDung) references NGUOI_DUNG(maNguoiDung),
	constraint fk_NTT_HD foreign key(maNguoiThueTro) references NGUOI_THUE_TRO(maNguoiThueTro)
)
drop table HOP_DONG
create table DICH_VU (
	maDichVu nchar(10) primary key not null,
	tenDichVu nvarchar(40),
	moTa ntext,
	gia money not null, 
	constraint check_gia check(gia >= 0)
)
drop table DICH_VU
create table GIAO_DICH(
	maGiaoDich nchar(10) primary key not null,
	maNguoiThueTro nchar(10),
	NgayGiaoDich date not null,
	NgayHetHan date not null,
	GiamGia money,
	tong_tien money,
	constraint check_tt check(tong_tien >= 0),
	constraint fk_NTT_GD foreign key (maNguoiThueTro) references NGUOI_THUE_TRO(maNguoiThueTro)
)
drop table GIAO_DICH
create table CHI_TIET_GIAO_DICH (
	maChiTietGD nchar(10) primary key not null,
	maGiaoDich nchar(10) not null,
	maDichVu nchar(10) not null,
	ThoiHan datetime not null,
	SoLuong int not null,
	GiaTien money not null,
	constraint fk_GD_CTGD foreign key (maGiaoDich) references GIAO_DICH(maGiaoDich),
	constraint fk_DV_CTGD foreign key (maDichVu) references DICH_VU(maDichVu)
)
drop table CHI_TIET_GIAO_DICH

INSERT INTO NGUOI_DUNG VALUES
('ND01', N'Nguyễn Văn A', 'nguyenvana', 'password1', 'vana@gmail.com', '0123456789'),
('ND02', N'Trần Thị B', 'tranthib', 'password2', 'thib@gmail.com', '0123456788'),
('ND03', N'Phạm Văn C', 'phamvanc', 'password3', 'vanc@gmail.com', '0123456787'),
('ND04', N'Lê Thị D', 'lithid', 'password4', 'thid@gmail.com', '0123456786'),
('ND05', N'Nguyễn Văn E', 'nguyenvane', 'password5', 'vane@gmail.com', '0123456785'),
('ND06', N'Trần Thị F', 'tranthif', 'password6', 'thif@gmail.com', '0123456784'),
('ND07', N'Phạm Văn G', 'phamvang', 'password7', 'vang@gmail.com', '0123456783'),
('ND08', N'Lê Thị H', 'lithih', 'password8', 'thih@gmail.com', '0123456782'),
('ND09', N'Nguyễn Văn I', 'nguyenvani', 'password9', 'vani@gmail.com', '0123456781'),
('ND10', N'Trần Thị J', 'tranthij', 'password10', 'thij@gmail.com', '0123456780'),
('ND11', N'Phạm Văn K', 'phamvank', 'password11', 'vank@gmail.com', '0123456790'),
('ND12', N'Lê Thị L', 'lithil', 'password12', 'thil@gmail.com', '0123456700'),
('ND13', N'Nguyễn Văn M', 'nguyenvanm', 'password13', 'vanm@gmail.com', '0123456710'),
('ND14', N'Trần Thị N', 'tranthin', 'password14', 'thin@gmail.com', '0123456720'),
('ND15', N'Phạm Văn O', 'phamvano', 'password15', 'vano@gmail.com', '0123456730'),
('ND16', N'Lê Thị P', 'lithip', 'password16', 'thip@gmail.com', '0123456740'),
('ND17', N'Nguyễn Văn Q', 'nguyenvanq', 'password17', 'vanq@gmail.com', '0123456750'),
('ND18', N'Trần Thị R', 'tranthir', 'password18', 'thir@gmail.com', '0123456760'),
('ND19', N'Phạm Văn S', 'phamvans', 'password19', 'vans@gmail.com', '0123456770'),
('ND20', N'Lê Thị T', 'lithit', 'password20', 'thit@gmail.com', '0123456789');


INSERT INTO NHA_TRO VALUES
('NT01', N'Nhà trọ A', 100.00, N'Nguyễn Văn A'),
('NT02', N'Nhà trọ B', 150.00, N'Trần Thị B'),
('NT03', N'Nhà trọ C', 200.00, N'Phạm Văn C'),
('NT04', N'Nhà trọ D', 120.00, N'Lê Thị D'),
('NT05', N'Nhà trọ E', 180.00, N'Nguyễn Văn E'),
('NT06', N'Nhà trọ F', 160.00, N'Trần Thị F'),
('NT07', N'Nhà trọ G', 140.00, N'Phạm Văn G'),
('NT08', N'Nhà trọ H', 110.00, N'Lê Thị H'),
('NT09', N'Nhà trọ I', 130.00, N'Nguyễn Thị Y'),
('NT10', N'Nhà trọ J', 210.00, N'Nguyễn Thị Z'),
('NT11', N'Nhà trọ K', 250.00, N'Phan Văn K'),
('NT12', N'Nhà trọ L', 190.00, N'Võ Thị L'),
('NT13', N'Nhà trọ M', 220.00, N'Nguyễn Thị M'),
('NT14', N'Nhà trọ N', 170.00, N'Ngô Thị N'),
('NT15', N'Nhà trọ O', 160.00, N'Hoàng Văn O'),
('NT16', N'Nhà trọ P', 180.00, N'Đoàn Thị P'),
('NT17', N'Nhà trọ Q', 210.00, N'Trương Văn Q'),
('NT18', N'Nhà trọ R', 230.00, N'Bùi Thị R'),
('NT19', N'Nhà trọ S', 200.00, N'Lê Văn S'),
('NT20', N'Nhà trọ V', 180.00, N'Lê Văn V');


INSERT INTO PHONG VALUES
('MP01', 'NT01', N'Phòng 101', N'Phòng rộng rãi, thoáng mát', 1500000),
('MP02', 'NT02', N'Phòng 102', N'Phòng có cửa sổ lớn', 1600000),
('MP03', 'NT03', N'Phòng 201', N'Phòng sạch sẽ, đầy đủ tiện nghi', 1700000),
('MP04', 'NT04', N'Phòng 202', N'Phòng có ban công', 1800000),
('MP05', 'NT05', N'Phòng 301', N'Phòng yên tĩnh, thích hợp cho học sinh', 1400000),
('MP06', 'NT06', N'Phòng 302', N'Phòng có điều hòa', 1900000),
('MP07', 'NT07', N'Phòng 401', N'Phòng có bếp riêng', 2000000),
('MP08', 'NT08', N'Phòng 402', N'Phòng có toilet riêng', 2100000),
('MP09', 'NT09', N'Phòng 501', N'Phòng có tủ lạnh', 1600000),
('MP10', 'NT10', N'Phòng 502', N'Phòng có máy giặt', 1700000),
('MP11', 'NT11', N'Phòng 601', N'Phòng có internet miễn phí', 1500000),
('MP12', 'NT12', N'Phòng 602', N'Phòng có TV', 1600000),
('MP13', 'NT13', N'Phòng 701', N'Phòng có sân thượng', 1800000),
('MP14', 'NT14', N'Phòng 702', N'Phòng có cửa sổ lớn', 1900000),
('MP15', 'NT15', N'Phòng 801', N'Phòng có view đẹp', 2000000),
('MP16', 'NT16', N'Phòng 802', N'Phòng có điều hòa', 2100000),
('MP17', 'NT17', N'Phòng 901', N'Phòng có bếp', 1600000),
('MP18', 'NT18', N'Phòng 902', N'Phòng có toilet riêng', 1700000),
('MP19', 'NT19', N'Phòng 1001', N'Phòng có tủ lạnh', 1800000),
('MP20', 'NT20', N'Phòng 1002', N'Phòng có máy giặt', 1900000);



INSERT INTO NGUOI_THUE_TRO VALUES
('NTT01', 'ND01', 'MP01', N'Trần Văn X', 'tranvanx@gmail.com', '0123456789'),
('NTT02', 'ND02', 'MP02', N'Nguyễn Thị Y', 'nguyenthiY@gmail.com', '0123456790'),
('NTT03', 'ND03', 'MP03', N'Phạm Văn Z', 'phamvanZ@gmail.com', '0123456701'),
('NTT04', 'ND04', 'MP04', N'Lê Thị W', 'lithiw@gmail.com', '0123456702'),
('NTT05', 'ND05', 'MP05', N'Nguyễn Văn V', 'nguyenvanV@gmail.com', '0123456703'),
('NTT06', 'ND06', 'MP06', N'Trần Thị U', 'tranthiu@gmail.com', '0123456704'),
('NTT07', 'ND07', 'MP07', N'Phạm Văn T', 'phamvant@gmail.com', '0123456705'),
('NTT08', 'ND08', 'MP08', N'Lê Thị S', 'lithis@gmail.com', '0123456706'),
('NTT09', 'ND09', 'MP09', N'Nguyễn Văn R', 'nguyenvanR@gmail.com', '0123456707'),
('NTT10', 'ND10', 'MP10', N'Trần Thị Q', 'tranthiq@gmail.com', '0123445667'),
('NTT11', 'ND11', 'MP11', N'Trần Thị A', 'tranthia@gmail.com', '0123456788'),
('NTT12', 'ND12', 'MP12', N'Nguyễn Văn B', 'nguyenvanB@gmail.com', '0123456791'),
('NTT13', 'ND13', 'MP13', N'Phạm Thị C', 'phamthiC@gmail.com', '0123456792'),
('NTT14', 'ND14', 'MP14', N'Lê Văn D', 'levand@gmail.com', '0123456793'),
('NTT15', 'ND15', 'MP15', N'Nguyễn Thị E', 'nguyenthie@gmail.com', '0123456794'),
('NTT16', 'ND16', 'MP16', N'Trần Văn F', 'tranvanf@gmail.com', '0123456795'),
('NTT17', 'ND17', 'MP17', N'Phạm Thị G', 'phamthig@gmail.com', '0123456796'),
('NTT18', 'ND18', 'MP18', N'Lê Thị H', 'lethih@gmail.com', '0123456797'),
('NTT19', 'ND19', 'MP19', N'Nguyễn Văn I', 'nguyenvani@gmail.com', '0123456798'),
('NTT20', 'ND20', 'MP20', N'Trần Thị J', 'tranthij@gmail.com', '0123456799');

INSERT INTO CHU_TRO VALUES 
(N'CT001', 'Nguyễn Văn A', N'0912345678', 'nguyenvana@example.com'),
(N'CT002', 'Trần Thị B', N'0987654321', 'tranthib@example.com'),
(N'CT003', 'Lê Văn C', N'0901234567', 'levanc@example.com'),
(N'CT004', 'Phạm Thị D', N'0934567890', 'phamthid@example.com'),
(N'CT005', 'Hoàng Văn E', N'0943219876', 'hoangvane@example.com'),
(N'CT006', 'Đặng Thị F', N'0971122334', 'dangthif@example.com'),
(N'CT007', 'Võ Văn G', N'0967890123', 'vovang@example.com'),
(N'CT008', 'Ngô Thị H', N'0956677889', 'ngothih@example.com'),
(N'CT009', 'Bùi Văn I', N'0944556677', 'buivani@example.com'),
(N'CT010', 'Đỗ Thị K', N'0922334455', 'dothik@example.com'),
(N'CT011', 'Mai Văn L', N'0911223344', 'maivanl@example.com'),
(N'CT012', 'Lý Thị M', N'0988997766', 'lythim@example.com'),
(N'CT013', 'Trịnh Văn N', N'0933445566', 'trinhvann@example.com'),
(N'CT014', 'Tạ Thị O', N'0909090909', 'tatheo@example.com'),
(N'CT015', 'Huỳnh Văn P', N'0949494949', 'huynhvanp@example.com'),
(N'CT016', 'Lâm Thị Q', N'0969696969', 'lamthiq@example.com'),
(N'CT017', 'Cao Văn R', N'0979797979', 'caovanr@example.com'),
(N'CT018', 'Nguyễn Thị S', N'0919191919', 'nguyenthis@example.com'),
(N'CT019', 'Trương Văn T', N'0929292929', 'truongvant@example.com'),
(N'CT020', 'Phan Thị U', N'0939393939', 'phanthiu@example.com')

INSERT INTO HOP_DONG  VALUES 
('MHD01', 'ND01', 'NTT01', '2023-01-01', '2024-01-01', 15000000),
('MHD02', 'ND02', 'NTT02', '2023-02-01', '2024-02-01', 16000000),
('MHD03', 'ND03', 'NTT03', '2023-03-01', '2024-03-01', 17000000),
('MHD04', 'ND04', 'NTT04', '2023-04-01', '2024-04-01', 18000000),
('MHD05', 'ND05', 'NTT05', '2023-05-01', '2024-05-01', 19000000),
('MHD06', 'ND06', 'NTT06', '2023-06-01', '2024-06-01', 20000000),
('MHD07', 'ND07', 'NTT07', '2023-07-01', '2024-07-01', 21000000),
('MHD08', 'ND08', 'NTT08', '2023-08-01', '2024-08-01', 22000000),
('MHD09', 'ND09', 'NTT09', '2023-09-01', '2024-09-01', 23000000),
('MHD10', 'ND10', 'NTT10', '2023-10-01', '2024-10-01', 24000000),
('MHD11', 'ND11', 'NTT11', '2023-11-01', '2024-11-01', 25000000),
('MHD12', 'ND12', 'NTT12', '2023-12-01', '2024-12-01', 26000000),
('MHD13', 'ND13', 'NTT13', '2024-01-01', '2025-01-01', 27000000),
('MHD14', 'ND14', 'NTT14', '2024-02-01', '2025-02-01', 28000000),
('MHD15', 'ND15', 'NTT15', '2024-03-01', '2025-03-01', 29000000),
('MHD16', 'ND16', 'NTT16', '2024-04-01', '2025-04-01', 30000000),
('MHD17', 'ND17', 'NTT17', '2024-05-01', '2025-05-01', 31000000),
('MHD18', 'ND18', 'NTT18', '2024-06-01', '2025-06-01', 32000000),
('MHD19', 'ND19', 'NTT19', '2024-07-01', '2025-07-01', 33000000);


INSERT INTO DICH_VU (maDichVu, tenDichVu, moTa, gia) VALUES   
('MDV01', N'Dịch vụ dọn phòng', N'Dọn dẹp phòng hàng tuần', 500000),
('MDV02', N'Dịch vụ giặt ủi', N'Giặt và ủi quần áo', 300000),
('MDV03', N'Dịch vụ internet', N'Cung cấp internet tốc độ cao', 200000),
('MDV04', N'Dịch vụ truyền hình', N'Cung cấp truyền hình cáp', 250000),
('MDV05', N'Dịch vụ ăn uống', N'Cung cấp bữa ăn hàng ngày', 1000000),
('MDV06', N'Dịch vụ bảo trì', N'Sửa chữa và bảo trì thiết bị', 400000),
('MDV07', N'Dịch vụ xe đưa đón', N'Dịch vụ đưa đón sân bay', 600000),
('MDV08', N'Dịch vụ tổ chức sự kiện', N'Tổ chức tiệc và sự kiện', 1500000),
('MDV09', N'Dịch vụ tư vấn', N'Tư vấn về nhà trọ', 700000),
('MDV10', N'Dịch vụ bảo vệ', N'Cung cấp dịch vụ bảo vệ 24/7', 800000),
('MDV11', N'Dịch vụ vệ sinh', N'Dọn dẹp vệ sinh khu vực chung', 350000),
('MDV12', N'Dịch vụ vận chuyển', N'Dịch vụ chuyển đồ đạc', 550000),
('MDV13', N'Dịch vụ giữ xe', N'Dịch vụ giữ xe cho khách thuê', 100000),
('MDV14', N'Dịch vụ giao đồ ăn', N'Giao đồ ăn tận phòng', 150000),
('MDV15', N'Dịch vụ massage', N'Massage thư giãn cho khách thuê', 700000),
('MDV16', N'Dịch vụ hỗ trợ 24/7', N'Hỗ trợ khách hàng 24/7', 400000),
('MDV17', N'Dịch vụ chăm sóc cây cảnh', N'Chăm sóc cây cảnh trong khuôn viên', 300000),
('MDV18', N'Dịch vụ thay ga giường', N'Thay ga giường và chăn mền định kỳ', 200000),
('MDV19', N'Dịch vụ cung cấp nước uống', N'Cung cấp nước uống cho phòng', 50000),
('MDV20', N'Dịch vụ phòng tập thể dục', N'Cung cấp phòng tập thể dục cho khách thuê', 1200000);


INSERT INTO GIAO_DICH VALUES
('MGD01', 'NTT01', '2023-01-05', '2023-01-10', 0, 1500000),
('MGD02', 'NTT02', '2023-02-05', '2023-02-10', 0, 1600000),
('MGD03', 'NTT03', '2023-03-05', '2023-03-10', 0, 1700000),
('MGD04', 'NTT04', '2023-04-05', '2023-04-10', 0, 1800000),
('MGD05', 'NTT05', '2023-05-05', '2023-05-10', 0, 1900000),
('MGD06', 'NTT06', '2023-06-05', '2023-06-10', 0, 2000000),
('MGD07', 'NTT07', '2023-07-05', '2023-07-10', 0, 2100000),
('MGD08', 'NTT08', '2023-08-05', '2023-08-10', 0, 2200000),
('MGD09', 'NTT09', '2023-09-05', '2023-08-10', 0, 2200000),
('MGD10', 'NTT10', '2023-10-05', '2023-10-10', 0, 2400000),
('MGD11', 'NTT11', '2023-11-05', '2023-11-10', 0, 2500000),
('MGD12', 'NTT12', '2023-12-05', '2023-12-10', 0, 2600000),
('MGD13', 'NTT13', '2024-01-05', '2024-01-10', 0, 2700000),
('MGD14', 'NTT14', '2024-02-05', '2024-02-10', 0, 2800000),
('MGD15', 'NTT15', '2024-03-05', '2024-03-10', 0, 2900000),
('MGD16', 'NTT16', '2024-04-05', '2024-04-10', 0, 3000000),
('MGD17', 'NTT17', '2024-05-05', '2024-05-10', 0, 3100000),
('MGD18', 'NTT18', '2024-06-05', '2024-06-10', 0, 3200000),
('MGD19', 'NTT19', '2024-07-05', '2024-07-10', 0, 3300000),
('MGD20', 'NTT20', '2024-08-05', '2024-08-10', 0, 3400000);


INSERT INTO CHI_TIET_GIAO_DICH VALUES
('MCT01', 'MGD01', 'MDV01', '2023-01-10', 1, 500000),  
('MCT02', 'MGD02', 'MDV02', '2023-01-10', 2, 300000),  
('MCT03', 'MGD03', 'MDV03', '2023-01-10', 1, 200000), 
('MCT04', 'MGD04', 'MDV04', '2023-02-10', 1, 500000),  
('MCT05', 'MGD05', 'MDV05', '2023-02-10', 1, 1000000), 
('MCT06', 'MGD06', 'MDV06', '2023-03-10', 1, 1000000), 
('MCT07', 'MGD07', 'MDV07', '2023-04-10', 1, 400000),  
('MCT08', 'MGD08', 'MDV08', '2023-05-10', 1, 600000),  
('MCT09', 'MGD09', 'MDV09', '2023-06-10', 1, 1500000), 
('MCT10', 'MGD10', 'MDV10', '2023-07-10', 1, 700000), 
('MCT11', 'MGD11', 'MDV11', '2023-08-10', 1, 800000), 
('MCT12', 'MGD12', 'MDV12', '2023-09-10', 1, 500000), 
('MCT13', 'MGD13', 'MDV13', '2023-10-10', 1, 300000), 
('MCT14', 'MGD14', 'MDV14', '2023-11-10', 1, 250000), 
('MCT15', 'MGD15', 'MDV15', '2023-12-10', 1, 700000), 
('MCT16', 'MGD16', 'MDV16', '2024-01-10', 1, 400000), 
('MCT17', 'MGD17', 'MDV17', '2024-02-10', 1, 350000), 
('MCT18', 'MGD18', 'MDV18', '2024-03-10', 1, 200000), 
('MCT19', 'MGD19', 'MDV19', '2024-04-10', 1, 50000), 
('MCT20', 'MGD20', 'MDV20', '2024-05-10', 1, 1200000);

create index idx_TenDangNhap on NGUOI_DUNG (tenDangNhap)
create index idx_Email_ND on NGUOI_DUNG (Email)
create index idx_TenNhaTro on NHA_TRO (tenNhaTro)
create index idx_MaNhaTro on PHONG (maNhaTro)
create index idx_TenPhong on PHONG (tenPhong)
create index idx_MaNguoiDung_NTT on NGUOI_THUE_TRO (maNguoiDung)
create index idx_MaPhong_NTT on NGUOI_THUE_TRO (maPhong)
create index idx_Email_NTT on NGUOI_THUE_TRO (Email)
create index idx_MaNguoiDung_HD on HOP_DONG (maNguoiDung)
create index idx_MaNguoiThueTro_HD on HOP_DONG (maNguoiThueTro)
create index idx_NgayBatDau on HOP_DONG (NgayBatDau)
create index idx_NgayKetThuc on HOP_DONG (NgayKetThuc)
create index idx_TenDichVu on DICH_VU (tenDichVu)
create index idx_MaNguoiThueTro_GD on GIAO_DICH (maNguoiThueTro)
create index idx_NgayGiaoDich on GIAO_DICH (NgayGiaoDich)
create index idx_NgayHetHan on GIAO_DICH (NgayHetHan)
create index idx_MaGiaoDich on CHI_TIET_GIAO_DICH (maGiaoDich)
create index idx_MaDichVu ON CHI_TIET_GIAO_DICH (maDichVu);

select* from NGUOI_DUNG
select* from NGUOI_THUE_TRO
select* from HOP_DONG
select* from NHA_TRO
select* from CHU_TRO
select* from PHONG
select* from GIAO_DICH
select* from CHI_TIET_GIAO_DICH
select* from DICH_VU

-- Cac cau lenh truy van 

-- Dem so luong phong ( Group By )
select maPhong, tenPhong, count(*) as SoLuongPhong 
from PHONG 
group by maPhong, tenPhong;

-- Lay thong tin hop dong va nguoi dung tu bang nguoi dung 
select HOP_DONG.maNguoiDung, tenNguoiDung, maHopDong, NgayBatDau, NgayKetThuc
from NGUOI_DUNG inner join HOP_DONG on NGUOI_DUNG.maNguoiDung = HOP_DONG.maNguoiDung
where NgayKetThuc > getdate();

-- Giai doan 4 : Xay dung cac chuc nang quan ly du lieu 
-- insert into da nhap o tren
-- Truy van thong tin NGUOI_THUE_TRO ho 'Nguyễn' ( SELECT )
-- (Cuong)
select tenNguoiThue, Email, std 
from NGUOI_THUE_TRO
where tenNguoiThue like N'Nguyễn%';
-- Cap nhat so dien thoai NGUOI_THUE_TRO ( UPDATE )
update NGUOI_THUE_TRO
set std = '0987654321'
where maNguoiThueTro = 'NTT01';
-- Xoa 1 nguoi thue tro ( DELETE )
delete from NGUOI_THUE_TRO
where maNguoiThueTro = 'NTT01';
-- Dem tong so phong ( COUNT, GROUP BY )
select maNhaTro, count(*) as TongSoPhong
from PHONG
group by maNhaTro;
-- Tinh tong tien tat ca phong tro (SUM)
select sum(tienPhong) as TongTienTatCa
from PHONG
-- Tinh tien trung binh cua cac phong (AVG)
select maNhaTro, avg(tienPhong)	as TrungBinhTienPhong
from PHONG
group by maNhaTro


--(Yen)
--Truy van NHA_TRO co ma nha tro la 'NT03'
SELECT *
FROM NHA_TRO
WHERE maNhaTro = 'NT03';

--Cập nhật giá tiền phòng của một phòng
UPDATE PHONG
SET tienPhong = 3500000
WHERE maPhong = 'MP021';

--Xóa một người thuê trọ từ bảng NGUOI_THUE_TRO
DELETE FROM NGUOI_THUE_TRO
WHERE maNguoiThueTro = 'NTT01';
-- DEM
SELECT PHONG.maNhaTro, tenNhaTro, COUNT(*) as SoLuongPhong
FROM PHONG
INNER JOIN NHA_TRO  ON PHONG.maNhaTro = NHA_TRO.maNhaTro
GROUP BY PHONG.maNhaTro, tenNhaTro;

--TONG
SELECT SUM(tong_tien) as TongDoanhThu
FROM GIAO_DICH
WHERE YEAR(NgayGiaoDich) = '2024';

--TB
SELECT AVG(tong_tien) as TrungBinhDoanhThu
FROM GIAO_DICH
WHERE YEAR(NgayGiaoDich) = '2024';

--BAOCAO
SELECT 
    MONTH(NgayGiaoDich) as Thang, 
    SUM(tong_tien) as DoanhThu
FROM GIAO_DICH
WHERE YEAR(NgayGiaoDich) = '2024'
GROUP BY MONTH(NgayGiaoDich)
ORDER BY Thang;


