## Topics
quick sort
Linked List
## Questions
Counting Bits
xoring and clearing
set the rightmost unset bit
Partition Array According to Given Pivot (do this)

## Counting Bits
```js
Given an integer `n`, return _an array_ `ans` _of length_ `n + 1` _such that for each_ `i` (`0 <= i <= n`)_,_ `ans[i]` _is the **number of**_ `1`_**'s** in the binary representation of_ `i`.

**Example 1:**

**Input:** n = 2
**Output:** [0,1,1]
**Explanation:**
0 --> 0
1 --> 1
2 --> 10

**Example 2:**

**Input:** n = 5
**Output:** [0,1,1,2,1,2]
**Explanation:**
0 --> 0
1 --> 1
2 --> 10
3 --> 11
4 --> 100
5 --> 101

**Constraints:**

- `0 <= n <= 105`
```

To understand how the line `ans[i] = ans[i >> 1] + (i & 1);` counts the number of set bits (1s) in the binary representation of an integer `i`, let's walk through a dry run example.

### Explanation:

- `i >> 1`: This operation right-shifts the bits of `i` by 1 position, effectively dividing `i` by 2 and discarding the least significant bit (LSB).
- `i & 1`: This operation checks whether the LSB of `i` is 1. If `i` is odd, `i & 1` is 1; otherwise, it is 0.
- `ans[i] = ans[i >> 1] + (i & 1)`: This relation states that the number of set bits in `i` is the same as the number of set bits in `i >> 1` (which is already computed and stored in `ans[i >> 1]`) plus 1 if the LSB of `i` is 1.

### Dry Run Example:

Let's consider `n = 5` and see how the array `ans` is filled.

#### Initial State:

- `ans[0] = 0` because 0 in binary is `0`.

#### Step-by-Step Calculation:

1. **i = 1**:
    
    - Binary: `1`
    - `i >> 1`: `0` (Binary of `1 >> 1` is `0`)
    - `i & 1`: `1` (Least significant bit is `1`)
    - `ans[1] = ans[0] + 1 = 0 + 1 = 1`
    - `ans` becomes `[0, 1]`
2. **i = 2**:
    
    - Binary: `10`
    - `i >> 1`: `1` (Binary of `2 >> 1` is `1`)
    - `i & 1`: `0` (Least significant bit is `0`)
    - `ans[2] = ans[1] + 0 = 1 + 0 = 1`
    - `ans` becomes `[0, 1, 1]`
3. **i = 3**:
    
    - Binary: `11`
    - `i >> 1`: `1` (Binary of `3 >> 1` is `1`)
    - `i & 1`: `1` (Least significant bit is `1`)
    - `ans[3] = ans[1] + 1 = 1 + 1 = 2`
    - `ans` becomes `[0, 1, 1, 2]`
4. **i = 4**:
    
    - Binary: `100`
    - `i >> 1`: `2` (Binary of `4 >> 1` is `10`)
    - `i & 1`: `0` (Least significant bit is `0`)
    - `ans[4] = ans[2] + 0 = 1 + 0 = 1`
    - `ans` becomes `[0, 1, 1, 2, 1]`
5. **i = 5**:
    
    - Binary: `101`
    - `i >> 1`: `2` (Binary of `5 >> 1` is `10`)
    - `i & 1`: `1` (Least significant bit is `1`)
    - `ans[5] = ans[2] + 1 = 1 + 1 = 2`
    - `ans` becomes `[0, 1, 1, 2, 1, 2]`

```cpp
class Solution {
public:
    vector<int> countBits(int n) {
        vector<int> ans(n+1);
        ans[0] = 0;

        for(int i = 1; i <= n; i++)
            ans[i] = ans[i >> 1] + (i & 1);

        return ans;
    }
};
```