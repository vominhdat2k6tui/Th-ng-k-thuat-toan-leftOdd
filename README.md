# Th-ng-k-thuat-toan-leftOdd
#include <stdio.h>
#include<stdlib.h>
#include<time.h>


void leftOdd(int a[], int n, int *comps, int *shifts){
    int pos = 0;
    (*comps) = 0;
    (*shifts) = 0;
    for(int i = 0 ; i < n;i++){
        (*comps)++;
        if(a[i]%2 == 1){
            int temp = a[i];
            int j = i - 1;
            while(j >= 0){
                (*comps)++;
                if(a[j] %2 == 0){
                    (*shifts)++;
                    a[j+1] = a[j];
                    j--;
                }
                else {
                    break;
                }
            }
            a[j+1] = temp;
        }
    }
}


void randomArr(int a[], int n, int min , int max){
    for(int i = 0; i < n; i++){
        a[i] = min + rand()%(max - min + 1);
    }
}

int main() {
    srand(time(NULL));
   int n = 10;
   int a[1000];
   int sumcomps = 0,sumshifts = 0;
   int comps,shifts;
   int freqcomps[50] = {0};
   int freqshifts[50] = {0};
   int min = 0, max = 1000;
   for(int i = 0; i < 1000;i++){
       
       randomArr(a,n,min,max);
       leftOdd(a,n,&comps,&shifts);
       sumcomps += comps;
       sumshifts += shifts;
       freqcomps[comps]++;
       freqshifts[shifts]++;
     
       
   }
   
   double avgcomps =(double) sumcomps/1000;
   double avgshifts = (double) sumshifts/1000;
   printf("Bảng tần số : \n");
   for(int i = 0 ; i < 50;i++){
       printf("%d\t%d\t%d\n",i,freqcomps[i],freqshifts[i]);
   }
   printf("Comps trung binh : %f\n",avgcomps);
   printf("Shifts trung binh: %f\n",avgshifts);
    return 0;
}
