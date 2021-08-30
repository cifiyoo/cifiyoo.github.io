#### K站中转内最便宜的航班

有` n` 个城市通过一些航班连接。给你一个数组 `flights` ，其中 `flights[i] = [fromi, toi, pricei]` ，表示该航班都从城市 `fromi` 开始，以价格 `toi` 抵达 `pricei`。

现在给定所有的城市和航班，以及出发城市 `src` 和目的地 `dst`，你的任务是找到出一条最多经过 k 站中转的路线，使得从 `src` 到 `dst` 的 价格最便宜 ，并返回该价格。 如果不存在这样的路线，则输出 -1。
链接：https://leetcode-cn.com/problems/cheapest-flights-within-k-stops

```c++
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
	const int INF = 1e9;
	vector<vector<int>> dp(k+2,vector<int>(n,INF));
	dp[0][src] = 0;
	for(int i = 1; i <= k + 1; ++ i){
		dp[i][src] = 0;//经过i次中转从src到达src的费用。
		for(const auto& x : flights)
			dp[i][x[1]] = min(dp[i][x[1]],dp[i-1][x[0]] + x[2]);
	}
	return dp[k+1][dst] >= INF ? -1 : dp[k+1][dst];
    }
};
```

##### 题解：

`dp[k][cur]`是经过`k`次中转到达当前城市`cur`的最小费用。可知`dp[k][cur]=dp[k-1][last]+cost`，所以`dp`公式为，`dp[k][cur]=min(dp[k][cur],dp[k-1][last]+cost)`.

另外，`const auto& x : flights`的写法需要学习。