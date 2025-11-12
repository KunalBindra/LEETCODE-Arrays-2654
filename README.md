# LEETCODE-Arrays-2654
---

### 🧠 First, What the Code Does

**Goal:**
Find the minimum number of operations to make all numbers in `nums` equal to 1 using a specific operation (each operation reduces two adjacent numbers into their gcd).

---

### 📦 Code Structure Summary

```java
class Solution {
    private int gcd(int a, int b) { ... }  // Standard Euclidean algorithm
}
```

---

### ⚙️ Step-by-Step Dry Run

Let’s test with an example:

```java
nums = [2, 6, 3, 4]
```

#### Step 1️⃣: Basic setup

* `n = 4`
* `count1 = 0`

#### Step 2️⃣: Count number of 1’s

Loop through nums:

* 2 → not 1
* 6 → not 1
* 3 → not 1
* 4 → not 1

So, `count1 = 0`

✅ No 1 present → we continue.

---

#### Step 3️⃣: Initialize

`minsteps = Integer.MAX_VALUE`

Now we’ll find the shortest subarray whose GCD becomes 1.

---

#### Step 4️⃣: Nested loops to find subarray GCD

Outer loop `i` goes from `0` to `n-1`.

---

##### For `i = 0`:

`gcdval = nums[0] = 2`

Now inner loop `j = i+1 = 1` → `3`:

* `j = 1`: gcd(2, 6) = 2 → not 1
* `j = 2`: gcd(2, 3) = 1 ✅

We found gcd == 1 at `j=2`.
So, `minsteps = min(∞, 2-0) = 2`

Then we `break` (stop inner loop).

---

##### For `i = 1`:

`gcdval = nums[1] = 6`

* `j = 2`: gcd(6, 3) = 3
* `j = 3`: gcd(3, 4) = 1 ✅

→ `minsteps = min(2, 3-1) = 2`
(no improvement)

---

##### For `i = 2`:

`gcdval = 3`

* `j = 3`: gcd(3, 4) = 1 ✅
  → `minsteps = min(2, 3-2) = 1` ✅
  (best so far)

---

##### For `i = 3`:

No `j` values left → skip.

---

#### Step 5️⃣: After loops

`minsteps = 1`

Check if `minsteps == Integer.MAX_VALUE` → ❌ (not true)

---

#### Step 6️⃣: Final answer

`return minsteps + (n - 1)`
→ `1 + (4 - 1)`
→ `1 + 3 = 4`

✅ **Output: 4**

---

### 🧩 Logic Explanation

* If the array **already contains some 1s**, we just need to make the rest 1 →
  `n - count1` operations.
* If no 1 exists:

  * We find the **shortest subarray** whose GCD becomes 1.
  * Suppose that subarray length is `L = j - i + 1`
  * It takes `L - 1` operations to make that segment a single `1`.
  * Then we still need `n - 1` total operations to make the whole array `1`.
  * So the formula becomes:
    **`minsteps + (n - 1)`**

---

### 🧮 Try Another Example

`nums = [2, 4, 6, 8]`

All are even → GCD of any subarray will never be 1.

→ `minsteps` stays `Integer.MAX_VALUE`

→ return `-1`

✅ Output: **-1**

---

### ✅ Summary Table

| Example   | Output | Explanation                                                                |
| --------- | ------ | -------------------------------------------------------------------------- |
| [2,6,3,4] | 4      | shortest gcd=1 subarray is [3,4] (len=2 → minsteps=1)                      |
| [1,2,3]   | 2      | already has 1 → only need n - count1 = 3 - 1 = 2                           |
| [2,4,6,8] | -1     | no gcd=1 subarray                                                          |
| [3,9,6,2] | 5      | subarray [6,2] gives gcd=2, [9,6,2] gives gcd=1 → minsteps=2 → total=2+3=5 |

---
