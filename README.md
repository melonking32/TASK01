通过动态数组实现托普利茨矩阵和三数之和
===
1.利用动态数组解决数据存放问题
---
编写一段代码，要求输入一个整数N，用动态数组A来存放2~N之间所有5或7的倍数，输出该数组。
代码：
```c
#include"stdio.h"
#include"stdlib.h"
int main()
{
    int n;
    scanf("%d",&n);
    int *p=(int*)malloc(1*sizeof(int));
    int k=0;
    int i=2;
    while(i<n)
    {
        if(i%5==0||i%7==0)
        {
            p[k]=i;
            k++;
            p=(int*)realloc(p,(1+k)*sizeof(int));
        }
        i++;
    }
    for(int j=0;j<k;j++)
        printf("%d ",p[j]);
    return 0;
}
```
2.托普利茨矩阵问题
---
如果一个矩阵的每一方向由左上到右下的对角线上具有相同元素，那么这个矩阵是托普利茨矩阵。

给定一个M x N的矩阵，当且仅当它是托普利茨矩阵时返回True。

代码：
```c
#include"stdio.h"
#include"stdlib.h"
int main()
{
    int m,n;
    scanf("%d %d",&m,&n);
    int a[m][n];
    for(int i=0;i<m;i++)
        for(int j=0;j<n;j++)
            scanf("%d",&a[i][j]);
    int l=1;
    for(int i=0;i<n;i++)
    {
        int y=i,x=m-1;
        while(x>=0&&y>=0)
        {
            if(a[x][y]!=a[m-1][i])
                {   
                    l=0;
                    break;
                }
            x--,y--;
        }
        
    }
    if(l==1)
        printf("TRUE");
    else
        printf("Flase");
    return 0;
    
}
```

3. 三数之和
---
https://leetcode-cn.com/problems/3sum/

给定一个包含 n 个整数的数组nums，判断nums中是否存在三个元素a，b，c，使得a + b + c = 0？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

代码：
```c
#include"stdio.h"
#include"stdlib.h"
int cmp(const void *a,const void *b){
    return (int*)a-(int*)b;
}
int main(){
    int n;
    scanf("%d",&n);
    int A[n];
    int B[10001]={0};
    int **result=(int**)malloc(1*sizeof(int*));
    int k=0;
    for(int i=0;i<1;i++)
        result[i]=(int *)malloc(sizeof(int)*n);
    for(int i=0;i<n;i++){
        scanf("%d",&A[i]);
        B[i]=1;
    }
    qsort(A,n,sizeof(A[0]),cmp);
    int i=0;
    int max=-1;
    while(A[i]<=0)
    {
        if(A[i]>max)
        {
            int j=i+1;
            int max2=-1;
            while(j<n&&A[j]<=-A[i])
            {
                if(B[0-A[i]-A[j]]==1&&A[j]>max2)
                  {
                        result[k][0]=A[i];
                        result[k][1]=A[j];
                        result[k][2]=0-A[i]-A[j];
                        k++;
                        result=(int**)realloc(result,(k+1)*sizeof(int*));
                        result[k]=(int*)malloc(sizeof(int)*3);
                        max2=A[j];
                    }
                //printf("%d %d %d\n",A[i],A[j],0-A[i]-A[j]);
                j++;
        }
        max=A[i];
        }
        i++;
    }
    for(int l=0;l<k;l++)
        printf("%d %d %d\n",result[l][0],result[l][1],result[l][2]);
    return 0;
}
```
