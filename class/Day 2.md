# Topics
Binary Search
## Search A 2d Matrix
```js
You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` _if_ `target` _is in_ `matrix` _or_ `false` _otherwise_.

You must write a solution in `O(log(m * n))` time complexity.

**Example 1:**

**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
**Output:** true

**Example 2:**

**Input:** matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
**Output:** false

**Constraints:**

- `m == matrix.length`
- `n == matrix[i].length`
- `1 <= m, n <= 100`
- `-104 <= matrix[i][j], target <= 104`
```

## Brute
O(n * m)
## Better
O(n * log m)
Apply binary search on each row
## Optimal
O(log (m * n))
consider the whole 2d array as a sorted 1d array and apply binary search

To map index with coordinate:
row = mid / col
col = mid % col

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int r = matrix.size();
        int c = matrix[0].size();
        int low = 0;
        int high = (r*c) - 1;

        while(low <= high) {
            int mid = low + (high - low) / 2;
            int row = mid / c;
            int col = mid % c;

            if(matrix[row][col] == target)
                return true;

            else if(matrix[row][col] < target)
                low = mid + 1;

            else
                high = mid - 1;
        }

        return false;
    }
};
```

## Aggressive Cows
```js
You are given an **array** consisting of **n integers** which denote the position of a **stall**. You are also given an **integer** **k** which denotes the number of aggressive cows. You are given the task of **assigning stalls to k cows** such that the **minimum distance between any two of them is the maximum possible**.  
The first line of input contains two space-separated integers **n** and **k**.  
The second line contains **n** space-separated integers denoting the position of the stalls.

**Example 1:**

**Input:**
n=5 
k=3
stalls = [1 2 4 8 9]
**Output:**
3
**Explanation:**
The first cow can be placed at stalls[0], 
the second cow can be placed at stalls[2] and 
the third cow can be placed at stalls[3]. 
The minimum distance between cows, in this case, is 3, 
which also is the largest among all possible ways.

**Example 2:**

**Input:**
n=5 
k=3
stalls = [10 1 2 7 5]
**Output:**
4
**Explanation:**
The first cow can be placed at stalls[0],
the second cow can be placed at stalls[1] and
the third cow can be placed at stalls[4].
The minimum distance between cows, in this case, is 4,
which also is the largest among all possible ways.

**Your Task:**  
Complete the function int solve(), which takes integer n, k, and a vector stalls with n integers as input and returns the largest possible minimum distance between cows.

**Expected Time Complexity:** O(n*log(10^9)).  
**Expected Auxiliary Space:** O(1).  
  
**Constraints:**  
2 <= n <= 10^5  
2 <= k <= n  
0 <= stalls[i] <= 10^9
```

The pattern used here is called binary search on answer.
Given:
- Array
- Variables can be:
	- candies
	- cows
	- toffees
	- packages

Could ask about minimize/ maximize

We first sort the stalls, so that we can find our search space. We then set our search space using `low` and `high`. After that we implement binary search over the imaginary search space in search of potential gaps.

We know that at least one cow can be placed at the first stall whose `index` is 0 so `placed_cows = 1`. We then iterate over the stalls to check the gap between the current cow and the last placed cow.

If more than or equal to the specified cows are placed we return `true` indicating that we can do `low = mid + 1` so that we can search for the maximum gap. 
Explanation: If in 4 gaps all cows can be placed, those cows can be placed in a higher gap as well.

If less cows are placed than specified then vice versa of above statement.

```cpp
bool bS(vector<int> stalls, int cows, int mid) {
        int size = stalls.size();
        int placed_cows = 1;
        int index = 0;
        
        for(int i = 1; i < size; i++) {
            if (stalls[i] - stalls[index] >= mid) {
                placed_cows++;
                index = i;
            }
        }

        if(placed_cows >= cows)
            return true;
        
        return false;
    }

int main() {
	vector<int> stalls = {1, 2, 4, 8, 9};
	int k = 3;
    sort(stalls.begin(), stalls.end());
    int low = 1;
    int high = stalls[stalls.size() - 1] - stalls[0];
    int ans = INT_MIN;
        
    while(low <= high) {
        int mid = low + (high - low)  / 2;
            
        if(bS(stalls, k, mid) == true) {
            ans = max(ans, mid);
            low = mid  + 1;
        }
        else
            high = mid - 1;
    }
    
    return ans;
}
```

## Smallest Division Given A Threshold
```js
Given an array of integers `nums` and an integer `threshold`, we will choose a positive integer `divisor`, divide all the array by it, and sum the division's result. Find the **smallest** `divisor` such that the result mentioned above is less than or equal to `threshold`.

Each result of the division is rounded to the nearest integer greater than or equal to that element. (For example: `7/3 = 3` and `10/2 = 5`).

The test cases are generated so that there will be an answer.

**Example 1:**

**Input:** nums = [1,2,5,9], threshold = 6
**Output:** 5
**Explanation:** We can get a sum to 17 (1+2+5+9) if the divisor is 1. 
If the divisor is 4 we can get a sum of 7 (1+1+2+3) and if the divisor is 5 the sum will be 5 (1+1+1+2). 

**Example 2:**

**Input:** nums = [44,22,33,11,1], threshold = 5
**Output:** 44

**Constraints:**

- `1 <= nums.length <= 5 * 104`
- `1 <= nums[i] <= 106`
- `nums.length <= threshold <= 106`
```

We know that our search space's `low` value is 1 as division by 0 is not defined in maths. Our `high` value is the largest element of the array because if you divide with anything larger than the largest value of the array the ceil of the resultant will be same.

Now we implement binary search on our imaginary search space. 

If the current divisor or `mid` produces a `sum` <= `threshold`, we return true, that means we have to look towards the left of the search space because we have to find the smallest divisor that can produce a `sum` <= `threshold`.

If the current divisor or `mid` produces a `sum` > `threshold`, we return false, that means we have to look towards the right of the search space because any element towards the left will only increase the `sum`.

```cpp
class Solution {
public:
    bool bS(vector<int> nums, int threshold, int mid) {
        int size = nums.size();
        int sum = 0;

        for(int i = 0; i < size; i++)
            sum += ceil((double) nums[i] / (double) mid);

        if(sum > threshold)
            return false;

        return true;
    }

    int smallestDivisor(vector<int>& nums, int threshold) {
        sort(nums.begin(), nums.end());

        int ans = INT_MAX;
        int low = 1;
        int high = nums[nums.size() - 1];

        while(low <= high) {
            int mid = low + (high - low) / 2;

            if(bS(nums, threshold, mid)) {
                ans = min(ans, mid);
                high = mid - 1;
            }
            else
                low = mid + 1;
        }
  
        return ans;
    }
};
```
