## Unique Paths
You coded the DP + recursive solution yourself.

## Minimum Falling Path Sum
DP + Recursive
```cpp
class Solution {
public:
int solve(vector<vector<int>>& matrix, vector<vector<int>>& dp, int r, int c, int j, int i = 0) {
		if(i == r)
			return 0;
	
		if(dp[i][j] != -1)
		return dp[i][j];
	
		int ans = 1e9;	  
		
		if(j - 1 >= 0)
			ans = min(ans, solve(matrix, dp, r, c, j - 1, i + 1) + matrix[i][j]);
		
		ans = min(ans, solve(matrix, dp, r, c, j, i + 1) + matrix[i][j]);
		
		if(j + 1 < r)
			ans = min(ans, solve(matrix, dp, r, c, j + 1, i + 1) + matrix[i][j]);
		
		return dp[i][j] = ans;
}

int minFallingPathSum(vector<vector<int>>& matrix) {
		vector<vector<int>>dp(matrix.size(), vector<int>(matrix[0].size(), -1));
		
		int ans = INT_MAX;
		
		for(int j = 0; j < matrix[0].size(); j++)
			ans = min(ans, solve(matrix, dp, matrix.size(), matrix[0].size(), j));  
		
		return ans;
	}
};
```

## Subset Sum Problem (GFG)
```cpp
vector<vector<int>>dp(n, vector<int>(max_sum)); // [n][1e4 + 1]
int subset(int i = 0, int sum = 0) {
	if(i == n) {
		if(sum == k) return 1;
		return 0;
	}

	int choose = subset(i + 1, sum + arr[i]);
	int not_choose = subset(i + 1, sum);

	return (choose | not_choose);
}
```

Iterative
```cpp
int n = arr.size();
vector<vector<int>>dp(n + 1, vector<int>(k));
dp[n][k] = 1;

for(int i = 0; i < k; i++)
	dp[n][i] = 0;

for(int i = n - 1; i >= 0; i--) {
	for(int j = 0; j <= k; j++) {
		dp[i][j] = dp[i + 1][j];
		if(j + arr[i] <= k)
			dp[i][j] += dp[i + 1][j + arr[i]];	// not if it is dp[i][j] = or dp[i][j] +=
	}
}
```

## Sub-sequence Sum
