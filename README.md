# 48. Rotate Image

## Problem Statement

Given an `n x n` 2D matrix representing an image, rotate the image by **90 degrees clockwise**.

You must rotate the image **in-place**, meaning you cannot allocate another 2D matrix.

### Example 1

Input:
```text
[
 [1,2,3],
 [4,5,6],
 [7,8,9]
]
```

Output:
```text
[
 [7,4,1],
 [8,5,2],
 [9,6,3]
]
```

### Example 2

Input:
```text
[
 [5,1,9,11],
 [2,4,8,10],
 [13,3,6,7],
 [15,14,12,16]
]
```

Output:
```text
[
 [15,13,2,5],
 [14,3,4,1],
 [12,6,8,9],
 [16,7,10,11]
]
```

---

## Approach

Instead of using an extra matrix, perform the rotation in two steps:

1. **Transpose the matrix**
   - Convert rows into columns.
   - Swap `matrix[i][j]` with `matrix[j][i]`.

2. **Reverse each row**
   - Reverse elements in every row.
   - This results in a 90° clockwise rotation.

### Visualization

Original Matrix:

```text
1 2 3
4 5 6
7 8 9
```

After Transpose:

```text
1 4 7
2 5 8
3 6 9
```

After Reversing Each Row:

```text
7 4 1
8 5 2
9 6 3
```

---

## Java Solution

```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // Reverse each row
        for (int i = 0; i < n; i++) {
            int left = 0, right = n - 1;

            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;

                left++;
                right--;
            }
        }
    }
}
```

---

## Complexity Analysis

- **Time Complexity:** `O(n²)`
- **Space Complexity:** `O(1)`

The solution modifies the matrix in-place without using any extra matrix.
