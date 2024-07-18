## Questions
N- queens
Sudoku Solver (you can try it as well, if you want)
## Insert Interval
```cpp
vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        int row = intervals.size();
        vector<vector<int>> ans;

        int i = 0;
        while(i < row && intervals[i][1] < newInterval[0]) {
            ans.emplace_back(intervals[i]);
            i++;
        }

        int start = newInterval[0];
        int end = newInterval[1];

        while(i < row && end >= intervals[i][0]) {
            start = min(start, intervals[i][0]);
            end = max(end, intervals[i][1]);
            i++;
        }

        ans.push_back({start, end});

        while(i < row) {
            ans.push_back({intervals[i][0], intervals[i][1]});
            i++;
        }

        return ans;
    }
```

## Valid Parentheses

## Implement Queue using Stacks

## Min stack

## Daily Temperatures

## Asteroid Collision
