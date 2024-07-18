## Continuing Modulo
b^-1 is called modulo multiplicative inverse.
`b^-1 = Pow(b, M - 2) % M` (when M is Prime)
If M not prime then use Extended Euclid A `gcd(b, M)` (should be co-prime)

## Binary Exponentiation
### Recursive
```cpp
#include <bits/stdc++.h>
using namespace std;

long long pow(int num, int power)
{
	if(power == 0) return 1;

	if(power == 1) return num;

	int ans = pow(num, power / 2);

	if(power % 2 == 0)
		return ans * ans;
	else
		return num * ans * ans; 
}

int main()
{
	cout << pow(10, 2);
}
```
O(log b)
### Iterative
split b into its binary representation and only multiply a when `ith` bit is 1.
a^b
3^7
3^111
3^3 * 3^2 * 3^1

```cpp
int ans = 1

while(b > 0) {
	if(b % 2 == 1)
		ans *= a % M;
	
	b >> 1; // right shift or b /= 2;
	a = (a * a) % M;
}
```
O(log b)

1. If a is very large
	then do a % M
2. If M is very large
	ex-> M  = 1e^18 + 7
	overflow can occur (in a and b). a's range (M - 1) and b's range is also (M - 1). Can't multiply them but we can add them.
	```cpp
 	for(i = 1; i<= b; i++)
	 	ans = (ans + a) % M
	// but now multiplying two number is taking O(b)
```
	we need binary multiplication.
	```cpp
	long long multi(a, b) {
		if(b == 0) return 0;

		long long k = multi(a, b / 2);
		k = (k + k) % M;
		if(b % 2 == 0)
			return k;
		else
			return ; // i guess a += a;
	}
```

3. If b is very large
	we want to calculate a^b^c % M. Also (a^b^c) % M != (a^ (b^c % M)) % M
	We need to do:
	(a^(b^c % phi(M))) % M
	phi(M) is (Euler TF). If M is prime phi(M) = M - 1.


