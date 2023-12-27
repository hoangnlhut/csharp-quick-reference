# Kiểu giá trị (Value Type)

Các biến value type trực tiếp chứa instance bên trong vùng nhớ của nó, khi khai báo một biến 
kiểu `value type`, CLR sẽ cấp phát bộ nhớ cho biến bất kể đang trong ngữ cảnh nào. Điều này 
khác với các biến kiểu `reference type`, trong đó vùng nhớ của biến chỉ chứa tham chiếu đến 
instance. Mặc nhiên khi thực hiện phép gán, truyền tham số hay trả về giá trị từ một phương thức, 
các giá trị của biến kiểu `value type` sẽ được sao chép (copy).

Các kiểu value type thừa kế từ System.ValueType, và luôn được khai báo là `sealed`, tức nó không
cho phép bạn tạo các lớp khác thừa kế từ nó. Tuy nhiên một `struct` vẫn có thể implement một
hoặc nhiều `interface`, và khi đó bạn vẫn có thể ép kiểu `struct` đó về một trong những 
`interface` mà nó implement. Việc ép kiểu này sẽ tạo ra một thao tác `boxing`, trong đó đối tượng
kiểu value type đó sẽ được đóng gói bên trong một kiểu reference type trên heap.

Xem thêm về Boxing và Unboxing.

Khi cần tạo một kiểu dữ liệu value type tùy biến mới, bạn có thể sử dụng từ khóa 
[`struct`](../keywords/struct.md).

Một kiểu dữ liệu value type nữa là `enum`, các `enum` giúp các tập giá trị trở nên dễ đọc hơn. 
Các `enum` thừa kế từ `System.Enum`, vốn cũng thừa kế từ `System.Enum`.
