
#include <stdio.h>
#include "Header.h"

int print(void);
int jisuan(void);
int function(void);


int main(int argc, const char * argv[])
{
//    int a;
//    float b;
//     scanf("%d%f",&a,&b);
//    int c,d;
//    c=++a;
//    d=b++;
//    printf("a的值为:%d,b的值为:%d\nc的值为:%d,d的值为:%d\n",a,b,c,d);
    
//    int m=10,n= 6;
//    int p = m | n;
//    printf("p的值为:%d\n",p);

//    向左移1位相当于x2,右移1位相当于处2
//    int r=m >> 1;
//    int q=n << 2;
//    printf("r:%d,q:%d\n",r,q);
//     print();
//     jisuan();
//    function();
    
    int a=10,b=20,c=30;
    bool  d = a>b || b<c;
    
    printf("hello,world\n");
    return 0;
}

//打印等腰三角形
int print(void){
    int n;
    scanf("%d",&n);
    for(int i=1;i<=n;i++){
        for (int j=n;j>i;j--) {
            printf(" ");
        }
    
        for (int j=0 ; j<2*i-1 ; j++) {
            printf("*");
        }
        printf("\n");
    }
    return 0;
}
//计算两个数的和差积商
int jisuan(void){
    int m,n;
    scanf("%d%d",&m,&n);
    int a=m+n;
    int b=m-n;
    int c=m*n;
    int d=m/n;
    printf("m+n=%d,m-n=%d,m*n=%d,m/n=%d\n",a,b,c,d);
    return 0;
}


int function(void){
    //在控制体打印出 %
    char s;
    s='%';
    printf("%c\n",s);
    return 0;
}

