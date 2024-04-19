#include <bits/stdc++.h>
using namespace std;
#define max_Heap(x) priority_queue<x, vector<x>, less<x>>
#define min_Heap(x) priority_queue<x, vector<x>, greater<x>>
typedef long long ll;
typedef unsigned long long ull;
typedef pair<int, int> PII;
typedef pair<long long, long long> PLL;
const double PI = acos(-1);

const int maxn = 5e3 + 6;
const int maxm = 5e3 + 6;

int n, m; // 点的个数，有向边的个数

struct edge
{
    int to, len; // to为边的指向，len为边的长度即边权
};

vector<edge> e[maxn]; // 存储以点i为起点的边

ll minDis[maxn]; // 从起点到第i个点的最短路长度
bool vis[maxn];  // 第i个点是否在队列中
int cnt[maxn];   // 记录某个点的入队次数，若次数大于等于n，存在负环

bool spfa()
{
    memset(minDis, 0x3f, sizeof(minDis));
    minDis[0] = 0; // 以超级源点为起点
    queue<int> q;
    q.push(0);
    vis[0] = 1;
    cnt[0]++;
    while (!q.empty())
    {
        int st = q.front();
        q.pop();
        vis[st] = 0;          // 已出队，vis赋值0
        for (edge eg : e[st]) // 遍历以st为起点的所有有向边
        {
            int ed = eg.to;
            int weight = eg.len;
            if (minDis[st] + weight < minDis[ed]) // 判断是否可以更新最短路长度
            {
                minDis[ed] = minDis[st] + weight;
                if (!vis[ed]) // 如果已经在队列中，则不需要再加入队列
                {
                    q.push(ed);
                    vis[ed] = 1;      // 记录在队列中
                    cnt[ed]++;        // 加入队列的次数++
                    if (cnt[ed] >= n) // 入队次数>=n，存在负环，返回0
                    {
                        return 0;
                    }
                }
            }
        }
    }

    return 1; // 不存在负环，返回1
}

int main()
{
    ios::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);

    cin >> n >> m;
    int u, v, w; // 从u到v的权值为w的有向边
    while (m--)
    {
        cin >> v >> u >> w;
        e[u].push_back({v, w});
    }
    // 以0为超级源点，该点到其他所有点的距离设置为0
    for (int i = 1; i <= n; i++)
    {
        e[0].push_back({i, 0});
    }

    if (spfa()) // 最短路的答案即为方程的一组解
    {
        for (int i = 1; i <= n; i++)
        {
            if (i != n)
                cout << minDis[i] << ' ';
            else
                cout << minDis[i] << '\n';
        }
    }
    else // 有负环，则无解
        cout << "NO" << '\n';

    return 0;
}
