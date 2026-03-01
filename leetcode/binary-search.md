# Binary Search
https://www.1point3acres.com/bbs/forum.php?mod=redirect&goto=findpost&ptid=678970&pid=14151702

https://leetcode.com/problems/binary-search/solutions/423162/Binary-Search-101-The-Ultimate-Binary-Search-Handbook/

Key concepts:
- Search array
- Search range

Key patterns:
- Searching in sorted/rotated arrays


## Tricks
### `<=` vs `<` (binary search boundaries)
- `while (left <= right)` treats the search range as a closed interval (`[left, right]`). This checks all valid indices. The loop stops when `left > right`, and `left` points to the insertion position or indicates "not-found".
    - Updates: `left = mid + 1` or `right = mid - 1`.
    - Best for: exact matches (Does targer exist?)
- `while (left < right)` treats the search range as a half-open interval (`[left,right)`), where `right` is one past the last valid index. The loop stops when `left==right`, effectively narrowing toward a boundary point.
    - Updates: `left = mid + 1` or `right=mid`.
    - Best for: boundary searches (first true, last false, lower bound, upper bound).

https://medium.com/my-leetcode/binary-search-boundaries-explained-why-loop-conditions-and-range-types-matter-fbcd51a66b3e

