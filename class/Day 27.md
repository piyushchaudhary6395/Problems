## Longest Common Sub-String
Iterative.
```cpp
ans = 0;

for(i = n - 1; i >= 0; i--) {
	for(j = m - 1; j >= 0; j--) {
		if(s[i] == s[j])
			dp[i][j] = dp[i + 1][j+1]+1;
		else
			dp[i][j] = 0;

		ans = max(ans, dp[i][j]);
	}
}

return ans;
```

## Longest Palindromic Sub-Sequence
Find current string's reverse and take LCS.

## How many characters to insert in a string to make it a palindrome
we remove characters that are not palindrome and if we double the remaining characters our string will become palindrome.
N - LPS(s)

## Edit Distance

## Longest Increasing Sub-Sequence

## House Robber (1 to 5)

## Buy And Sell (1 to 6)

## Wildcard Matching

## Kadanes

## Domino Tiling

## Binary Tree Cameras

## Maximum Product Sub-Array

## Maximum Square Sub-Matrix

# Additional DP's If Interested

## Bit-mask DP

## Digit DP

## MCM DP

## Tree DP

