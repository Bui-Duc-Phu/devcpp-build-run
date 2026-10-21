# Dev-C++ Build & Run

## [**Vì sao extension này ra đời?**](#cài-đặt)

[**Bạn muốn code C/C++ trên VS Code, nhưng vừa bắt đầu đã phải lo thiết lập môi trường, chỉnh đường dẫn, cấu hình build rồi xử lý đủ kiểu lỗi? Với những bạn mới học, đôi khi chưa kịp viết chương trình đầu tiên đã thấy nản vì phần cài đặt.**](#cài-đặt)

[**Vì vậy, Dev-C++ Build & Run được sinh ra để giúp bạn bớt loay hoay với những bước đó. Khi máy đã cài Dev-C++, bạn chỉ cần cài extension, mở file C/C++ rồi bấm ▶. Extension tự nhận Dev-C++ và mở PowerShell riêng để chạy chương trình — để bạn dành thời gian cho việc học và viết code.**](#cài-đặt)

[**Điều kiện cần: máy Windows đã cài VS Code và Dev-C++.**](#cài-đặt)

Extension VS Code cho Windows: mở file C/C++, bấm **▶** ở góc phải editor để build bằng Dev-C++ và chạy trong **cửa sổ PowerShell riêng**.

**[Tải extension .vsix](https://github.com/Bui-Duc-Phu/devcpp-build-run/releases/latest/download/devcpp-build-run-0.1.0.vsix)** · **[Xem bản phát hành](https://github.com/Bui-Duc-Phu/devcpp-build-run/releases/latest)**

Chỉ cần **VS Code + Dev-C++ đã cài trên máy**;

## Cài đặt

1. Cài VS Code 1.85 trở lên và Dev-C++ trên máy Windows.
2. Trong VS Code nhấn **Ctrl+Shift+X**, chọn dấu **…** ở đầu bảng Extensions → **Install from VSIX…**.
3. Chọn `devcpp-build-run-0.1.0.vsix` để cài extension.

   ![Cài xong nhớ Reload lại VS Code!](https://github.com/user-attachments/assets/41c5a547-57ab-4687-8430-a4ffef706fbb)

4. **Reload lại VS Code:** nhấn **Ctrl+Shift+P** → gõ **Reload Window** → chọn **Developer: Reload Window**.
5. Mở thư mục chứa code 
6. Mở file `.c`, `.cpp`, `.cc` hoặc `.cxx`, bấm nút tam giác **Dev-C++: Build & Run** ở góc phải editor. Có thể tìm cùng tên lệnh bằng **Ctrl+Shift+P**.

**Giao diện sau khi cài đặt thành công trong VS Code:**

![Dev-C++ Build & Run đã được cài đặt trong VS Code](https://github.com/user-attachments/assets/7f32b8fb-1168-4e65-bd36-14212e07c602)

Bạn cũng có thể cài bằng CLI:

```powershell
code --install-extension "C:\duong-dan\devcpp-build-run-0.1.0.vsix"
```

## Cách chạy

Extension lưu file, tự nhận Dev-C++, build ra `.devcpp-build\ten-file.cpp.exe` cạnh file nguồn và mở PowerShell riêng để chạy. Bạn nhập dữ liệu trực tiếp trong cửa sổ đó. Chạy xong cửa sổ giữ mở, hiện mã thoát; đóng bằng nút **X**.

PowerShell ngoài VS Code có thể được Windows Terminal tiếp nhận tùy thiết lập terminal mặc định của Windows. Chương trình không chạy trong terminal tích hợp VS Code.

Mở `examples/hello.c` hoặc `examples/hello.cpp`, bấm ▶ rồi nhập `2 3`; kết quả là `Tong: 5`.

## Tự nhận Dev-C++

Extension tự tìm Dev-C++ đã cài trên máy và sử dụng các thành phần sẵn có của Dev-C++. Bạn không cần tự chép thư viện sang VS Code hay chỉnh đường dẫn hệ thống.

Nếu không tự nhận được, extension sẽ cho bạn chọn thư mục đã cài Dev-C++. Với bản portable hoặc cài ở ổ khác, có thể đặt **Settings → Devcpp Build Run: Compiler Path**, ví dụ:

```json
{
  "devcppBuildRun.compilerPath": "C:\\Program Files (x86)\\Dev-Cpp",
  "devcppBuildRun.compilerArgs": ["-Wall", "-Wextra"],
  "devcppBuildRun.programArgs": []
}
```

Trong `compilerPath`, hãy nhập đường dẫn thư mục cài Dev-C++. Nếu chọn nhầm, sửa hoặc xóa đường dẫn này để extension tự tìm lại.

Mỗi phần tử trong `compilerArgs`/`programArgs` là **một đối số**, không ghép thành một câu lệnh shell. Ví dụ `"compilerArgs": ["-Wall", "-Wextra", "-std=c++11"]`. Thư viện bên thứ ba cần cấu hình `-I`, `-L`, `-l` phù hợp; bản đầu không nhập cấu hình project/thư viện tùy chỉnh từ Dev-C++ và không cấu hình IntelliSense. Chuẩn C/C++ mặc định theo compiler, vì Dev-C++ cũ có thể chưa hỗ trợ chuẩn mới.

## Khi gặp lỗi

- **Biên dịch lỗi:** chọn **Xem lỗi**, hoặc View → Output → Dev-C++ Build & Run để xem chi tiết. Build lỗi sẽ không chạy executable cũ.
- **Không ghi được .exe:** đóng chương trình cũ đang chạy, kiểm tra quyền ghi thư mục nguồn rồi thử lại.
- **Không tìm thấy Dev-C++:** kiểm tra Dev-C++ đã cài trên máy, rồi chọn đúng thư mục cài đặt trong extension.
- **Không có nút ▶:** mở file đã lưu có đuôi hỗ trợ trên VS Code Windows cục bộ. Kiểm tra extension đã bật và workspace được tin cậy. Nếu toolbar bị chật, lệnh có thể nằm trong menu **…** của editor.
- **WSL/SSH/container:** mở thư mục trực tiếp trên Windows để dùng Dev-C++ và PowerShell trên máy.
- **Tên thư mục có dấu:** một số bản Dev-C++ cũ có thể không đọc được tên thư mục có dấu. Nếu báo không tìm thấy file, thử thư mục không dấu.

Bản đầu build **một file nguồn đang mở**. Project nhiều file, `.dev`, debugger và IntelliSense nằm ngoài phạm vi bản này.

## Phát triển

Mã nguồn CommonJS, không có dependency runtime. Chạy `node --test test/*.test.cjs`. Đóng gói bằng `pnpm install` rồi `pnpm run package`; VSIX nằm trong `dist/`.
