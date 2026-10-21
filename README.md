# Dev-C++ Build & Run

Extension VS Code cho Windows: mở file C/C++, bấm **▶** ở góc phải editor để build bằng GCC/G++ sẵn có trong Dev-C++ và chạy trong **cửa sổ PowerShell riêng**.

**[Tải extension .vsix](https://github.com/Bui-Duc-Phu/devcpp-build-run/releases/latest/download/devcpp-build-run-0.1.0.vsix)** · **[Xem bản phát hành](https://github.com/Bui-Duc-Phu/devcpp-build-run/releases/latest)**

Chỉ cần **VS Code + Dev-C++ có GCC/G++**; không cần Node.js khi sử dụng extension. Mã nguồn MIT được đính kèm bản phát hành trong file `devcpp-build-run-0.1.0-source.zip`.

## Cài đặt

1. Cài VS Code 1.85 trở lên và Dev-C++ có GCC/G++ trên Windows.
2. Trong VS Code nhấn **Ctrl+Shift+X**, chọn dấu **…** ở đầu bảng Extensions → **Install from VSIX…**.
3. Chọn `devcpp-build-run-0.1.0.vsix`. Nếu VS Code yêu cầu, chọn Reload Window.
4. Mở thư mục chứa code và tin cậy thư mục nếu bạn tin nguồn mã đó.
5. Mở file `.c`, `.cpp`, `.cc` hoặc `.cxx`, bấm nút tam giác **Dev-C++: Build & Run** ở góc phải editor. Có thể tìm cùng tên lệnh bằng **Ctrl+Shift+P**.

Bạn cũng có thể cài bằng CLI:

```powershell
code --install-extension "C:\duong-dan\devcpp-build-run-0.1.0.vsix"
```

## Cách chạy

Extension lưu file, tìm compiler Dev-C++, build ra `.devcpp-build\ten-file.cpp.exe` cạnh file nguồn và mở PowerShell riêng để chạy. Bạn nhập dữ liệu trực tiếp trong cửa sổ đó. Chạy xong cửa sổ giữ mở, hiện mã thoát; đóng bằng nút **X**. PowerShell tắt các prompt riêng của nó để tránh chờ nạp PSReadLine; chương trình C/C++ vẫn dùng console để nhập/xuất.

PowerShell ngoài VS Code có thể được Windows Terminal tiếp nhận tùy thiết lập terminal mặc định của Windows. Chương trình không chạy trong terminal tích hợp VS Code.

Mở `examples/hello.c` hoặc `examples/hello.cpp`, bấm ▶ rồi nhập `2 3`; kết quả là `Tong: 5`.

## Compiler và thư viện

Tự tìm các bộ Dev-C++ thường gặp: Orwell/Embarcadero, thư mục `MinGW64`, `MinGW32`, `TDM-GCC-64`, các vị trí cài đặt Windows và PATH. Header, thư viện chuẩn và runtime DLL được dùng từ bộ GCC/G++ đã tìm thấy; không cần chép thư viện sang VS Code hoặc sửa PATH hệ thống.

Nếu không tìm thấy, extension cho chọn thư mục Dev-C++ hoặc thư mục `bin`. Với bản portable hoặc cài ở ổ khác, có thể đặt **Settings → Devcpp Build Run: Compiler Path**, ví dụ:

```json
{
  "devcppBuildRun.compilerPath": "C:\\Program Files (x86)\\Dev-Cpp",
  "devcppBuildRun.compilerArgs": ["-Wall", "-Wextra"],
  "devcppBuildRun.programArgs": []
}
```

`compilerPath` cũng nhận đường dẫn `bin`, `gcc.exe` hoặc `g++.exe`; thư mục phải có cả gcc và g++. Nếu cấu hình sai, sửa/xóa đường dẫn này để tự tìm lại.

Mỗi phần tử trong `compilerArgs`/`programArgs` là **một đối số**, không ghép thành một câu lệnh shell. Ví dụ `"compilerArgs": ["-Wall", "-Wextra", "-std=c++11"]`. Thư viện bên thứ ba cần cấu hình `-I`, `-L`, `-l` phù hợp; bản đầu không nhập cấu hình project/thư viện tùy chỉnh từ Dev-C++ và không cấu hình IntelliSense. Chuẩn C/C++ mặc định theo compiler, vì Dev-C++ cũ có thể chưa hỗ trợ chuẩn mới.

## Khi gặp lỗi

- **Biên dịch lỗi:** chọn **Xem lỗi**, hoặc View → Output → Dev-C++ Build & Run để xem chi tiết. Build lỗi sẽ không chạy executable cũ.
- **Không ghi được .exe:** đóng chương trình cũ đang chạy, kiểm tra quyền ghi thư mục nguồn rồi thử lại.
- **Thiếu compiler:** kiểm tra bộ Dev-C++ có cài kèm GCC/MinGW hay chưa; bản chỉ có IDE không đủ để build.
- **Không có nút ▶:** mở file đã lưu có đuôi hỗ trợ trên VS Code Windows cục bộ. Kiểm tra extension đã bật và workspace được tin cậy. Nếu toolbar bị chật, lệnh có thể nằm trong menu **…** của editor.
- **WSL/SSH/container:** mở thư mục trực tiếp trên Windows để dùng compiler Dev-C++ và PowerShell trên máy.
- **Đường dẫn Unicode với GCC cũ:** extension giữ nguyên đường dẫn, nhưng một số GCC/MinGW cũ có thể không đọc được tên thư mục có dấu. Nếu compiler báo không tìm thấy file, thử thư mục không dấu.

Bản đầu build **một file nguồn đang mở**. Project nhiều file, `.dev`, debugger và IntelliSense nằm ngoài phạm vi bản này.

## Phát triển

Mã nguồn CommonJS, không có dependency runtime. Chạy `node --test test/*.test.cjs`. Đóng gói bằng `pnpm install` rồi `pnpm run package`; VSIX nằm trong `dist/`.
