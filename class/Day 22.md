## Bit Manipulation

## Convert N To Its Binary Representation
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
	int N = 5;
	while(N != 0) {
		if(N & 1)
			cout << "1" << " ";
		else
			cout << "0" << " ";

		N = N >> 1;
	}
}
```

## Toggle `Kth` Bit
Use XOR and bit masking.

## Set `kth` Bit
Use OR and bit masking
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int k = 1;
    int N = 9;
    N = N | (1 << k);
    
    vector<int> bits;
    while(N != 0) {
        if(N & 1)
            bits.push_back(1);
        else
            bits.push_back(0);
        N = N >> 1;
    }
    
    reverse(bits.begin(), bits.end());
    for(int bit : bits) {
        cout << bit << " ";
    }
}
```

## Unset `kth` Bit
Use AND and bit masking
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int k = 1;
    int N = 9;
    N = N & ~(1 << k);
    
    vector<int> bits;
    while(N != 0) {
        if(N & 1)
            bits.push_back(1);
        else
            bits.push_back(0);
        N = N >> 1;
    }
    
    reverse(bits.begin(), bits.end());
    for(int bit : bits) {
        cout << bit << " ";
    }
}
```

## Swap A And B Without Third Variable
A = A ^ B
B = A ^ B (A ^ B ^ B) (B will cancel out) (A)
A =  A ^ B (A ^ B ^ A) (A will cancel out) (B)

## Count Set Bits
There is a `STL` function to count this.
`__builtin_popcount(N)`

## Maximum Product of Word Lengths
O(n^2) is common among all.
## Brute
O(n^2) to check each combination of words. To check if there is something common between two words or not, we take a set and push all elements of 1st word then check these elements in 2nd word. If no word is found common between them then it is a potential answer.

## Better
We can make a map for each word and count each character frequency in them. O(n * l).
Then we loop on one of the map and check if there is anything common between them.

## Optimal
We want to compare two string in O(1). We use bit masking. Total unique characters are 26. We represent each character as a-> 2^0, z-> 2^25. Their sum is equal to 2^26 - 1. Each string can be represented using a number and its sum will be less than equal to 2^26 - 1.

Now how to compare these numbers ?

"abc"
2^0 + 2^1 + 2^2 = 7
We cannot produce sum 7 with any other character combination.
7 = 1 1 1(a present, b present, c present)
0 represents no present

a b c d ----- z ("abc")
1 1 1  0 ----- 0 (let p)
a b c d ---- x y z ("xyz")
0 0 0 0 ---- 1  1 1 (let q)

if(p & q == 0)
	nothing common
else
	something is common

```cpp
map<string, int> mp;
for(i = 0; i < size; i++) {
	ans = 0;
	string s = v[i];
	for(auto it: s) {
		int it = it - 'a';
		ans = ans | (1 << it);
	}
	mp[s] = it;
}

for(i = 0; i< sz; i++) {
	for(j = i + 1; j < sz; j++) {
		s1 = v[i], s2 = v[j];
		a = mp[s1], b = mp[s2];

		if(a & b == 0)
			ans = max(ans, s1.size() *  s2.size());
	}
}
```
