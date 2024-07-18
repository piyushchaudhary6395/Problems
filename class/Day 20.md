Sieve works till 1e9
## Lowest Prime Factor Of A Number
From 1 to N print LPF of all numbers

We can do it by finding out the prime numbers by root n logic.

## Optimal
We can also use sieve here.
```cpp
int n = 24;
vector<int> LPF(n + 1, -1)
vector<bool> Prime(n + 1, 1)
Prime[1] = 0;

for(int i = 2; i <= n; i++) {
	if(Prime[i] == 1) {
		LPF[i] = i;
		for(int j = 2 * i; j <= n; j+i) {
			if(LPF[j] == -1)
				LPF[j] = i;
			Prime[j] = 0;
		}
	}
}
```

## Find All Divisors Of All Elements Of An Array
```cpp

```

## Brute
O(N * sqrt(N))

## Optimal
Using sieve
```cpp
// n is the maximum element of array
vector<vector<int>> ans(n);

for(int i = 2; i <= n; i++) {
	if(Prime[i] == 1) {
		LPF[i] = i;
		for(int j = i; j <= n; j = j + i) {
			Prime[j] = 0;
			ans[j].push_back(i);
		}
	}
}
// Now return ans[arr[i]] while looping over the given array to get all divisors of each element.
```
O(N * log N)


## Given An Array Find All The Prime Factors Of Each Element
## Brute
n sqrt(n)

## Optimal
find LPF of all elements till the maximum number of array. Then divide the array element with their LPF until no. becomes 1. With each division the LPF used for the current no. will be the prime factors of the original no.

It is exactly how you find prime factors of a number in math.
2 | 60
2 | 30
3 | 15
5 | 5
   | 1

```cpp

```
O(N log logN) + O(N log N)
O(N log N) (final complexity, since it is the worst case between them)

## Find GCD Of a And b
`euclid's algo`
```cpp
int gcd(a, b) {
	if(a == 0) return b;
	
	return gcd(b % a, a);
}
```
O(log min(a, b))

`a * b = gcd(a, b) * lcm(a, b)`
To find LCM just find GCD.

## Modulo
1. (a + b) % M = (a % M + b % M) % M 
(a % M + b % M) % M) this is what compiler does internally to calculate.

a % M = value ranges between (0 -> M - 1)
a = 2e9
b = 2e9
M = 2e9
a + b = 4e9 (integer can't store this)
so, (a + b) % M

2. (a - b) % M = (a % M - b % M + M) % M
3. (a * b) % M = (a % M * b % M) % M
4. (a / b) % M = (a % M / b % M) % M (this does not work, gives wrong output)

(a/b) % M = (a * (b inverse)) % M
