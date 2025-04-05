

### 🔍 **Problem Statement :**
You're given an array `nums`, and you need to calculate the **sum of XOR values of all subsets** of this array.

Each subset (including the empty one) should be considered, and for each subset, we calculate the **XOR** of its elements. Then sum all those XORs together.

---

### ✅ **Key Observations & Intuition:**

1. **Subsets and XOR**:
   - A set of `n` elements has `2^n` subsets.
   - For example, for `[5,1,6]`:
     - Subsets: [], [5], [1], [6], [5,1], [5,6], [1,6], [5,1,6]
     - XORs: 0, 5, 1, 6, 5^1, 5^6, 1^6, 5^1^6 → sum all these.

2. **Brute-force approach is acceptable for small inputs**:
   - Since `nums.length <= 12` (in constraints), we can afford to **generate all subsets** using recursion or bitmasking.

3. **XOR properties make recursive traversal elegant**:
   - XOR is **associative** and **commutative**, and `a ^ a = 0`.
   - We can **use DFS** or **bitmasking** to traverse all subsets, track the XOR so far, and sum it up.

---

### 💡 **Approach 1: Recursive DFS (Backtracking)**

We explore all subsets by either **including** or **excluding** each element.

```java
class Solution {
    public int subsetXORSum(int[] nums) {
        return dfs(nums, 0, 0);
    }

    private int dfs(int[] nums, int index, int currentXOR) {
        if (index == nums.length) {
            return currentXOR;  // base case: add XOR of one subset
        }

        // Include nums[index] in XOR
        int include = dfs(nums, index + 1, currentXOR ^ nums[index]);
        // Exclude nums[index] from XOR
        int exclude = dfs(nums, index + 1, currentXOR);

        return include + exclude;
    }
}
```

---

### 🧠 **Time Complexity:**

- There are `2^n` subsets → `O(2^n)` calls.
- Each call is constant work → overall time: `O(2^n)`.
- For `n <= 12`, it's **very fast** in practice.

---

### ✨ Example Walkthrough: `[1, 3]`

- Subsets:
  - `[]` → 0
  - `[1]` → 1
  - `[3]` → 3
  - `[1,3]` → 1 ^ 3 = 2  
- Total sum: `0 + 1 + 3 + 2 = 6` ✅

