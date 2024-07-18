## Coin Change 2
write recursive, DP and iterative code.

Recursive
```cpp
class Solution {
public:
int solve(vector<int> &coins, int amount, int sum = 0, int i = 0) {
	if(i >= coins.size()) {
		if(sum == amount) return 1;

	return 0;
	}

	int a = solve(coins, amount, sum, i+1);
	int b = 0;
	
	if(sum + coins[i] <= amount)
		b = solve(coins, amount, sum + coins[i], i);

	return a + b;
}
int change(int amount, vector<int>& coins) {
	return solve(coins, amount, dp);
	}
};
```

With DP
```cpp
class Solution {
public:
int solve(vector<int> &coins, int amount, vector<vector<int>> &dp, int sum = 0, int i = 0) {

	if(i >= coins.size()) {
		if(sum == amount) return 1;
			
		return 0;
	}
		
	if(dp[i][sum] != -1)
		return dp[i][sum];
	
	int a = solve(coins, amount, dp, sum, i+1);
	int b = 0;
	
	if(sum + coins[i] <= amount)
		b = solve(coins, amount, dp, sum + coins[i], i);
	
	return dp[i][sum] = a + b;
}

int change(int amount, vector<int>& coins) {
	vector<vector<int>> dp(coins.size(), vector<int>(amount + 1, -1));

oins.size()) {

if(sum == amount) return 1;

  

return 0;

}

  

if(dp[i][sum] != -1)

return dp[i][sum];

  

int a = solve(coins, amount, dp, sum, i+1);

int b = 0;

  

if(sum + coins[i] <= amount)

b = solve(coins, amount, dp, sum += coins[i], i);

return dp[i	return solve(coins, amount, dp);
	}
};
```

Iterative.
```cpp
d[n][amount] = 1;
for(i = 0; i < amount; i + 1)
	dp[n][i] = 0;
	
for(i = N - 1; i >= 0; i--) {
	for(j = amount; j >= 0; j--) {
		int a = dp[i + 1][j];
		
		if(j + coins[i] <= amount)
			dp[i][j + coins[i]];

		dp[i][j] = a + b;
	}
}

return dp[0][0];
```

## D-Knapsack 1 (`atcoder`)
Recursive
```cpp
vector<vector<long long>> dp(, vector<int>(, -1));
long long func(vector<int> &weights, vector<int> &cost, int amount, int i = 0, int sum = 0) {
	if(i == N) return 0;
	
	func(weights, cost, i+1, sum);
	
	if(sum + weights[i] <= amount)
		ans = max(ans, func(weights, cost, i+1, sum+weights[i]) + cost[i]);

	return ans;
}
```

Iterative
```cpp
for(i = 0; i <= amount; i++)
	dp[n][i] = 0;

for(i = n - 1; i >= 0; i--) {
	for(j = amount; j >= 0; j--) {
		dp[i][j] = dp[i+1][j]; // skip

		if(j + weights[i] <= amount)
			dp[i][j] = max(dp[i][j], dp[i+1][j+weights[i]] + cost[i]); // choose
	}
}

return dp[0][0];
```

## Rod Cutting (`GFG`)
Recursive
```cpp
int func(int N, vector<int> &price) {
	if(N == 0)
		return 0;

	int ans = 0;
	for(int i = 1; i <= N; i++) {
		if(N - i >= 0)
			ans = max(ans, func(N-i, price) + price[i])
	}

	return ans;
}
```

With DP.
```cpp

int func(int N, vector<int> &price) {
	if(N == 0)
		return 0;

	int ans = 0;
	for(int i = 1; i <= N; i++) {
		if(N - i >= 0)
			ans = max(ans, func(N-i, price) + price[i - 1])
	}

	return ans;
}
```
S.C O(n)
T.C O(n^2)

Iterative.
```cpp
dp[0] = 0;
for(i = 1; i <= N; i++) {
	ans = 0;
	for(j = 1; j <= N; j++) {
		if(i - j >= 0)
			ans = max(ans, dp[i-j] + price[j-1]);
	}
}

return dp[N];
```

## Longest Common Sub-sequence
```cpp
int func(string s1, string s2, int i = 0, int j = 0) {
	if(i == n || j == m)
		return = 0;

	if(s1[i] != s2[j]) {
		return max(func(s1, s2, i + 1, j), func(s1, s2, i, j + 1));
	}
	else
		return func(s1, s2, i + 1, j + 1) + 1;
}
```

```cpp
class Solution {
public:
int longestCommonSubsequence(string s1, string s2) {
	vector<vector<int>>dp(s1.size()+1, vector<int>(s2.size()+1));
	
	int n = s1.size();
	int m = s2.size();
	
	for(int i = 0; i <= m; i++)
		dp[n][i] = 0;
	
	for(int i = 0; i <= n; i++)
		dp[i][m] = 0;
	
	for(int i = n - 1; i >= 0; i--) {
		for(int j = m - 1; j >= 0; j--) {
		if(s1[i] == s2[j])
			dp[i][j] = dp[i+1][j+1] + 1;
		else
			dp[i][j] = max(dp[i+1][j], dp[i][j+1]);

		}
	}

	return dp[0][0];
	}
};
```

## The Longest Common Sub-sequence (Hacker Rank)
```cpp
vector<int> longestCommonSubsequence(vector<int> s1, vector<int> s2) {
vector<vector<int>>dp(s1.size()+1, vector<int>(s2.size()+1));

int n = s1.size();
int m = s2.size();

  

for(int i = 0; i <= m; i++)

dp[n][i] = 0;

  

for(int i = 0; i <= n; i++)

dp[i][m] = 0;

  

for(int i = n - 1; i >= 0; i--) {

for(int j = m - 1; j >= 0; j--) {

if(s1[i] == s2[j])

dp[i][j] = dp[i+1][j+1] + 1;

else

dp[i][j] = max(dp[i+1][j], dp[i][j+1]);

}

}

int i = 0, j = 0;

vector<int> ans;

  

while(i < n && j < m) {

if(s1[i] == s2[j]) {

ans.push_back(s1[i]);

i += 1;

j += 1;

}

else {

if(dp[i+1][j] > dp[i][j+1])

i++;

else

j++;

}

}

return ans;

}

```