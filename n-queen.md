[原题链接---acwing](https://www.acwing.com/problem/content/description/845/)

#### 思路&想法：

DFS最重要的就是顺序，涉及到顺序一般就是用DFS，每一个DFS一定对应一棵搜索树。

##### Q:为什么会想到DFS呢？

##### A：因为DFS一般都是处理全排列的问题，假如有4个不同的数字，找出这4个不同的数字组成的所有的排列，其实也就相当于在4*4的棋盘去搜索，找到不同行，不同列的数字的组合。我们也可以人手演算，一个个枚举这16种情况，我们在进行枚举的时候，也是一个位置处理完了，才会处理下一个位置，这样不会轻易漏掉任何一种情况，枚举完成后剔除掉不符合规则的排列，DFS和BFS也是做这个事情的，只不过我们用代码实现了人的思想，让for循环去做那些重复的工作，我们就可以不用那么累了。

```c++
#include<iostream>
using namespace std; 
const int N =20;
int n;//每行需要放一个棋子，棋盘n*n的
char plan[N][N];
bool col[N],dig[N],ndig[N];//开辟3个数组用来记录列，正对角线，负对角线是否已经放过元素

//DFS模板
void dfs(int u){
	if(u==n){//输出棋盘
		for(int i=0;i<n;i++){
			for(int j=0;j<n;j++){
					cout<<plan[i][j];
			}
			cout<<endl;
			
		} 
		puts("");
		return;
	}
	
	for(int i=0;i<n;i++){//一列一列的循环 
		if(!col[i]&& !dig[u+i]&& !ndig[n-u+i]){//注意下标不能有负值
			plan[u][i]='Q';
			col[i]=dig[u+i]=ndig[n-u+i]=true;
			dfs(u+1);
			col[i]=dig[u+i]=ndig[n-u+i]=false;
			plan[u][i]='.';
			
		}
	}
} 
int main(){
	cin>>n; 
	for(int i=0;i<n;i++){
		for(int j=0;j<n;j++){
			plan[i][j]='.';
		}
	}
	dfs(0);
	return 0;
} 

```

