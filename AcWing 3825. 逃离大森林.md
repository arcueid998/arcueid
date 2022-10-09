### AcWing 3825. 逃离大森林

#### 思路

走最短路径，绕路的话对面会在终点等你，肯定没有最短路优。关于答案，可以从终点开始广搜，记录下距离，答案就是到终点的距离小于等于你的最短路的饲养员数量。

#### 代码

```c
#include<bits/stdc++.h>
using namespace std;
int n,m,ans,endx,endy,f;
int mp[1005][1005],w[1005][1005];
char c;
queue<int>qx;
queue<int>qy;
int dx[4]={1,-1,0,0},dy[4]={0,0,1,-1};
int main(){
    scanf("%d%d",&n,&m);
    for(int i=1;i<=n;i++){
        for(int j=1;j<=m;j++){
            cin>>c;
            if(c>='0'&&c<='9')mp[i][j]=c-'0';
            if(c=='E')qx.push(i),qy.push(j);
            if(c=='T')w[i][j]=1;
            if(c=='S')endx=i,endy=j;
        }
    }
    while(!qx.empty()){
        int x=qx.front(),y=qy.front();
        qx.pop(),qy.pop();
        for(int i=0;i<4;i++){
            int wx=x+dx[i],wy=y+dy[i];
            if(wx<1||wx>n||wy<1||wy>m||w[wx][wy])continue;
            w[wx][wy]=w[x][y]+1;
            if(wx==endx&&wy==endy)f=w[wx][wy];
            if(!f||w[wx][wy]<=f){
                qx.push(wx),qy.push(wy);
                ans+=mp[wx][wy];
            }
        }
    }
    printf("%d\n",ans);
    return 0;
}
```

