# Topics
Bit Manipulation
Math needed for placements

## Count of factors of a number
Note: perfect squares have even factors and non perfect squares have odd factors.

Brute: O(n)
Till n

Better: O(n/2)
Till n/2

Optimal: O(squareRoot n)
n = 30
i      n      n/i
1 * 30 = 30
2 * 15 = 30
3 * 10 = 30
5 * 6 = 30
6 * 5 = 30 (repetiton starts around square root of n)
10 * 3 = 30
15 * 2 = 30
30 * 1 = 30

n = 36
. . .
when 6 * 6 arrives it will contribute 1 to the count of factors
. . .
```cpp
// Online C++ compiler to run C++ program online
#include <bits/stdc++.h>
using namespace std;

int main() {
    int n = 30;
    int sq = sqrt(n);
    int count  = 0;

    for(int i = 1; i <= sq; i++) {
        if(n % i == 0) {
            if(i == n/i)
                count++;
            else 
                count += 2;
        }
    }
    
    cout << count;
}
```

## Prime Or Not
Range of number is given, find out which of them are prime and which are not.

Better: O(n * root n) (i guess)

Optimal: O(n * log(log n)) (geek for geeks)
==Sieve of Eratosthenes==

We assume all numbers in the range are prime using bool array. Now we start from 2 and mark all its multiple as false in the array and we go up to square root of n.

```cpp
class Solution {
public:
    int countPrimes(int n) {
        vector<int> prime(n + 1, 1);
        
        for (int i = 2; i * i <= n; i++) {
            if (prime[i] == 1) {
                for (int j = i * i; j <= n; j += i) {
                    prime[j] = 0;
                }
            }
        }
        
        int cnt = 0;
        for (int i = 2; i < n; i++) {
            if (prime[i] == 1)
                cnt++;
        }

        return cnt;
    }
};
```

## Greatest Common Divisor
Brute: if n1 < n2
O(n1)

We will start from min(n1, n2) to 1, this way our first element will be our ans. We wont have to update the `ans` variable again and again.

==Eucledian==
## Bit Manipulation
### ==Homework==
## Single Number 2
==Brute:== O(n * 32)
Forming the number bit by bit. We count the no. of set bits in all the numbers of the array, since the duplicate number in the arrays appear three times they will be multiple of 3.

So at each bit position from `i = 0 -> 31`. we count the set bits at position `i` in each number. If they are a multiple of 3 that means that at that `ith` position in our single occuring number is 0. If they are not 0 that means that at that `ith` position in our single occuring number is 1, so we set it using the OR `|` operation.

To get the set bit at `ith` position in each number we are using left shift of 1 together with `&`.
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ans = 0;

        for(int i = 0; i < 32; i++) {
            int odd_count = 0;
            int size = nums.size();

            for(int j = 0; j < size; j++) {
                if((1 << i) & nums[j])
                    odd_count++;
            }

            if(odd_count % 3)
                ans = ans | (1 << i);
        }

        return ans;
    }
};
```

==Better:== O(n + (n log n)
Sort the array. Use sliding window of size 3 wherever the first element of the window is not equal to its last, break and the first element is your answer.
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int size = nums.size();

        // for(int i = 1; i < size; i = i + 3) {
        //     if(nums[i] != nums[i - 1])
        //         return nums[i - 1];
        // }


        //                  OR

        for(int i = 0; i < size; i = i + 3) {
            if(i + 2 < size) {
                if(nums[i] != nums[i + 2])
                    return nums[i];
            }
        }

        return nums[size - 1];
    }
};
```

==Optimal:== O(n)
We use two variables `ones` and `twos`. `ones` keep track of the elements that appear once and `twos` keep track of the elements that appear twice. We can also have `threes` but its not required. 

We need a way to add and delete elements from `ones` and `twos` because the elements that appears once needs to be added to `ones` if it does not exist in `twos` whereas if it appears twice it needs to deleted from `ones` and added to `twos`.

ones = (ones ^ arr[i]) & ~twos;
two = (twos ^ arr[i]) & ~ones;
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ones = 0;
        int twos = 0;
        int size = nums.size();

        for(int i = 0; i < size; i++) {
            ones = (ones ^ nums[i]) & ~twos;
            twos = (twos ^ nums[i]) & ~ones;
        }

        return ones;
    }
};
```
