# ==Number Theory==

## Find All Divisors Of N
### Brute
O(N)

### Better
If we go till root N, our number will be in pairs
Ex:-
N = 36
==1 2 3 4 6== | 9 12 18 36
1-> 36 (N / 1)
2-> 18 (N / 2)
3-> 12 (N / 3)
4-> 9 (N / 4)
6 (N / N)

O(sqrt(n))
```cpp
for(int i = 1; i * i <= N; i++) {
	if(N % i == 0) {
		cout << i << " ";
		if(i != N / i)
			cout << N / i << endl;
	}
}
```

## Prime Number Or Not
### Brute
O(N)

### Better
O(sqrt(n))

If no number is dividing the number till root N. Then even after root N the numbers won't divide it because we know that they come in pairs.

## Find All Prime Factors Of N
### Brute
O(N)

### Better
O(sqrt(N))

## Check If N Is A Perfect Square

1. for(1->N)
2. for(1->sqrt(n))
3. N will be a perfect square if square root of N multiplied by itself equals N.
4. Binary Search O(log n)
5. Odd number of divisors


## Using Prime Factors Find Count Of Divisors, Sum of Divisors, Product Of Divisors
N = p^a q^b y^c
a,b,c are given

### Count Of Divisors
(a + 1) * (b + 1)

### Sum Of Divisors
(p^a+1 - 1/ p-1) * (q^b+1 - 1 / q-1)

### Product Of Divisors
N^F/2 (F = even)
N^F/2 * sqrt(N) (F = odd)

## Number Of Prime Number From 1 To N
## Brute
O(N * sqrt(N))

## Optimal
Sieve

## Given An Array From 1 To N Find the number that appears twice
### Brute
Sum from 1 to n. Then subtract from array's sum.

### Better
XOR from 1 to n then XOR array elements. Then XOR each other.
```cpp
#include <bits/stdc++.h>
using namespace std;


```
### Optimal
