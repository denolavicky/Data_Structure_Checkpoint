# Distinct Sum Algorithm

A simple pseudocode implementation designed to find the **sum of all distinct elements** from two sets. This algorithm identifies the symmetric difference between two arrays—meaning it sums the numbers that appear in one set but not the other.

## 📝 Problem Description

Given two sets of integers, find the sum of all elements which are present in either of the sets, but not in both.

**Example:**
- **Set 1:** `[3, 1, 7, 9]`
- **Set 2:** `[2, 4, 1, 9, 3]`
- **Distinct Elements:** `7, 2, 4`
- **Result:** `13` (7 + 2 + 4)

## 🚀 How it Works

The algorithm uses a nested loop approach to compare elements across two passes:

1.  **Pass 1:** Iterates through `set1`. For each element, it checks if it exists in `set2`. If it is **not found**, it's added to the `sum`.
2.  **Pass 2:** Iterates through `set2`. For each element, it checks if it exists in `set1`. If it is **not found**, it's added to the `sum`.

## 💻 Logic Breakdown (Pseudocode)

```pascal
ALGORITHM DistintSum
VAR
    set1, set2 : ARRAY_OF INTEGER
    sum, i, j : INTEGER
    found : BOOLEAN
BEGIN
    // Comparison Logic
    FOR i FROM 0 TO set1.length - 1 DO
        found := FALSE
        FOR j FROM 0 TO set2.length - 1 DO
            IF (set1[i] == set2[j]) THEN
                found := TRUE
                BREAK
            END_IF
        END_FOR
        IF (found == FALSE) THEN
            sum := sum + set1[i]
        END_IF
    END_FOR
    // ... Repeat for set2 ...
END
