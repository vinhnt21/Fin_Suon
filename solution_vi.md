## Q1: List vs. Dictionary

Câu hỏi này yêu cầu giải thích sự khác biệt giữa **List** (danh sách) và **Dictionary** (từ điển) trong Python và cho ví dụ.

- **List (Danh sách):**

  - Là một tập hợp **có thứ tự** (ordered) các mục.
  - Truy cập các phần tử bằng **chỉ số** (index) - vị trí số nguyên của chúng (bắt đầu từ 0).
  - Sử dụng dấu ngoặc vuông `[]`.
  - **Ví dụ:** `my_list = ["apple", 10, True]` (Bạn có thể truy cập "apple" bằng `my_list[0]`).

- **Dictionary (Từ điển):**

  - Là một tập hợp **không có thứ tự** (trước Python 3.7) hoặc **thứ tự theo chèn** (từ Python 3.7) gồm các cặp **key-value** (khóa-giá trị).
  - Truy cập các giá trị (values) bằng **khóa** (key) duy nhất của chúng.
  - Sử dụng dấu ngoặc nhọn `{}`.
  - **Ví dụ:** `my_dict = {"name": "John", "age": 30}` (Bạn có thể truy cập 30 bằng `my_dict["age"]`).

**Tóm tắt:** Sự khác biệt chính là **cách chúng được tổ chức và truy cập**. List sử dụng các chỉ số (index) số nguyên có thứ tự, trong khi Dictionary sử dụng các khóa (key) duy nhất để truy cập các giá trị (value) của nó.

---

## Q2: Python Code Solution

Phần này cung cấp một đoạn mã đầy đủ thực hiện tất cả 4 bước được yêu cầu.

### Code

```python
import pandas as pd
import numpy as np

# Mã được cung cấp
df = pd.DataFrame({'A': [1, 2, np.nan, 4]})
print("--- Initial DataFrame ---")
print(df)

# 1. Thay thế giá trị bị thiếu (np.nan) trong cột A bằng giá trị trung bình
# Giá trị trung bình của A là (1 + 2 + 4) / 3 = 2.333...
mean_A = df['A'].mean()
df['A'] = df['A'].fillna(mean_A)

# 2. Tạo cột mới B = A²
df['B'] = df['A'] ** 2

# 3. Tạo cột C: 'High' nếu A > mean(A), ngược lại 'Low' (sử dụng loc)
# Đầu tiên, gán giá trị mặc định 'Low' cho tất cả
df['C'] = 'Low'
# Sau đó, cập nhật những hàng thỏa mãn điều kiện A > mean_A thành 'High'
df.loc[df['A'] > mean_A, 'C'] = 'High'
# Lưu ý: Hàng có A = mean_A (2.333...) sẽ không > mean_A, nên vẫn là 'Low'.

# 4. In DataFrame cuối cùng
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
