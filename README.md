#include<stdio.h>
#include<stdlib.h>
#include<malloc.h>
#include<string.h>
using namespace std;

struct QLSach {
	char MaSSach[255];
	char TenSach[255];
	char TacGia[255];
	char TenGiaiThuong[255];
	int NamXB, SL, NamNhanGT;
	QLSach *ptr;
};

void Start();
void ThemDSach(QLSach **QLS);
void Menu();
void XuatDS(QLSach* QLS);
int KT(char A[], char B[]);
void inTu(char A[]);
void XoaManHinh();
void TongSoSach(QLSach *QLS);

int main()
{
	Start();
	return 0;
}

void Start()
{
	int chose;
	QLSach *QLS = NULL;
	while(true)
	{
		chose = 0;
		Menu();
		scanf("%d",&chose);
		if(chose == 1)
			ThemDSach(&QLS);
		if(chose == 2)
			XuatDS(QLS);
		if(chose == 3)
			TongSoSach(QLS);
		/*if(chose == 4)
			ThemTTGiaiThuong(&QLS);
		if(chose == 5)
			XuatTTGiaiThuong(&QLS);
		if(chose == 6)
			XoaDSach(&QLS);
		if(chose == 7)
			XuatTTTheoNamvaTen(&QLS);
		if(chose == 8)
			LuuDS(&QLS);
		if(chose == 9)
			MoFile(&QLS);*/
		if(chose == 10)
			XoaManHinh();
		if(chose == 11)
		{
			printf("------Ban chon thoat chuong trinh-----");
			exit(0);
		}
	}
}
void Menu()
{
	printf("____________Menu______________\n");
	printf("1. Khoi tao danh sach\n");
	printf("2. Tim kiem thong tin sach theo MSSach\n");
	printf("3. Tinh tong so sach co trong thu vien\n");
	printf("4. Them thong tin ve giai thuong\n");
	printf("5. Tim kiem thong tin giai thuong\n");
	printf("6. Xoa mot dau sach\n");
	printf("7. Tim kiem MaSSach, TenSach sach theo nam va ten tac gia\n");
	printf("8. Luu danh sach vao o dia\n");
	printf("9. Mo file da co tren dia va nhap thong tin\n");
	printf("10.Xoa man hinh\n");
	printf("11.Thoat\n");
	printf("------------------------------------------------------------\n");
	printf("Nhap luu chon cua ban: ");
}
void ThemDSach(QLSach **QLS)
{
	int n, i;
	QLSach* qls;
	char temp[255];
	printf("------Ban chon khoi tao danh sach------\n");
	printf("Nhap so dau sach them vao: ");
	scanf("%d",&n);
	qls = (QLSach*)malloc(n*sizeof(QLSach));
	if(qls == NULL)
		printf("EROR!! \n");
	for(i = 0 ; i < n ; i++)
	{
		printf("Nhap ma so sach thu %d: ", i+1);
		gets(temp);
		gets(qls->MaSSach);
		printf("Nhap ten sach thu %d: ", i+1);
		gets(qls->TenSach);
		printf("Nhap ten tac gia cua sach thu %d: ", i+1);
		gets(qls->TacGia);
		printf("Nhap nam xuat ban cua sach thu %d: ", i+1);
		scanf("%d",&qls->NamXB);
		printf("Nhap so luong cua sach thu %d: ", i+1);
		scanf("%d",&qls->SL);
		qls->ptr = (*QLS);
		*QLS = qls;
		printf("\n");
	}
	if(QLS != NULL)
		printf("Them thanh cong !!!\n");
}
void XuatDS(QLSach* QLS)
{
	printf("------Ban chon xuat danh sach theo ma so sach------\n");
	if(QLS == NULL)
	{
		printf("Danh sach rong !!!!\n");
		system("pause");
		exit(0);
	}
	char temp[255];
	QLSach *qls = QLS;
	qls = QLS;
	printf("Vui long nhap ma so sach can tim: ");
	gets(temp);
	gets(temp);
	printf("MaSSach\t\tTacGia\t\tNamXB\t\tSL\n");
	while(qls != NULL)
	{
		int check = KT(temp, qls->MaSSach);
		if(check == 1)
		{
			inTu(qls->MaSSach);
			printf("\t\t");
			inTu(qls->TacGia);
			printf("\t\t");
			printf("%d\t\t", qls->NamXB);
			printf("%d\n",qls->SL);
		}
		qls = qls->ptr;
	}
	printf("Xuat danh sach thanh cong !!!\n");
}
int KT(char A[], char B[])
{
	int len = strlen(A);
	for(int i = 0 ; i <  len ; i++)
		if(A[i] != B[i])
			return 0;
	return 1;
}
void inTu(char A[])
{
	int len = strlen(A);
	printf("%s", A);
}
void XoaManHinh()
{
	printf("------Ban chon xoa man hinh-----\n");
	system("pause");
	system("cls");
}
void TongSoSach(QLSach *QLS)
{
	int sum = 0;
	QLSach *qls;
	qls = QLS;
	while(qls != NULL)
	{
		sum += qls->SL;
		qls = qls->ptr;
	}
	printf("Tong so luong sach la %d\n", sum);
	printf("Tinh tong so sach thanh cong!!!!\n");
}
