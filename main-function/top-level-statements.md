# Top-level statements

Từ C#10, chúng ta có thể viết một chương trình mà không dùng hàm Main, tính năng này gọi là top-level statements.
Bạn có thể viết một chương trình đơn giản như sau:

```csharp
Console.WriteLine("Hello World!");
```

Tính năng này cho phép chúng ta viết các đoạn code ngắn, đặc biệt phù hợp với các cloud functions như Azure Functions,
GitHub Actions và AWS Lambda Functions.

Một số điểm cần lưu ý khi sử dụng top-level statements:

- Mỗi chương trình chỉ được phép có một top-level statement file.
- Top-level statement file luôn là điểm thực thi đầu tiên của chương trình, bạn vẫn có thể khai báo hàm Main nhưng 
chương trình vẫn bắt đầu chạy từ file top-level statement. (Trình biên dịch sẽ cảnh cáo trong trường hợp này).
- Bạn vẫn có thể khai báo lớp hoặc namespace, nhưng chúng bắt buộc phải nằm phía sau các câu lệnh top-level statement.

```csharp
Console.WriteLine(MyHelloWorld.GetHelloWorld());

public class MyHelloWorld
{
    public static string GetHelloWorld()
    {
        return "Hello World!";
    }

}
```

- Trình biên dịch sẽ tạo ra một hàm tương tự như sau để chứa các câu lệnh top-level statement của bạn:

```csharp
private static void <Main>$(string[] args)
{
    Console.WriteLine("Hello, World!");
}
```

- Bạn có thể sử dụng biến args để truy cập đến các tham số được truyền cho chương trình.
- Bạn có thể sử dụng `await` trong đoạn code top-level statement.
- Bạn cũng có thể dùng `return` để trả về giá trị cho chương trình gọi, tương tự như khi bạn viết hàm Main
với kiểu trả về là int.
- Bạn có thể sử dụng `using`, nhưng chúng phải được khai báo ở đầu file. 
