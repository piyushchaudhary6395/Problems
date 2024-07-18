Questions like next greater element, next smaller element, previous smaller element, previous greater element: Can be solved using stack using stack.
# Daily Temperatures
## Brute O(n^2)

## Optimal
### Approach

- Initialize an array `results` to store the number of days until a warmer day for each day's temperature.
- Initialize an empty stack to keep track of indices.
- Iterate through each temperature in the array.
    - While the stack is not empty and the current temperature is greater than the temperature at the index on the top of the stack:
        - Update the result for the index at the top of the stack with the difference between the current index and the index on the top of the stack.
        - Pop the index from the stack.
    - Push the current index onto the stack.
- After the iteration, the `results` array contains the number of days until a warmer day for each given day.

### Complexity

- Time complexity: O(n), where n is the number of temperatures.
- Space complexity: O(n), as the stack can have at most n elements.

```cpp
int size = temperatures.size();
        vector<int> ans(size);
        stack<int> s;

        for(int i = 0; i < size; i++) {
            while(!s.empty() && temperatures[s.top()] < temperatures[i]) {
                ans[s.top()] = i - s.top();
                s.pop();
            }

            s.push(i);
        }

        return ans;
    }
```


## Largest Rectangle in Histogram

## Sliding Window Maximum

## Reverse Linked List
