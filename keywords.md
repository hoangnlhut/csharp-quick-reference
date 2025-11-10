# Tham khảo nhanh C# – Reserved keywords

## Reserved keywords (77 từ, A–Z)

### 1. `abstract`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:**  
  - Đánh dấu class/member trừu tượng, không có triển khai đầy đủ.  
  - Class `abstract` không thể `new`.  
  - Member `abstract` bắt buộc phải được `override` trong lớp con.

**Ví dụ:**

```csharp
public abstract class Shape
{
    public abstract double Area();

    public virtual void Print()
        => Console.WriteLine($"Area = {Area()}");
}

public sealed class Circle : Shape
{
    public double Radius { get; }

    public Circle(double radius) => Radius = radius;

    public override double Area() => Math.PI * Radius * Radius;
}
```

**Ghi chú:**  
Thường dùng khi muốn định nghĩa “hợp đồng + một phần behavior chung” cho một nhóm class.

---

### 2. `as`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Cast an toàn giữa reference type / nullable value type. Thất bại ⇒ `null`, không ném exception.

**Ví dụ:**

```csharp
object obj = "hello";

string? s = obj as string;        // "hello"
FileStream? fs = obj as FileStream; // null

if (s != null)
{
    Console.WriteLine(s.ToUpper());
}
```

**Ghi chú:**  
Luôn nhớ kiểm tra `null` sau khi dùng `as`. Nếu muốn lỗi rõ ràng hơn, dùng cast thường `(T)obj`.

---

### 3. `base`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Dùng trong class dẫn xuất để gọi ctor hoặc member của base class (đặc biệt trong `override`).

**Ví dụ:**

```csharp
public class Animal
{
    public string Name { get; }

    public Animal(string name) => Name = name;

    public virtual void Speak()
        => Console.WriteLine($"{Name} makes a sound");
}

public class Dog : Animal
{
    public Dog(string name) : base(name) { }

    public override void Speak()
    {
        base.Speak(); // gọi behavior chung
        Console.WriteLine($"{Name} barks");
    }
}
```

**Ghi chú:**  
Không dùng được trong `struct`. Nếu base không có ctor mặc định, lớp con phải gọi `base(...)`.

---

### 4. `bool`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Kiểu Boolean với hai giá trị `true` / `false`. Không cho dùng int thay bool như C/C++.

**Ví dụ:**

```csharp
bool isActive = true;

if (isActive)
{
    Console.WriteLine("Enabled");
}
else
{
    Console.WriteLine("Disabled");
}
```

---

5. `break`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Thoát khỏi vòng lặp (`for`, `foreach`, `while`, `do`) hoặc `switch` ngay lập tức.

**Ví dụ:**

```csharp
for (int i = 0; i < 100; i++)
{
    if (i == 10)
        break;
}

switch (statusCode)
{
    case 200:
        Console.WriteLine("OK");
        break;
    default:
        Console.WriteLine("Other");
        break;
}
```

**Ghi chú:**  
Quá nhiều `break`/`continue` trong cùng một vòng lặp có thể làm flow khó đọc.

---

### 6. `byte`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên không dấu 8-bit (`0..255`), thường dùng cho buffer, stream, dữ liệu nhị phân.

**Ví dụ:**

```csharp
byte b = 255;
byte[] buffer = new byte[1024];
```

**Ghi chú:**  
Phép toán trên `byte` trả về `int`, cần cast ngược nếu muốn gán lại vào `byte`.

---

### 7. `case`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Định nghĩa nhánh trong `switch` (statement).

**Ví dụ:**

```csharp
switch (status)
{
    case 200:
        Console.WriteLine("OK");
        break;
    case 404:
        Console.WriteLine("Not Found");
        break;
    default:
        Console.WriteLine("Unknown");
        break;
}
```

