# Tham khảo nhanh C# – Operators

## 5. Các toán tử trong C#

### 5.1 Ghi chú chung

- Trừ toán tử mới (`??`, `?.`, `??=`, `^`, `..`, `>>>`, v.v.), đa số toán tử có từ **C# 1.0**.  
- Một số toán tử là keyword (`new`, `typeof`, `await`, `checked`, …) – chi tiết xem thêm phần keywords tương ứng.

---

### 5.2 Nhóm toán tử số học & tăng/giảm

#### 5.2.1 `+`, `-`, `*`, `/`, `%`

- **Loại:** Số học (arithmetic) – C# 1.0  
- `+`: cộng, nối chuỗi, cộng delegate.  
- `-`: trừ, đổi dấu.  
- `*`: nhân.  
- `/`: chia (số nguyên: chia lấy phần nguyên).  
- `%`: modulo (phần dư).

**Ví dụ:**

```csharp
int a = 5, b = 3;
int sum = a + b;      // 8
int diff = a - b;     // 2
int prod = a * b;     // 15
int div = a / b;      // 1
int mod = a % b;      // 2

string s = "Hello " + "world"; // nối chuỗi
```

---

#### 5.2.2 `++`, `--`

- **Loại:** Unary – C# 1.0  
- `++x`: tăng rồi trả giá trị mới.  
- `x++`: trả giá trị cũ rồi tăng.

**Ví dụ:**

```csharp
int x = 1;
int a = ++x; // x = 2, a = 2
int b = x++; // x = 3, b = 2
```

---

### 5.3 Nhóm so sánh & equality

#### 5.3.1 `<`, `>`, `<=`, `>=`

- **Loại:** Quan hệ – C# 1.0  
- So sánh thứ tự cho số, `DateTime`, các type overload toán tử này.

```csharp
if (age >= 18 && age < 65) { ... }
```

---

#### 5.3.2 `==`, `!=`

- **Loại:** Equality – C# 1.0  
- So sánh bằng / khác. Với `string`, so sánh nội dung; với reference type khác, mặc định so sánh tham chiếu (trừ khi override).

```csharp
string a = "abc";
string b = "ab" + "c";

bool eq = (a == b);  // true
bool ne = (a != b);  // false
```

---

### 5.4 Toán tử logic & bit

#### 5.4.1 `!`, `&&`, `||`

- **Loại:** Logic boolean – C# 1.0 (short-circuit cho `&&`, `||`).

```csharp
bool IsAdult(Person p)
    => p != null && p.Age >= 18;
```

---

#### 5.4.2 `&`, `|`, `^`, `~`

- **Loại:** Bitwise / non-short-circuit – C# 1.0

```csharp
int flags = 0b_0101;
bool hasBit0 = (flags & 0b_0001) != 0;
flags |= 0b_0010;    // bật bit 1
flags &= ~0b_0100;   // tắt bit 2
```

---

#### 5.4.3 `<<`, `>>`, `>>>`

- **Loại:** Shift – `<<`, `>>`: C# 1.0; `>>>`: C# 11.0  
- `>>` là dịch phải **có dấu**; `>>>` là dịch phải **không dấu** (zero-fill).

```csharp
int a = 1 << 3;   // 8
int b = -1 >> 1;  // -1 (dịch phải có dấu)
// C# 11:
int c = -1 >>> 1; // dịch phải không dấu
```

---

### 5.5 Toán tử gán & gán kết hợp

#### 5.5.1 `=`

- **Loại:** Gán – C# 1.0  

```csharp
int x;
int y = (x = 10); // x = 10, y = 10
```

---

#### 5.5.2 `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`, `>>>=`

- **Loại:** Compound assignment – C# 1.0, `>>>=` từ C# 11.0.  

```csharp
int x = 5;
x += 3;   // 8
x <<= 1;  // 16
```

---

### 5.6 Toán tử điều kiện & null

#### 5.6.1 `?:` – conditional (3 ngôi)

```csharp
string grade = score >= 50 ? "Pass" : "Fail";
```

---

#### 5.6.2 `??` – null-coalescing (C# 2.0)

