Here is the full solution in English.

## Q1: List vs. Dictionary

This question asks for the difference between a Python **List** and a **Dictionary**, with examples.

- **List:**

  - It is an **ordered** collection of items.
  - Elements are accessed by their **index** (an integer position, starting from 0).
  - It uses square brackets `[]`.
  - **Example:** `my_list = ["apple", 10, True]` (You access "apple" using `my_list[0]`).

- **Dictionary:**

  - It is a collection of **key-value** pairs. It is **unordered** (before Python 3.7) or **insertion-ordered** (Python 3.7+).
  - Values are accessed by their unique **key**.
  - It uses curly braces `{}`.
  - **Example:** `my_dict = {"name": "John", "age": 30}` (You access the value 30 using `my_dict["age"]`).

**Summary:** The main difference is **how they are organized and accessed**. A List uses ordered, integer indices, while a Dictionary uses unique keys to access values.

---

## Q2: Python Code Solution

This section provides the complete code to perform all 4 requested steps.

### Code

```python
import pandas as pd
import numpy as np

# Provided code
df = pd.DataFrame({'A': [1, 2, np.nan, 4]})
print("--- Initial DataFrame ---")
print(df)

# 1. Replace missing values in column A with the mean
# The mean of A is (1 + 2 + 4) / 3 = 2.333...
mean_A = df['A'].mean()
df['A'] = df['A'].fillna(mean_A)

# 2. Create a new column B = A²
df['B'] = df['A'] ** 2

# 3. Create another column C: 'High' if A > mean(A), otherwise 'Low' (using loc)
# First, assign 'Low' as the default value
df['C'] = 'Low'
# Then, update rows where the condition A > mean_A is true
# Note: The row where A == mean_A (2.333...) will correctly remain 'Low'.
df.loc[df['A'] > mean_A, 'C'] = 'High'

# 4. Print the DataFrame
print("\n--- Final DataFrame ---")
print(df)
```

### Output

```
--- Initial DataFrame ---
     A
0  1.0
1  2.0
2  NaN
3  4.0

--- Final DataFrame ---
          A          B     C
0  1.000000   1.000000   Low
1  2.000000   4.000000   Low
2  2.333333   5.444444   Low
3  4.000000  16.000000  High
```
