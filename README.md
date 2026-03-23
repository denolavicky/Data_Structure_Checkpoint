# Algorithm Documentation

## Table of Contents
- [Problem 1 — Sum of Distinct Elements](#problem-1--sum-of-distinct-elements)
- [Problem 2 — Dot Product](#problem-2--dot-product)

---

## Problem 1 — Sum of Distinct Elements(read.algo)

### Description
Given two sets of elements, find the sum of all **distinct** elements — meaning elements that appear in **only one** of the two sets (not both).

### Example
| | Values |
|---|---|
| **Set 1** | `[3, 1, 7, 9]` |
| **Set 2** | `[2, 4, 1, 9, 3]` |
| **Shared (ignored)** | `1, 3, 9` |
| **Distinct elements** | `7` (from Set 1), `2, 4` (from Set 2) |
| **Output** | `7 + 2 + 4 = 13` |

### Variable Declarations
| Variable | Type | Purpose |
|---|---|---|
| `set1[4]` | INTEGER array | Stores elements of the first set |
| `set2[5]` | INTEGER array | Stores elements of the second set |
| `sum` | INTEGER | Stores the running total of distinct elements |
| `found` | BOOLEAN | Flag to check if an element exists in the other set |
| `i, j` | INTEGER | Loop counters for the nested loops |

### Algorithm
```
BEGIN
  DECLARE set1[4]  : INTEGER   // first set
  DECLARE set2[5]  : INTEGER   // second set
  DECLARE sum      : INTEGER   // stores the total of distinct elements
  DECLARE found    : BOOLEAN   // flag to track if element exists in other set
  DECLARE i, j     : INTEGER   // loop counters

  // Initialize sets
  set1 = [3, 1, 7, 9]
  set2 = [2, 4, 1, 9, 3]
  sum = 0

  // Check elements in set1 that are NOT in set2
  FOR i = 0 TO length(set1) - 1
    found = FALSE
    FOR j = 0 TO length(set2) - 1
      IF set1[i] == set2[j] THEN
        found = TRUE
      END IF
    END FOR
    IF found == FALSE THEN
      sum = sum + set1[i]     // add to sum if not found in set2
    END IF
  END FOR

  // Check elements in set2 that are NOT in set1
  FOR i = 0 TO length(set2) - 1
    found = FALSE
    FOR j = 0 TO length(set1) - 1
      IF set2[i] == set1[j] THEN
        found = TRUE
      END IF
    END FOR
    IF found == FALSE THEN
      sum = sum + set2[i]     // add to sum if not found in set1
    END IF
  END FOR

  PRINT sum   // Output: 13
END
```

### How It Works
1. Loop through **Set 1** — for each element, check every element in Set 2
2. If it is **not found** in Set 2, add it to `sum`
3. Repeat the same process in reverse — loop through **Set 2** and check against Set 1
4. Print the final `sum`

---

## Problem 2 — Dot Product

### Description
The dot product (also called the scalar product) of two vectors is calculated by multiplying each pair of matching elements and adding all the results together.

```
v1 = [a, b, c]
v2 = [x, y, z]

dot product = (a×x) + (b×y) + (c×z)
```

> **Orthogonal vectors** are vectors whose dot product equals **zero**. This means the two vectors are perpendicular to each other.

### Example
| | Values |
|---|---|
| **v1** | `[1, 2, 3]` |
| **v2** | `[4, 5, 6]` |
| **Calculation** | `(1×4) + (2×5) + (3×6) = 4 + 10 + 18 = 32` |
| **Result** | `32 ≠ 0` → **NOT orthogonal** |

**Orthogonal example:**
| | Values |
|---|---|
| **v1** | `[1, 0]` |
| **v2** | `[0, 1]` |
| **Calculation** | `(1×0) + (0×1) = 0` |
| **Result** | `0` → **Orthogonal ✓** |

---

### Part 1 — Procedure

> Uses an `OUT` parameter — `ps` is passed **by reference** so the result is written back to the calling algorithm.

```
PROCEDURE dot_product(v1[] : REAL, v2[] : REAL, n : INTEGER, OUT ps : REAL)
  DECLARE i : INTEGER       // loop counter

  ps = 0                    // initialize ps to 0 before calculation
  FOR i = 0 TO n - 1
    ps = ps + (v1[i] * v2[i])   // multiply matching elements and add to ps
  END FOR
END PROCEDURE
```

---

### Part 2 — Algorithm Calling the Procedure

> This is the **main algorithm**. It reads `n` pairs of vectors, calls the `dot_product` procedure, and checks if each pair is orthogonal.

```
BEGIN
  DECLARE n        : INTEGER   // number of vector pairs
  DECLARE size     : INTEGER   // size of each vector
  DECLARE k, i     : INTEGER   // loop counters
  DECLARE ps       : REAL      // stores the dot product result
  DECLARE v1[100]  : REAL      // first vector
  DECLARE v2[100]  : REAL      // second vector

  READ n                             // read how many pairs of vectors to check
  FOR k = 1 TO n                    // outer loop — goes through each pair
    READ size                        // read the size of the current vectors
    FOR i = 0 TO size - 1           // inner loop — reads each element of the vectors
      READ v1[i]                     // read element i of first vector
      READ v2[i]                     // read element i of second vector
    END FOR

    CALL dot_product(v1, v2, size, ps)  // call procedure, ps is filled by reference

    // check if dot product is zero — if yes vectors are orthogonal
    IF ps == 0 THEN
      PRINT "Vectors are orthogonal"
    ELSE
      PRINT "Vectors are NOT orthogonal"
    END IF
  END FOR
END
```

---

### Part 3 — Modified Algorithm Using a Function

> Same logic as Part 2 but `dot_product` is now a **function** — it returns the value directly instead of using an `OUT` parameter.

```
FUNCTION dot_product(v1[] : REAL, v2[] : REAL, n : INTEGER) : REAL
  DECLARE i      : INTEGER   // loop counter
  DECLARE result : REAL      // stores the running total

  result = 0                           // initialize result to 0
  FOR i = 0 TO n - 1
    result = result + (v1[i] * v2[i])  // multiply matching elements and add to result
  END FOR
  RETURN result                        // return the final dot product value
END FUNCTION

BEGIN
  DECLARE n        : INTEGER   // number of vector pairs
  DECLARE size     : INTEGER   // size of each vector
  DECLARE k, i     : INTEGER   // loop counters
  DECLARE ps       : REAL      // stores the returned dot product result
  DECLARE v1[100]  : REAL      // first vector
  DECLARE v2[100]  : REAL      // second vector

  READ n                             // read how many pairs of vectors to check
  FOR k = 1 TO n                    // outer loop — goes through each pair
    READ size                        // read the size of the current vectors
    FOR i = 0 TO size - 1           // inner loop — reads each element of the vectors
      READ v1[i]                     // read element i of first vector
      READ v2[i]                     // read element i of second vector
    END FOR

    ps = dot_product(v1, v2, size)  // call function and store returned value in ps

    // check if dot product is zero — if yes vectors are orthogonal
    IF ps == 0 THEN
      PRINT "Vectors are orthogonal"
    ELSE
      PRINT "Vectors are NOT orthogonal"
    END IF
  END FOR
END
```

---

