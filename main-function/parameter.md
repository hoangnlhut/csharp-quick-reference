# Tham số của hàm Main

Hàm Main có thể nhận vào tham số dưới dạng một `string[]`. Tham số này *luôn luôn* khác `null`, 
bạn có thể dùng args.Length != 0 một cách an toàn để kiểm tra xem có tham số nào được truyền khi chương trình
chạy hay không.

Trong trường hợp không dùng tham số `string[] args`, bạn vẫn có thể lấy giá trị của chúng thông qua
Environment.CommandLine hoặc Environment.GetCommandLineArgs.
