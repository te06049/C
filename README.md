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


## 2. 배열과 함수 실습2
```
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void init_arr(int arr[], int size);
void print_arr(int arr[], int size);
int sum(int arr[], int size);
int index(int arr[], int size);
void shuff(int arr[], int size);//return 안받고 print_arr로 출력가능하므로 void
void rot_left(int arr[], int size);
void rot_nleft(int arr[], int size, int n);
void rot_right(int arr[], int size);
void rot_nright(int arr[], int size, int n);

void main(void){
	int arr[5], n;
	init_arr(arr, 5);
	print_arr(arr, 5);
	printf("합: %d\n",sum(arr, 5));
	printf("최댓값의 인덱스: %d\n",index(arr, 5));
	printf("셔플: ");
	shuff(arr, 5);//셔플하고
	print_arr(arr, 5);//출력해라
	printf("왼쪽 로테이션: ");
	rot_left(arr, 5);
	print_arr(arr, 5);
	printf("오른쪽 로테이션: ");
	rot_right(arr, 5);
	print_arr(arr, 5);
	printf("왼쪽으로 93번 로테이션: ");
	rot_nleft(arr, 5, 93);
	print_arr(arr, 5);


	}
//배열 성분 n칸 왼쪽 로테이션
void rot_left(int arr[], int size){
	int i, tmp=arr[0];
	for(i=1;i<size;i++){
		arr[i-1]=arr[i];
	}
	arr[size-1]=tmp;
}
void rot_nleft(int arr[], int size, int n){
int i;
n%=size;
    for(i=0;i<n;i++){
		rot_left(arr, size);
    }
}
//배열 성분 n칸 오른쪽 로테이션
void rot_right(int arr[], int size){
	int i, tmp=arr[size-1];
	for(i=size-1;i>0;i--){
		arr[i]=arr[i-1];
	}
	arr[0]=tmp;
}
void rot_nright(int arr[], int size, int n){
int i;
n%=size;
	for(i=0;i<n;i++){
		rot_right(arr, size);
		}
}
//배열 성분 셔플링(shuffling)
void shuff(int arr[], int size){
	int i, tmp, r;
	for(i=0;i<size;i++){
		r=rand()%size;
		tmp=arr[i];
		arr[i]=arr[r];
		arr[r]=tmp;
	}
}

//배열의 최댓값의 인덱스를 반환하는 함수
int index(int arr[], int size){
	int max_arr=arr[0], i, j=0;
	for(i=1;i<size;i++){
		if(max_arr<arr[i]) {
			max_arr=arr[i];
			j=i;
		}
	}
	return j;
}
//배열의 모든 성분의 합을 반환하는 함수
int sum(int arr[], int size){
	int i, sum=0;
	for(i=0;i<size;i++){
		sum+=arr[i];
	}
		return sum;
}

//배열의 모든 성분을 출력하는 함수
void print_arr(int arr[], int size){
	int i;
	for(i=0;i<size;i++){
	printf("%d ",arr[i]);
	}
	puts("");
}
//배열의 성분을 -20에서 20까지의 난수로 초기화하는 함수
void init_arr(int arr[], int size){
	int i;	
	srand(time(NULL));
	for(i=0;i<size;i++){
	arr[i]=rand()%41-20;
	}
}
```