**Ghi chú:**  
Trong `switch` cũ, mỗi `case` phải kết thúc bằng `break`/`return`/`goto`… Trên `switch expression` (C# 8+) không dùng `case` kiểu này nữa.

---

### 8. `catch`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Bắt exception được ném từ khối `try`.

**Ví dụ:**

```csharp
try
{
    File.ReadAllText("data.txt");
}
catch (FileNotFoundException ex)
{
    Console.WriteLine("File không tồn tại");
}
catch (IOException ex)
{
    Console.WriteLine("Lỗi IO khác");
}
catch (Exception ex)
{
    Console.WriteLine("Lỗi không xác định");
}
```

**Ghi chú:**  
Tránh `catch (Exception) { }` bỏ trống – rất khó debug. Nên log hoặc wrap thành exception có ý nghĩa cụ thể.

---

### 9. `char`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Ký tự Unicode 16-bit (`System.Char`). Một số ký tự (emoji, ký hiệu phức tạp) cần 2 `char` (surrogate pair).

**Ví dụ:**

```csharp
char c = 'A';
bool isLetter = char.IsLetter(c); // true
```

**Ghi chú:**  
Đừng giả định “1 ký tự người dùng = 1 `char`”; với Unicode phức tạp nên dùng API trên `string` hoặc `System.Text.Rune`.

---

### 10. `checked`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Bật kiểm tra overflow cho toán tử số học/ép kiểu integral. Overflow ⇒ ném `OverflowException`.

**Ví dụ:**

```csharp
int x = int.MaxValue;

checked
{
    int y = x + 1; // OverflowException
}
```

**Ghi chú:**  
Dùng ở chỗ cần đảm bảo không overflow (tài chính, số quan trọng). Có thể bật mặc định trong project và dùng `unchecked` cho các chỗ đặc biệt.

---

### 11. `class`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Khai báo **reference type** (class).

**Ví dụ:**

```csharp
public class Person
{
    public string Name { get; set; } = "";
    public int Age { get; set; }

    public void SayHello()
        => Console.WriteLine($"Hi, I'm {Name} ({Age})");
}
```

**Ghi chú:**  
Class là reference type → được cấp phát trên heap, truyền qua reference. Với type nhỏ, immutable, nhạy hiệu năng, cân nhắc `struct` hoặc `record struct`.

---

### 12. `const`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Khai báo hằng compile-time. Giá trị được inline vào IL của caller.

**Ví dụ:**

```csharp
public const double Pi = 3.14159265358979;
private const string AppName = "MyApp";
```

**Ghi chú:**  
Thay đổi giá trị `public const` trong library không tự update cho code client đã build; cần rebuild client. Với giá trị có thể thay đổi, dùng `static readonly`.

---

### 13. `continue`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Bỏ phần còn lại của vòng lặp hiện tại, nhảy tới lần lặp tiếp theo.

**Ví dụ:**

```csharp
foreach (var item in items)
{
    if (item == null) continue;
    Process(item);
}
```

---

### 14. `decimal`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số thập phân 128-bit, độ chính xác cao, rất phù hợp tài chính / tiền tệ.

**Ví dụ:**

```csharp
decimal price = 19.99m;
decimal qty   = 3;
decimal total = price * qty; // 59.97m
```

**Ghi chú:**  
Chậm hơn `double`; không lý tưởng cho tính toán khoa học nặng.

---

### 15. `default`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:**  
  - Trong `switch`: nhánh mặc định.  
  - Trong expression: `default(T)` hoặc `default` (C# 7.1+) ⇒ giá trị mặc định của kiểu (`0`, `false`, `null`, struct rỗng…).

**Ví dụ:**

```csharp
int x = default;      // 0
string? s = default;  // null

T Create<T>() => default!;
```

---

### 16. `delegate`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Khai báo kiểu đại diện cho method (function pointer an toàn). Dùng cho callback, event handler, v.v.

**Ví dụ:**

```csharp
public delegate void LogHandler(string message);

public class Worker
{
    public LogHandler? Logger { get; set; }

    public void DoWork()
    {
        Logger?.Invoke("Working...");
    }
}
```

**Ghi chú:**  
Trong code hiện đại, thường dùng `Action<>`, `Func<>` thay vì tự khai báo delegate, trừ khi cần type public có tên rõ ràng.

---

### 17. `do`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Bắt đầu vòng lặp `do { ... } while (cond)` – thân vòng lặp **chạy ít nhất 1 lần**.

**Ví dụ:**

```csharp
int i = 0;

do
{
    Console.WriteLine(i);
    i++;
} while (i < 3);
```

---

### 18. `double`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số thực 64-bit theo chuẩn IEEE 754; dùng nhiều cho tính toán khoa học, đồ họa, đo đạc.

**Ví dụ:**

```csharp
double x = 0.1 + 0.2;
Console.WriteLine(x); // 0.30000000000000004
```

**Ghi chú:**  
Luôn tồn tại sai số floating-point; khi so sánh nên dùng epsilon, không so sánh trực tiếp bằng `==` cho số thực.

---

### 19. `else`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Nhánh “ngược lại” của `if`.

**Ví dụ:**

```csharp
if (score >= 90)
    grade = "A";
else if (score >= 80)
    grade = "B";
else
    grade = "C";
```

---

### 20. `enum`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Định nghĩa kiểu liệt kê (enum) với underlying integral type (mặc định `int`).

**Ví dụ:**

```csharp
public enum OrderStatus
{
    Pending = 0,
    Processing = 1,
    Completed = 2,
    Cancelled = 3
}
```

**Ghi chú:**  
Enum vẫn là số bên dưới ⇒ cast được giá trị không hợp lệ; nếu nhận từ bên ngoài cần validate.

---

### 21. `event`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Khai báo event .NET, cho phép subscribe/unsubscribe handler.

**Ví dụ:**

```csharp
public class Button
{
    public event EventHandler? Click;

    protected virtual void OnClick()
        => Click?.Invoke(this, EventArgs.Empty);

    public void SimulateClick() => OnClick();
}
```

**Ghi chú:**  
Cẩn thận memory leak nếu subscriber không hủy đăng ký ở các scenario sống lâu (winforms, WPF, v.v.).

---

### 22. `explicit`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Toán tử chuyển kiểu tường minh, bắt buộc dùng cast.

**Ví dụ:**

```csharp
public readonly struct Meter
{
    public double Value { get; }
    public Meter(double value) => Value = value;

    public static explicit operator Meter(double v) => new(v);
    public static explicit operator double(Meter m) => m.Value;
}

Meter m = (Meter)5.0;
double d = (double)m;
```

---

### 23. `extern`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Chỉ ra method được implement bên ngoài (thường là native DLL, dùng với `DllImport`).

**Ví dụ:**

```csharp
using System.Runtime.InteropServices;

class NativeMethods
{
    [DllImport("kernel32.dll")]
    public static extern void Sleep(uint milliseconds);
}
```

---

### 24. `false`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Hằng Boolean `false`.

**Ví dụ:**

```csharp
bool ok = false;
if (!ok)
{
    Console.WriteLine("Not OK");
}
```

---

### 25. `finally`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Khối cleanup luôn chạy sau `try`/`catch` (dù có exception hay không).

**Ví dụ:**

```csharp
FileStream? stream = null;
try
{
    stream = File.OpenRead("data.txt");
    // xử lý
}
finally
{
    stream?.Dispose();
}
```

**Ghi chú:**  
Cẩn thận không ném exception mới từ `finally` (dễ che mất exception gốc). Hiện đại hơn là dùng `using` / `using var`.

---

### 26. `fixed`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Trong `unsafe`, pin object để lấy địa chỉ cố định (pointer) cho interop/native.

**Ví dụ:**

```csharp
unsafe
{
    int[] arr = { 1, 2, 3 };
    fixed (int* p = &arr[0])
    {
        // p trỏ tới arr[0], GC không được di chuyển arr trong khối fixed
        Console.WriteLine(*p);
    }
}
```

---

### 27. `float`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số thực 32-bit (nhẹ hơn nhưng kém chính xác hơn `double`).

**Ví dụ:**

```csharp
float f = 1.23f;
```

---

### 28. `for`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Vòng lặp có phần khởi tạo, điều kiện, bước tăng/giảm rõ ràng.

**Ví dụ:**

```csharp
for (int i = 0; i < items.Length; i++)
{
    Console.WriteLine(items[i]);
}
```

---

### 29. `foreach`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Vòng lặp tiện dụng trên mọi `IEnumerable` / `IEnumerable<T>`.

**Ví dụ:**

```csharp
foreach (var item in items)
{
    Console.WriteLine(item);
}
```

---

### 30. `goto`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Nhảy tới label hoặc `case`/`default` trong `switch`.

**Ví dụ:**

```csharp
switch (option)
{
    case 0:
        Console.WriteLine("Zero");
        goto case 1;
    case 1:
        Console.WriteLine("One");
        break;
}
```

**Ghi chú:**  
Thường được xem là “code smell”, trừ vài pattern rất hiếm (ví dụ thoát lồng nhiều vòng).

---

### 31. `if`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Câu lệnh rẽ nhánh cơ bản.

**Ví dụ:**

```csharp
if (user is null)
    throw new ArgumentNullException(nameof(user));
```

---

### 32. `implicit`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Toán tử chuyển kiểu ngầm định (không cần cast).

**Ví dụ:**

```csharp
public readonly struct Meter
{
    public double Value { get; }
    public Meter(double value) => Value = value;

    public static implicit operator Meter(double v) => new(v);
}

Meter m = 5.0; // implicit
```

---

### 33. `in`

- **Loại:** reserved · **C#:** 1.0 (thêm ý nghĩa mới ở C# 7.2)  
- **Mục đích:**  
  - Trong tham số: `in` ⇒ readonly by-ref.  
  - Trong `foreach`: một phần cú pháp (`foreach (var x in xs)`).

**Ví dụ (C# 7.2+):**

```csharp
public static double Distance(in Point a, in Point b)
{
    // a, b truyền by-ref nhưng không gán lại được
    // tránh copy struct lớn
}
```

---

### 34. `int`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 32-bit có dấu, kiểu integer phổ biến nhất.

**Ví dụ:**

```csharp
int count = 42;
```

---

### 35. `interface`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Định nghĩa hợp đồng (method, property, event…) mà class/struct phải thực hiện.

**Ví dụ:**

```csharp
public interface ILogger
{
    void Log(string message);
}
```

---

### 36. `internal`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Access modifier – chỉ thấy được trong cùng assembly.

**Ví dụ:**

```csharp
internal class InternalHelper { }
```

---

### 37. `is`

- **Loại:** reserved · **C#:** 1.0 (pattern matching từ C# 7.0)  
- **Mục đích:**  
  - Kiểm tra kiểu (`obj is T`).  
  - Từ C# 7: pattern matching (`is T v`, `is null`, `is > 0`, v.v.).

**Ví dụ:**

```csharp
if (obj is string s && s.Length > 0)
{
    Console.WriteLine(s);
}
```

---

### 38. `lock`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Đồng bộ truy cập giữa các thread (`Monitor.Enter/Exit`).

**Ví dụ:**

```csharp
private readonly object _sync = new();
private int _counter;

public void Increment()
{
    lock (_sync)
    {
        _counter++;
    }
}
```

---

### 39. `long`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 64-bit có dấu (`System.Int64`).

**Ví dụ:**

```csharp
long big = 1_000_000_000_000L;
```

---

### 40. `namespace`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Tổ chức không gian tên cho type.

**Ví dụ:**

```csharp
namespace MyApp.Core
{
    public class Service { }
}
```

---

### 41. `new`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:**  
  - Tạo instance: `new Type(...)`.  
  - Hide member base: `new void Foo()`.  
  - Constraint: `where T : new()`.

**Ví dụ:**

```csharp
var p = new Person("Alice");

public class Base
{
    public void Print() => Console.WriteLine("Base");
}

public class Derived : Base
{
    public new void Print() => Console.WriteLine("Derived");
}
```

---

### 42. `null`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Giá trị “không tham chiếu tới object nào” cho reference type & nullable value type.

**Ví dụ:**

```csharp
string? name = null;
if (name is null)
{
    // ...
}
```

---

### 43. `object`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Kiểu gốc của mọi reference type (alias cho `System.Object`).

**Ví dụ:**

```csharp
object o = 42;   // boxing
int x = (int)o;  // unboxing
```

---

### 44. `operator`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Định nghĩa toán tử overload (`+`, `-`, `==`, conversion…) cho type custom.

**Ví dụ:**

```csharp
public readonly struct Money
{
    public decimal Value { get; }

    public Money(decimal value) => Value = value;

    public static Money operator +(Money a, Money b)
        => new(a.Value + b.Value);
}
```

---

### 45. `out`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Tham số output; method phải gán trước khi return.

**Ví dụ:**

```csharp
if (int.TryParse("123", out int value))
{
    Console.WriteLine(value);
}
```

---

### 46. `params`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Cho phép truyền số lượng đối số biến đổi (varargs).

**Ví dụ:**

```csharp
void Log(params string[] messages)
{
    foreach (var m in messages)
        Console.WriteLine(m);
}

Log("A", "B", "C");
```

---

### 47. `private`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Access modifier – chỉ trong cùng type.

**Ví dụ:**

```csharp
public class User
{
    private string _passwordHash = "";
}
```

---

### 48. `protected`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Access modifier – trong type và lớp dẫn xuất.

```csharp
public class Base
{
    protected void OnChanged() { }
}
```

---

### 49. `public`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Access modifier – public ở khắp nơi nếu nhìn thấy type/assembly.

```csharp
public class ApiClient { }
```

---

### 50. `readonly`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Field chỉ gán trong ctor hoặc tại điểm khai báo.

```csharp
public class Config
{
    public readonly string ConnectionString;

    public Config(string conn) => ConnectionString = conn;
}
```

---

### 51. `ref`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Tham số by-ref (đọc/ghi), C# 7+ có `ref local`, `ref return`.

```csharp
void Swap(ref int a, ref int b)
{
    int t = a; a = b; b = t;
}
```

---

### 52. `return`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Trả giá trị (nếu có) và kết thúc method/local function.

```csharp
int Double(int x) => x * 2;
```

---

### 53. `sbyte`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 8-bit có dấu; không CLS-compliant, hiếm dùng.

```csharp
sbyte x = -5;
```

---

### 54. `sealed`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:**  
  - `sealed class`: cấm kế thừa.  
  - `sealed override`: không cho override tiếp.

```csharp
public sealed class FinalType { }
```

---

### 55. `short`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 16-bit có dấu.

```csharp
short s = 10;
```

---

### 56. `sizeof`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Trả kích thước (byte) của kiểu.

```csharp
int size = sizeof(int); // 4
```

---

### 57. `stackalloc`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Cấp phát mảng trên stack, thường dùng với `Span<T>` hoặc pointer.

```csharp
Span<int> span = stackalloc int[100];
```

---

### 58. `static`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Thành viên/kiểu thuộc về type, không thuộc instance.

```csharp
public static class MathHelper
{
    public static int Square(int x) => x * x;
}
```

---

### 59. `string`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Chuỗi Unicode immutable (alias `System.String`).

```csharp
string s = "Hello";
s += " world"; // tạo string mới
```

---

### 60. `struct`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Khai báo value type tùy biến.

```csharp
public readonly struct Point
{
    public int X { get; }
    public int Y { get; }
    public Point(int x, int y) => (X, Y) = (x, y);
}
```

---

### 61. `switch`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Câu lệnh rẽ nhánh nhiều nhánh; C# 8+ có thêm switch expression.

```csharp
switch (day)
{
    case DayOfWeek.Monday:
        Console.WriteLine("Start");
        break;
    default:
        Console.WriteLine("Other");
        break;
}
```

---

### 62. `this`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Tham chiếu tới instance hiện tại; trong extension method đứng trước tham số đầu tiên.

```csharp
public class Person
{
    public string Name { get; set; } = "";
    public void Introduce()
        => Console.WriteLine($"I'm {this.Name}");
}

public static class StringExtensions
{
    public static bool IsEmpty(this string? value)
        => string.IsNullOrEmpty(value);
}
```

---

### 63. `throw`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Ném exception.

```csharp
if (id <= 0)
    throw new ArgumentOutOfRangeException(nameof(id));
```

---

### 64. `true`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Hằng Boolean `true`.

```csharp
while (true)
{
    if (ShouldStop()) break;
}
```

---

### 65. `try`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Bắt đầu khối có xử lý ngoại lệ (`catch`, `finally`).

```csharp
try
{
    DoWork();
}
catch (Exception ex)
{
    Log(ex);
}
```

---

### 66. `typeof`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Lấy `System.Type` của một kiểu.

```csharp
Type t1 = typeof(string);
Type t2 = typeof(List<int>);
```

---

### 67. `uint`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 32-bit không dấu; không CLS-compliant.

```csharp
uint u = 10u;
```

---

### 68. `ulong`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 64-bit không dấu.

```csharp
ulong u = 10UL;
```

---

### 69. `unchecked`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Tắt kiểm tra overflow.

```csharp
unchecked
{
    int x = int.MaxValue + 1; // wrap, không ném exception
}
```

---

### 70. `unsafe`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Cho phép dùng pointer, `stackalloc`, `fixed` – giống C/C++ style.

```csharp
unsafe void Foo(int* p)
{
    *p = 42;
}
```

---

### 71. `ushort`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Số nguyên 16-bit không dấu.

```csharp
ushort u = 10;
```

---

### 72. `using`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:**  
  - Import namespace (`using System;`).  
  - Quản lý lifetime tài nguyên (`using var` hoặc `using (...) { ... }`).

```csharp
using System;

using var stream = File.OpenRead("data.txt");
// dùng stream...
```

---

### 73. `virtual`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Cho phép member được override trong lớp con.

```csharp
public class Base
{
    public virtual void Do() { }
}
```

---

### 74. `void`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Kiểu trả về “không có gì”.

```csharp
void Log(string message) => Console.WriteLine(message);
```

---

### 75. `volatile`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Field `volatile` đảm bảo read/write luôn đi thẳng bộ nhớ, cải thiện visibility giữa thread.

```csharp
public volatile bool _stopped;
```

---

### 76. `while`

- **Loại:** reserved · **C#:** 1.0  
- **Mục đích:** Vòng lặp kiểm tra điều kiện trước mỗi lần lặp.

```csharp
int i = 0;
while (i < 10)
{
    Console.WriteLine(i++);
}
```

---

## Contextual keywords (tóm tắt)

> Contextual keyword: chỉ là keyword trong **một số ngữ cảnh**; ngoài ra vẫn có thể dùng làm tên biến/class.

| Từ khóa   | Mục đích / ngữ cảnh chính                                  | C#   |
|----------|-------------------------------------------------------------|------|
| `add`    | Accessor `add` cho event                                    | 1.0  |
| `allows` | Constraint `allows ref struct`                              | 13.0 |
| `alias`  | `extern alias`, alias namespace                             | 2.0  |
| `and`    | Pattern combinator AND                                      | 9.0  |
| `ascending` | Thứ tự tăng trong LINQ `orderby`                        | 3.0  |
| `args`   | Tham số dòng lệnh trong top-level statements               | 9.0  |
| `async`  | Đánh dấu method/lambda bất đồng bộ                         | 5.0  |
| `await`  | Chờ `Task` / `ValueTask`                                    | 5.0  |
| `by`     | `group ... by` / `orderby ... by` trong LINQ               | 3.0  |
| `descending` | Thứ tự giảm trong LINQ `orderby`                       | 3.0  |
| `dynamic` | Kiểu dynamic – binding lúc runtime                        | 4.0  |
| `equals` | `join ... on ... equals ...` trong LINQ                    | 3.0  |
| `from`   | Bắt đầu LINQ query                                         | 3.0  |
| `get`    | Accessor getter của property                               | 1.0  |
| `global` | `global::` – namespace root                                | 2.0  |
| `group`  | `group ... by ... into ...` trong LINQ                     | 3.0  |
| `init`   | Init-only setter cho property                              | 9.0  |
| `into`   | Đặt tên group or query continuation trong LINQ             | 3.0  |
| `join`   | Kết hợp hai sequence trong LINQ                            | 3.0  |
| `let`    | Tạo biến tạm trong LINQ query                              | 3.0  |
| `managed`| Calling convention `delegate* managed<...>`                | 9.0  |
| `nameof` | Lấy tên symbol thành string                                | 6.0  |
| `nint`   | Native-sized int                                            | 9.0  |
| `not`    | Pattern combinator NOT                                      | 9.0  |
| `notnull`| Generic constraint “không được null”                        | 8.0  |
| `nuint`  | Native-sized uint                                           | 9.0  |
| `on`     | `join ... on ... equals ...`                                | 3.0  |
| `or`     | Pattern combinator OR                                       | 9.0  |
| `orderby`| Clause sắp xếp trong LINQ                                   | 3.0  |
| `partial`| Chia nhỏ định nghĩa type/member                             | 2.0  |
| `record` | Khai báo record / record struct                             | 9.0  |
| `remove` | Accessor `remove` cho event                                 | 1.0  |
| `required`| Property/field bắt buộc khởi tạo                           | 11.0 |
| `select` | Chọn phần kết quả trong LINQ                                | 3.0  |
| `set`    | Accessor setter của property                                | 1.0  |
| `unmanaged` | Generic constraint “unmanaged struct”                    | 7.3  |
| `value`  | Giá trị được gán vào setter / event accessor                | 1.0  |
| `var`    | Suy luận kiểu local variable                                | 3.0  |
| `when`   | Filter trong `catch` & pattern matching                     | 6.0  |
| `where`  | Generic constraint / filter trong LINQ                      | 2.0  |
| `with`   | Clone object theo kiểu copy-with                            | 9.0  |
| `yield`  | Tạo iterator (`yield return`, `yield break`)                | 2.0  |
