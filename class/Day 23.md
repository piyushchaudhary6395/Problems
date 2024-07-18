# DP
## Fibonaaci Series
```cpp
#include <bits/stdc++.h>
using namespace std;

int fib(int n)
{
    if (n <= 1)
        return n;

    return fib(n - 1) + fib(n - 2);
}

int main()
{
    int n = 9;
    cout << n << "th Fibonacci Number: " << fib(n);
    return 0;
}
```
O(2^n)

Using DP

```cpp
#include <bits/stdc++.h>
using namespace std;

int fib(int n, vector<int> &dp;)
{
    if (n <= 1)
        return n;

	if(dp[n] != -1)
		return dp[n];

    return dp[n] = fib(n - 1) + fib(n - 2);
}

int main()
{
    int n = 9;
    vector<int> dp(n, -1);
    cout << n << "th Fibonacci Number: " << fib(n, dp);
    return 0;
}
```
Since we are solving each problem one time and the no. of problems are from 1 to N. So,
T: O(N)
S: O(N)

## DP Types
### Top-Down
It is recursive + memoization.
Starts from problem to sub problem. Then sub problem to problem.

### Bottom-Up
It is iterative + tabulation.
Starts from sub problem then problem.

We know iteration is better than recursion. So our aim is to always write the bottom up approach. Because  then we will 0 stack space due to recursion.
### Recursive To Iterative
1. See base case and initialize it.
2. Loop from bottom to N.
3. Repeat the recurrence.

While making DP, make a note of the state of DP. Meaning what variables are changing in each recursion call.

## Fibonacci (Bottom-Up)
```cpp
#include <bits/stdc++.h>
using namespace std;

int main()
{
    int n = 9;
    vector<int> dp(n + 1, -1);
    dp[0] = 0;
    dp[1] = 1;
    
    for(int i = 2; i <= n; i++)
	    dp[i] = dp[i - 1] + dp[i - 2];


	cout << dp[n] << endl;
}
```

## Climbing Stairs

## Min Cost Climbing Stairs
### Recursive
We will start from N and reach 0 and 1. We can do it vice versa but then we would have to make to separate recursion calls.


```cpp
vector<int> min_cot(N, cost);
int a = min_cost(N - 1, cost[N - 1]);
int b;
if(N - 2 >= 0)
	b = min_cost(N - 2, cost[N - 2]);
```
