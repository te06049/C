# C

## 1. 이차원함수와 배열

~~~ c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void init_arr(double arr[][4], int row, int col);
double sum_arr(double arr[][4], int row, int col);
void print_arr(double arr[][4], int row, int col);
void colsum_arr(double arr[][4], int row, int col);
void rowsum_arr(double arr[][4], int row, int col);
double maxsum_arr(double arr[][4], int row, int col);
void main(void){
	double arr[3][4];
	init_arr(arr, 3, 4);
	puts("배열의 모든 성분");
	print_arr(arr, 3, 4);
	puts("");
	sum_arr(arr, 3, 4);
	puts("");
	puts("배열의 열의 합");
	colsum_arr(arr, 3, 4);
	puts("");
	puts("배열의 행의 합");
	rowsum_arr(arr, 3, 4);
	puts("");
	printf("배열의 행별 합이 가장 큰 행: %.0lf\n", maxsum_arr(arr, 3, 4));
}

//배열의 성분을 0.0~10.0의 난수로 초기화 하는 함수
void init_arr(double arr[][4], int row, int col){
	int i, j;
	srand(time(NULL));

	for(i=0;i<row;i++){
		for(j=0;j<col;j++){
			arr[i][j] = rand()%101/10.0;
		}
	}
}
//배열의 모든 성분을 출력하는 함수
void print_arr(double arr[][4], int row, int col){
	int i, j;

	for(i=0;i<row;i++){
	    for(j=0;j<col;j++){
		printf("%.1lf  ",arr[i][j]);
		}
		puts("");
	}
}
//배열의 모든 성분의 합을 반환하는 함수
double sum_arr(double arr[][4], int row, int col){
	int i, j;
	double sum=0;
	for(i=0;i<row;i++){
		for(j=0;j<col;j++){
			sum+=arr[i][j];
		}
	}
	return printf("배열의 모든 성분의 합: %.1lf\n",sum);
}
//배열의 열별 합을 출력하는 함수
void colsum_arr(double arr[][4], int row, int col){
	double colsum;
	int i, j;
	for(j=0;j<col;j++){
		colsum=0;
		for(i=0;i<row;i++){
		colsum+=arr[i][j];
	   }
	printf("%d열의 합: %.1lf", j+1, colsum);
	puts("");
    }
}
//배열의 행별 합을 출력하는 함수
void rowsum_arr(double arr[][4], int row, int col){
	double rowsum;
	int i, j;
	for(i=0;i<row;i++){
		rowsum=0;
		for(j=0;j<col;j++){
			rowsum+=arr[i][j];
		}
		printf("%d행의 합: %.1lf",i+1, rowsum);
		puts("");
	}

}
//배열의 행별 합이 가장 큰 행을 반환하는 함수
double maxsum_arr(double arr[][4], int row, int col){
	double rowsum, max=0, r=0;
	int i, j;
	for(i=0;i<row;i++){
		rowsum=0;
		for(j=0;j<col;j++){
			 rowsum+=arr[i][j];
			if(max<rowsum) r=i;
		}
	}
	return r+1;
}

~~~
이차원 함수와 배열에 관해 배웠던 코드를 모두 합해서 실현한 코드이다.