```csharp
string? name = null;
string display = name ?? "Unknown";
```

---

#### 5.6.3 `??=` – null-coalescing assignment (C# 8.0)

```csharp
List<int>? numbers = null;
(numbers ??= new List<int>()).Add(5);
```

---

#### 5.6.4 `?.`, `?[]` – null-conditional (C# 6.0)

```csharp
int? len = user?.Address?.Street?.Length;
var item = list?[0];
```

---

#### 5.6.5 `!` (postfix) – null-forgiving (C# 8.0)

```csharp
#nullable enable

string? FindName() => null;
string name = FindName()!; // “tôi chắc là không null”
```

---

### 5.7 Truy cập, gọi hàm, index & range

#### 5.7.1 `.` – truy cập thành viên

```csharp
user.Address.City
Math.PI
```

---

#### 5.7.2 `()`, `[]` – gọi hàm & indexer

```csharp
int Add(int a, int b) => a + b;
int sum = Add(1, 2);

int first = list[0];
```

---

#### 5.7.3 `^` – index from end (C# 8.0)

```csharp
int[] arr = { 1, 2, 3, 4, 5 };
int last = arr[^1];     // 5
int secondLast = arr[^2]; // 4
```

---

#### 5.7.4 `..` – range (C# 8.0)

```csharp
int[] arr = { 0, 1, 2, 3, 4, 5 };
int[] middle = arr[1..4]; // {1,2,3}
int[] last3 = arr[^3..];  // {3,4,5}
```

---

#### 5.7.5 `::` – alias qualifier

```csharp
using Project = MyCompany.Project;
Project::Service svc;

global::System.String s;
```

---

### 5.8 Toán tử kiểu & cast

#### 5.8.1 `(T)x` – cast

```csharp
object o = 42;
int value = (int)o;
```

---

#### 5.8.2 `is`, `as`

```csharp
if (obj is string s && s.Length > 0)
    Console.WriteLine(s);

Stream? stream = obj as Stream;
if (stream != null) { ... }
```

---

### 5.9 Lambda & expression-bodied members – `=>`

- **C#:** 3.0 (lambda), 6.0 (expression-bodied members).

```csharp
Func<int, int> square = x => x * x;
int result = square(5);

public override string ToString()
    => $"{Name} ({Age})";
```

---

### 5.10 Toán tử pointer & unsafe

> Cần `unsafe` + bật “Allow unsafe code”.

- `&x` – address-of  
- `*p` – dereference  
- `p->Member` – truy cập member qua pointer  
- `p[i]` – index qua pointer  

```csharp
unsafe
{
    int value = 10;
    int* p = &value;
    *p = 20;
}
```

---

### 5.11 Bảng tóm tắt nhóm toán tử

| Nhóm toán tử                    | Ví dụ chính                                           | C# từ      |
|---------------------------------|--------------------------------------------------------|-----------|
| Số học & tăng/giảm             | `+`, `-`, `*`, `/`, `%`, `++`, `--`                   | 1.0       |
| So sánh & equality             | `<`, `>`, `<=`, `>=`, `==`, `!=`                      | 1.0       |
| Logic điều kiện                | `!`, `&&`, `||`                                       | 1.0       |
| Bitwise & shift                | `&`, `|`, `^`, `~`, `<<`, `>>`, `>>>`                 | 1.0 / 11.0|
| Gán & gán kết hợp              | `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`, `>>>=` | 1.0 / 11.0 |
| Điều kiện & null               | `?:`, `??`, `??=`, `?.`, `?[]`, `!` (null-forgiving)  | 1.0 / 2.0 / 6.0 / 8.0 |
| Truy cập, gọi, index & range   | `.`, `()`, `[]`, `^`, `..`, `::`                      | 1.0 / 8.0 |
| Kiểu & cast                    | `(T)x`, `is`, `as`, `typeof`, `sizeof`, `checked`    | 1.0+      |
| Lambda & expression-bodied     | `=>`                                                  | 3.0 / 6.0 |
| Unsafe & pointer               | `&x`, `*p`, `p->M`, `p[i]`, `stackalloc`             | 1.0+      |
