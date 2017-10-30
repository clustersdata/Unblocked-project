# Unblocked-project-

Unblocked project 

Problem Description

某省调查城镇交通状况，得到现有城镇道路统计表，表中列出了每条道路直接连通的城镇。省政府“畅通工程”的目标是使全省任何两个城镇间都可以实现交通（但不一定有直接的道路相连，只要互相间接通过道路可达即可）。问最少还需要建设多少条道路？

Input

测试输入包含若干测试用例。每个测试用例的第1行给出两个正整数，分别是城镇数目N ( < 1000 )和道路数目M；随后的M行对应M条道路，每行给出一对正整数，分别是该条道路直接连通的两个城镇的编号。为简单起见，城镇从1到N编号。

注意:两个城市之间可以有多条道路相通,也就是说

3 3
1 2
1 2
2 1

这种输入也是合法的

当N为0时，输入结束，该用例不被处理。

Output

对每个测试用例，在1行里输出最少还需要建设的道路数目。


Sample Input

4 2 1 3 4 3 3 3 1 2 1 3 2 3 5 2 1 2 3 5 999 0 0

Sample Output

1 0 2 998 

代码：
#include <stdio.h>

#include <string.h>

#define MAX 2000

int n,m;

int arr[MAX][2];

int res[MAX];

int set;

void proc()

{

    int i,j;
    
    int rest;
    
    set=1;    //用来统计集合个数
    
    memset(res,0,(n+1)*sizeof(int));
    
    res[arr[0][0]]=res[arr[0][1]]=1;
    
    for(i=1;i<=set;i++)
    
    {
    
        for(j=0;j<m;j++)
        
        {
        
            if(res[arr[j][0]]*res[arr[j][1]]) continue;    //当前数据已经归类，则不进行任何操作
            
            if(res[arr[j][0]]==i||res[arr[j][1]]==i) 
            
            {
            
                res[arr[j][0]]=res[arr[j][1]]=i;    //对数据进行集合划分
                
                j=-1;                    //从第一组元素开始继续遍历
                
            }
            
        }
        
        for(j=0;j<m;j++)
        
            if(res[arr[j][0]]*res[arr[j][1]]==0) break; //遇到首或尾没有归类的情况的时候跳出
            
        if(j<m) set++;                 //如果当前还有没有归类的情况新增加一个集合
        
        else break;                    //如果当前数据全部归类则跳出所有循环
        
        for(j=0;j<m;j++)
        
        {
        
            if(res[arr[j][0]]*res[arr[j][1]]==0){ res[arr[j][0]]=res[arr[j][1]]=set;   break;  }
            
        }
        
    }
    
    rest=0;
    
    for(i=1;i<=n;i++)         if(res[i]==0) rest++;
    
    if(m==0) printf("%d\n",n-1);
    
    else if(rest==0)
    
    {
    
        if(set==1) printf("0\n");
        
        else printf("%d\n",set-1);
        
    }
    
    else printf("%d\n",rest+set-1);
    
}

int main()

{

    int i;
    
    scanf("%d",&n);
    
    while(n)
    
    {
    
        scanf("%d",&m);
        
        for(i=0;i<m;i++) scanf("%d %d",&arr[i][0],&arr[i][1]);
        
        proc();
        
        scanf("%d",&n);
        
    }
    
    return 0;
    
}

