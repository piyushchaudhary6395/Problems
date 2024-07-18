## B- Frog 2 (`atcoder`)

```cpp
int jump(vector<int> arr, int k, int i = 0) {
	if(i == N -1)
		return 0;

	int ans = 1e9;

	for(int j = 1; j <= k; j++) {
		int net_distance = i + j;
		if(i + j < N)
			ans = min(ans, jump(arr, k, net) + abs(arr[net] - arr[i]));
	}

	return ans;
}
```
we have k choices.
O(k^n)

My state only consists `i`.
```cpp
vector<int> dp(N + 1, -1);
int jump(vector<int> arr, int k, int i = 0) {
	if(i == N -1)
		return 0;

	int ans = 1e9;
	if(dp[i] != -1)
		return dp[i];

	for(int j = 1; j <= k; j++) {
		int net_distance = i + j;
		if(i + j < N)
			ans = min(ans, jump(arr, k, net) + abs(arr[net] - arr[i]));
	}

	return dp[i] = ans;
}
```
Each state is running K loops.
O(N * K)
SC: O(N)

Iterative:
```cpp
vector<int> dp(N + 1);
dp[N - 1] = 0;

for(int i = N - 2; i >= 0; i--) {
	int ans = 1e9;
	
	for(int k = 1; j <= k; j++) {
		if(i + j < N)
			ans = min(ans, dp[i + j] + abs(A[i + j] - A[i]));
	}
    dp[i] = ans;
}

return dp[0];
```

## House Robber
We have to find maximum sub-sequence sum.

```cpp
int seq_sum(vector<int> arr,int i = 0) {
	if(i == N) return 0;
	
	int ans = -1e9;
	ans = seq_sum(arr, i+2) + arr[i];
	ans = max(ans, seq_sum(arr, i+1));

	return ans;
}
```
we have two choices at each step.
O(2^n)

Using DP:
```cpp
vector<int> dp(N + 1, -1);
int seq_sum(vector<int> arr,int i = 0) {
	if(i == N) return 0;

	if(dp[i] != -1)
		return dp[i];
	
	int ans = -1e9;
	ans = seq_sum(arr, i+2) + arr[i];
	ans = max(ans, seq_sum(arr, i+1));

	return dp[i] = ans;
}
```

Iterative:
```cpp
vector<int> dp(N + 2);
dp[N] = 0; 
dp[N + 1] = 0;

for(int i = N - 1; i >= 0; i--) {
	dp[i] max(dp[i + 1], dp[i + 2] + arr[i]);
}

return dp[0];
```

## C-Vacation (`atcoder`)
```cpp
int vacation(vector<int> arr, int i = 0;, int j = -1) {
	if(i == arr.size()) return 0;

	if(j == -1) {
		return max(vacation(arr, i + 1, 0) + arr[i][0], max(vacation(arr, i + 1, 1) + arr[i][1], vacation(arr, i + 1, 2) + arr[i][2]));
	}
	else if(j == 0) {
		return max(vacation(arr, i + 1, 1) + arr[i][1], vacation(arr, i + 1, 2) + arr[i][2])
	}
	else if(j == 1){
		return max(vacation(arr, i + 1, 0) + arr[i][0], vacatin(arr, i + 1, 2) + arr[i][2]);
	}
	else {
		return max(vacation(arr, i + 1, 0) + arr[i][0], vacation(arr, i + 1, 1) + arr[i][1]);
	}
}
```

Using DP:
We are doing `j + 1` so that we don't get runtime error because `-1` index dose not exist. Also because of this we have take the column size 5 instead of 4.
```cpp
vector<vector<int>> dp(N + 1, vector<int>(5, -1));
int vacation(vector<int> arr, int i = 0;, int j = -1) {
	if(i == arr.size()) return 0;

	if(dp[i][j + 1] != -1)
		return dp[i][j + 1];

	if(j == -1) {
		return dp[i][j + 1] = max(vacation(arr, i + 1, 0) + arr[i][0], max(vacation(arr, i + 1, 1) + arr[i][1], vacation(arr, i + 1, 2) + arr[i][2]));
	}
	else if(j == 0) {
		return dp[i][j + 1] = max(vacation(arr, i + 1, 1) + arr[i][1], vacation(arr, i + 1, 2) + arr[i][2])
	}
	else if(j == 1){
		return dp[i][j + 1] = max(vacation(arr, i + 1, 0) + arr[i][0], vacatin(arr, i + 1, 2) + arr[i][2]);
	}
	else {
		return dp[i][j + 1] = max(vacation(arr, i + 1, 0) + arr[i][0], vacation(arr, i + 1, 1) + arr[i][1]);
	}
}
```
Negative numbers cannot be `memoized`. So to `memoize` them, just add how much it is negative.

Iterative:
```cpp
vector<vector<int>> dp(N + 1, vector<int>(4));
dp[n][0] = 0;
dp[n][1] = 0;
dp[n][2] = 0;

for(int i = N - 1, i >= 0; i--) {
	dp[i][0] = max(dp[i + 1][1] + arr[i][1], dp[i + 1][2]) + arr[i][2];

	dp[i][1] = max(dp[i + 1][0] + arr[i][0], dp[i + 1][2]) + arr[i][2];

	dp[i][2] = max(dp[i + 1][1] + arr[i][1], dp[i + 1][0]) + arr[i][0];
}

return max(dp[0][0], max(dp[0][1], dp[0][2]));
```
