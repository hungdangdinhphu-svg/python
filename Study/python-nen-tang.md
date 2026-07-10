# Python Từ Con Số 0: Nền Tảng Trước Khi Đọc "Từ Python Yếu Đến Senior"

> **Dành cho ai:** Bạn chưa từng lập trình bao giờ, mới cài Python vào máy, chưa biết biến/vòng lặp/hàm là gì.
>
> **Mục tiêu:** Sau khi đọc và **gõ tay theo từng ví dụ**, bạn sẽ đủ nền tảng để đọc hiểu tài liệu `huong-dan-python-senior.md` mà bạn đã có sẵn — tài liệu đó giả định bạn *đã* biết những gì viết trong tài liệu này.

---

## Cách dùng tài liệu này

Ba nguyên tắc, giống hệt tài liệu senior mà bạn sẽ đọc tiếp theo — vì đây là thói quen đúng ngay từ đầu:

1. **Gõ lại tay từng dòng code, đừng chỉ đọc.** Mở một cửa sổ terminal/editor bên cạnh khi đọc, gõ theo, chạy thử, xem kết quả có đúng không. Đọc suông sẽ quên trong 1 tuần; tự gõ và tự sai sẽ nhớ.
2. **Làm bài tập 🔨 trước khi đọc tiếp**, đừng bỏ qua dù thấy dễ. Bài tập ở đây đều rất ngắn (1-5 phút), mục đích là buộc tay bạn "chạm" vào khái niệm vừa học chứ không phải để đánh đố.
3. **Không hiểu 100% ngay lần đầu là bình thường.** Lập trình là kỹ năng vận động (giống học đi xe đạp) chứ không phải kiến thức ghi nhớ. Đọc xong Phần 1, làm bài tập, sai vài lần, sửa được — đó chính là quá trình học, không phải dấu hiệu bạn "không hợp".

Tài liệu chia làm 13 phần, đọc **theo đúng thứ tự**, vì phần sau luôn dùng lại khái niệm phần trước:

0. (Bạn đang ở đây) Cách dùng tài liệu
1. Lập trình là gì & làm quen với Python
2. Biến, kiểu dữ liệu, toán tử — những viên gạch đầu tiên
3. Chuỗi (string) — làm việc với văn bản
4. Câu lệnh điều kiện — dạy máy tính "ra quyết định"
5. Vòng lặp — dạy máy tính "lặp lại"
6. Cấu trúc dữ liệu: list, tuple, dict, set
7. Hàm (function) — tái sử dụng code
8. Xử lý lỗi cơ bản — khi chương trình "nổ"
9. Làm việc với file
10. Module và thư viện
11. Lập trình hướng đối tượng (OOP) cơ bản
12. Ba dự án nhỏ tổng hợp
13. Bản đồ nối sang tài liệu Senior

Sau khi xong Phần 13, bạn quay lại file `huong-dan-python-senior.md` và bắt đầu từ Phần 1 của nó — lúc đó mọi thứ trong đó sẽ có nghĩa.

---

## PHẦN 1: LẬP TRÌNH LÀ GÌ & LÀM QUEN VỚI PYTHON

### 1.1. Lập trình là gì, thực ra?

Máy tính rất "ngu" — nó không tự suy nghĩ, chỉ làm **chính xác** những gì bạn bảo nó làm, theo **đúng thứ tự** bạn viết ra. Lập trình là quá trình viết ra một chuỗi chỉ dẫn (gọi là **code** hoặc **mã nguồn**) để máy tính thực hiện từng bước, giống như viết công thức nấu ăn cho một người... rất máy móc làm theo.

Ví dụ công thức nấu ăn bằng tiếng Việt:
1. Đun sôi nước.
2. Cho mì vào.
3. Đợi 3 phút.
4. Vớt mì ra.

Lập trình cũng vậy, chỉ khác là viết bằng một **ngôn ngữ lập trình** (ở đây là Python) — thứ ngôn ngữ mà máy tính "hiểu" được sau khi qua một bước dịch.

### 1.2. Python là gì, và ai "dịch" code của bạn cho máy tính hiểu?

Python là một **ngôn ngữ lập trình** — một tập quy tắc về cách viết chỉ dẫn. Khi bạn viết file `.py`, máy tính không đọc hiểu trực tiếp được; cần một chương trình gọi là **Python interpreter** (trình thông dịch) đọc code của bạn từng dòng và thực thi nó ngay lập tức. Đây là lý do khi bạn "chạy" một file Python, thực chất bạn đang ra lệnh cho interpreter đọc và thực thi file đó.

Python được chọn làm ngôn ngữ học đầu tiên phổ biến nhất thế giới vì cú pháp gần với tiếng Anh tự nhiên, ít ký hiệu rườm rà (không cần dấu `;` cuối dòng, không cần khai báo kiểu dữ liệu tường minh) hơn nhiều ngôn ngữ khác như Java hay C.

### 1.3. Kiểm tra Python đã cài đúng chưa

Bạn nói đã tải Python về máy — giờ hãy xác nhận nó hoạt động. Mở **terminal** (trên Windows gọi là Command Prompt hoặc PowerShell; trên Mac/Linux gọi là Terminal) và gõ:

```bash
python3 --version
```

Nếu máy bạn là Windows và lệnh trên báo lỗi "không tìm thấy lệnh", thử:

```bash
python --version
```

Bạn sẽ thấy kết quả dạng `Python 3.12.1` (số phiên bản có thể khác, miễn là bắt đầu bằng số 3 — Python 2 đã ngừng hỗ trợ từ 2020, nếu máy bạn hiện Python 2.x hãy cài lại bản Python 3 mới nhất từ [python.org](https://www.python.org/)).

> 💡 Từ đây về sau, tài liệu này dùng `python3`. Nếu máy bạn chỉ nhận `python`, cứ thay thế tương ứng trong mọi lệnh.

### 1.4. Ba cách chạy code Python

**Cách 1 — REPL (chế độ tương tác):** gõ `python3` (không có gì phía sau) vào terminal, bạn sẽ vào một chế độ gõ-và-chạy-ngay, dấu nhắc `>>>` xuất hiện:

```
>>> 2 + 3
5
>>> print("Xin chào")
Xin chào
```

Gõ `exit()` hoặc bấm `Ctrl+D` (Mac/Linux) / `Ctrl+Z` rồi Enter (Windows) để thoát. REPL rất tiện để thử nhanh 1 dòng code, nhưng không dùng để viết chương trình thật vì không lưu lại được.

**Cách 2 — Chạy file `.py`:** đây là cách bạn sẽ dùng 95% thời gian. Viết code vào một file có đuôi `.py`, lưu lại, rồi chạy bằng terminal:

```bash
python3 ten_file.py
```

**Cách 3 — Notebook (Jupyter):** phổ biến trong phân tích dữ liệu/AI, cho phép chạy từng ô code riêng lẻ. Không cần quan tâm ở giai đoạn này — tài liệu senior bạn sắp đọc không dùng notebook, nên ta bỏ qua.

### 1.5. Chọn công cụ soạn code (editor)

Bạn có thể viết file `.py` bằng Notepad, nhưng sẽ rất bất tiện vì không có tô màu cú pháp, không báo lỗi trước khi chạy. Công cụ được khuyên dùng nhất hiện nay là **Visual Studio Code (VS Code)** — miễn phí, tải tại [code.visualstudio.com](https://code.visualstudio.com/). Sau khi cài, mở VS Code, cài thêm extension tên **"Python"** (do Microsoft phát hành) từ tab Extensions (biểu tượng 4 ô vuông ở thanh bên trái) — extension này cho bạn gợi ý code, tô màu, báo lỗi cú pháp ngay khi gõ.

### 1.6. Làm quen terminal — bạn sẽ dùng nó suốt đời lập trình viên

Vài lệnh tối thiểu cần biết (terminal tích hợp sẵn trong VS Code: menu `Terminal` → `New Terminal`):

| Lệnh | Ý nghĩa | Ví dụ |
|---|---|---|
| `cd <thư mục>` | Di chuyển vào thư mục | `cd Documents/python-hoc` |
| `cd ..` | Lùi ra thư mục cha | `cd ..` |
| `ls` (Mac/Linux) hoặc `dir` (Windows) | Liệt kê file trong thư mục hiện tại | `ls` |
| `pwd` (Mac/Linux) | In ra đường dẫn thư mục hiện tại | `pwd` |
| `python3 file.py` | Chạy file Python | `python3 hello.py` |

🔨 **Bài tập 1:**
1. Tạo một thư mục tên `python-hoc` ở đâu đó dễ tìm (Desktop chẳng hạn).
2. Mở thư mục đó bằng VS Code (`File` → `Open Folder`).
3. Tạo file mới tên `hello.py`, gõ đúng dòng này (không copy-paste, gõ tay):
   ```python
   print("Xin chào, tôi đang học Python!")
   ```
4. Mở terminal trong VS Code, chạy `python3 hello.py`.
5. Xác nhận bạn thấy đúng dòng chữ đó hiện ra trên terminal.

Nếu bước 5 thành công — chúc mừng, bạn vừa chạy chương trình Python đầu tiên. Nếu có lỗi, đọc kỹ dòng lỗi (thường Python sẽ chỉ rõ sai ở đâu), đây cũng là kỹ năng bạn sẽ luyện suốt Phần 8.

---

## PHẦN 2: BIẾN, KIỂU DỮ LIỆU, TOÁN TỬ — NHỮNG VIÊN GẠCH ĐẦU TIÊN

### 2.1. Biến là gì?

Biến (variable) là một cái **tên** bạn đặt ra để "gắn" vào một giá trị, để dùng lại sau này thay vì gõ lại giá trị đó mỗi lần.

```python
ten = "An"
tuoi = 25
print(ten)     # An
print(tuoi)    # 25
```

Ở đây `=` là **toán tử gán** (assignment) — không phải "bằng nhau" như trong toán học, mà nghĩa là "gán giá trị bên phải cho cái tên bên trái". Đọc `ten = "An"` là "đặt tên `ten` trỏ tới giá trị `"An"`".

**Quy tắc đặt tên biến trong Python:**
- Chỉ gồm chữ cái, số, dấu gạch dưới `_`; không được bắt đầu bằng số.
- Có phân biệt hoa/thường: `tuoi` và `Tuoi` là hai biến khác nhau.
- Quy ước cộng đồng Python (bạn sẽ thấy trong tài liệu senior gọi là `snake_case`): tên biến viết thường, các từ nối nhau bằng `_`. Ví dụ: `so_du_tai_khoan`, không viết `SoDuTaiKhoan` hay `soDuTaiKhoan` (đó là quy ước của ngôn ngữ khác như Java/C#).
- Tên nên có ý nghĩa: `tuoi` tốt hơn nhiều so với `x` hay `a`.

```python
# Có thể gán lại giá trị mới cho biến bất cứ lúc nào
diem = 8
diem = 9      # bây giờ diem là 9, giá trị cũ bị "quên"
```

### 2.2. Các kiểu dữ liệu cơ bản

Mỗi giá trị trong Python thuộc về một **kiểu dữ liệu** (data type). 5 kiểu bạn cần biết trước tiên:

| Kiểu | Tên Python | Ví dụ | Ý nghĩa |
|---|---|---|---|
| Số nguyên | `int` | `5`, `-3`, `1000` | Số không có phần thập phân |
| Số thực | `float` | `3.14`, `-0.5` | Số có phần thập phân |
| Chuỗi văn bản | `str` | `"Xin chào"`, `'An'` | Văn bản, đặt trong `"` hoặc `'` |
| Boolean (đúng/sai) | `bool` | `True`, `False` | Chỉ có 2 giá trị, dùng cho điều kiện |
| Rỗng/không có gì | `NoneType` | `None` | Đại diện "không có giá trị" |

Dùng hàm `type()` để kiểm tra một giá trị thuộc kiểu gì — rất hữu ích khi bạn không chắc:

```python
print(type(5))          # <class 'int'>
print(type(3.14))       # <class 'float'>
print(type("An"))       # <class 'str'>
print(type(True))       # <class 'bool'>
print(type(None))       # <class 'NoneType'>
```

> 💡 Python **tự nhận biết** kiểu dữ liệu khi bạn gán giá trị, không cần khai báo trước như `int tuoi = 25;` trong Java/C. Tài liệu senior gọi đặc điểm này là "dynamically typed" — bạn sẽ hiểu rõ hơn về khái niệm này khi đọc tới đó, giờ chỉ cần nhớ: **không cần nói trước Python biến này chứa kiểu gì**.

### 2.3. Toán tử số học

```python
a = 10
b = 3

print(a + b)    # 13   — cộng
print(a - b)    # 7    — trừ
print(a * b)    # 30   — nhân
print(a / b)    # 3.333333333333335 — chia, LUÔN trả về float
print(a // b)   # 3    — chia lấy phần nguyên (bỏ phần thập phân)
print(a % b)    # 1    — chia lấy số dư (modulo)
print(a ** b)   # 1000 — lũy thừa (10 mũ 3)
```

`//` và `%` là hai toán tử bạn sẽ dùng rất nhiều — ví dụ kiểm tra một số có chia hết cho 2 không (số chẵn):

```python
so = 8
if so % 2 == 0:
    print("Số chẵn")
```

(Cú pháp `if` sẽ học kỹ ở Phần 4, ở đây chỉ để bạn thấy `%` dùng làm gì trong thực tế.)

### 2.4. Toán tử so sánh và toán tử logic

Toán tử so sánh trả về một giá trị `bool` (`True` hoặc `False`):

```python
print(5 == 5)    # True   — bằng nhau (chú ý: 2 dấu = , khác với gán biến chỉ 1 dấu =)
print(5 != 3)    # True   — khác nhau
print(5 > 3)     # True   — lớn hơn
print(5 < 3)     # False  — nhỏ hơn
print(5 >= 5)    # True   — lớn hơn hoặc bằng
print(5 <= 3)    # False  — nhỏ hơn hoặc bằng
```

⚠️ **Bẫy rất phổ biến với người mới:** nhầm `=` (gán) với `==` (so sánh bằng nhau). `a = 5` gán giá trị; `a == 5` kiểm tra a có bằng 5 không.

Toán tử logic kết hợp nhiều điều kiện `bool` lại với nhau:

```python
tuoi = 20
co_bang_lai = True

print(tuoi >= 18 and co_bang_lai)   # True  — AND: cả 2 phải True thì kết quả mới True
print(tuoi >= 18 or co_bang_lai)    # True  — OR: chỉ cần 1 trong 2 True
print(not co_bang_lai)              # False — NOT: đảo ngược giá trị
```

### 2.5. Toán tử gán rút gọn

```python
diem = 5
diem += 1     # tương đương diem = diem + 1  -> diem = 6
diem -= 2     # tương đương diem = diem - 2  -> diem = 4
diem *= 3     # tương đương diem = diem * 3  -> diem = 12
diem /= 4     # tương đương diem = diem / 4  -> diem = 3.0
```

### 2.6. `print()`, `input()`, và chuyển đổi kiểu dữ liệu

`print()` in giá trị ra màn hình — bạn đã dùng ở Phần 1. Có thể in nhiều giá trị cùng lúc, cách nhau bằng dấu phẩy:

```python
ten = "An"
tuoi = 25
print("Tên:", ten, "- Tuổi:", tuoi)   # Tên: An - Tuổi: 25
```

`input()` đọc dữ liệu người dùng gõ vào từ bàn phím — **luôn trả về kiểu `str`**, kể cả khi người dùng gõ số:

```python
ten = input("Nhập tên của bạn: ")
print("Xin chào,", ten)
```

Vì `input()` luôn trả về chuỗi, nếu bạn muốn xử lý như số, phải **chuyển đổi kiểu** (type casting) bằng `int()` hoặc `float()`:

```python
tuoi_str = input("Nhập tuổi: ")   # ví dụ người dùng gõ "25" -> tuoi_str = "25" (là str, không phải số)
tuoi = int(tuoi_str)              # chuyển "25" (str) thành 25 (int)
print(tuoi + 1)                   # 26 — giờ mới cộng số được

# Viết gọn trong 1 dòng:
tuoi = int(input("Nhập tuổi: "))
```

⚠️ Nếu người dùng gõ chữ không phải số (ví dụ "hai mươi lăm") mà bạn gọi `int(...)`, chương trình sẽ báo lỗi (`ValueError`) và dừng lại — cách xử lý việc này đúng chuẩn sẽ học ở Phần 8.

Chiều ngược lại, `str()` chuyển số thành chuỗi (hữu ích khi muốn nối số vào một câu chữ):

```python
tuoi = 25
print("Tuổi: " + str(tuoi))   # nối chuỗi, cần tuoi phải là str trước
```

🔨 **Bài tập 2:** Viết file `tinh_tong.py`:
1. Dùng `input()` hỏi người dùng nhập 2 số.
2. Chuyển cả 2 sang kiểu `float`.
3. In ra tổng, hiệu, tích, thương của 2 số đó, mỗi phép tính một dòng, có nhãn rõ ràng (ví dụ: `Tổng: 15.0`).

---

## PHẦN 3: CHUỖI (STRING) — LÀM VIỆC VỚI VĂN BẢN

### 3.1. Tạo chuỗi và nối chuỗi

```python
ho = "Nguyễn Văn"
ten = "An"
ho_ten = ho + " " + ten     # nối chuỗi bằng +
print(ho_ten)                # Nguyễn Văn An
```

Dùng `"` hay `'` đều được, miễn nhất quán. Nếu chuỗi cần chứa dấu nháy, dùng loại nháy còn lại để bao ngoài:

```python
cau = "Cô ấy nói: 'Xin chào'"
```

### 3.2. Index và slicing — lấy 1 phần của chuỗi

Mỗi ký tự trong chuỗi có một **vị trí (index)**, bắt đầu đếm từ **0**, không phải từ 1:

```python
tu = "Python"
#     P  y  t  h  o  n
#     0  1  2  3  4  5    (đếm từ trái, từ 0)
#    -6 -5 -4 -3 -2 -1    (đếm từ phải, từ -1)

print(tu[0])     # P     — ký tự đầu tiên
print(tu[5])     # n     — ký tự cuối cùng (index 5)
print(tu[-1])    # n     — cách khác để lấy ký tự cuối
print(tu[-2])    # o     — ký tự áp chót
```

**Slicing** — lấy một đoạn con, cú pháp `chuoi[bat_dau:ket_thuc]` (lấy từ `bat_dau` đến **trước** `ket_thuc`, không bao gồm `ket_thuc`):

```python
tu = "Python"
print(tu[0:3])    # Pyt   — từ index 0 đến trước index 3
print(tu[2:])     # thon  — từ index 2 đến hết
print(tu[:2])     # Py    — từ đầu đến trước index 2
print(tu[:])      # Python — toàn bộ chuỗi (copy)
```

`len()` trả về độ dài chuỗi (số ký tự):

```python
print(len("Python"))    # 6
```

### 3.3. Các method thường dùng của chuỗi

Chuỗi có sẵn nhiều **method** (hàm gắn liền với giá trị, gọi bằng dấu chấm `.`) hữu ích:

```python
s = "  Xin Chào Việt Nam  "

print(s.strip())          # "Xin Chào Việt Nam"  — xóa khoảng trắng thừa 2 đầu
print(s.lower())           # "  xin chào việt nam  " — chuyển thành chữ thường
print(s.upper())           # "  XIN CHÀO VIỆT NAM  " — chuyển thành chữ hoa
print(s.strip().replace("Chào", "Xin Chào"))  # thay thế đoạn chuỗi con

cau = "python,java,c++"
print(cau.split(","))      # ['python', 'java', 'c++']  — tách chuỗi thành list theo dấu phẩy

danh_sach = ["python", "java", "c++"]
print(", ".join(danh_sach))   # "python, java, c++"  — ghép list thành 1 chuỗi, ngược lại với split

print("Python" in "Tôi học Python")    # True — kiểm tra chuỗi con có tồn tại không
print("python".startswith("py"))       # True
print("python".endswith("on"))         # True
```

> 💡 `.split()` và `.join()` là 2 method bạn sẽ dùng rất thường xuyên khi xử lý dữ liệu văn bản thật (ví dụ đọc file CSV ở Phần 9).

### 3.4. f-string — cách chuẩn để chèn giá trị vào chuỗi

Thay vì nối chuỗi bằng `+` (dễ lỗi, khó đọc khi nhiều biến), Python hiện đại dùng **f-string**: thêm chữ `f` ngay trước dấu nháy, rồi đặt biến trong `{}`:

```python
ten = "An"
tuoi = 25

# Nối bằng + — dài dòng, dễ quên str()
print("Tên: " + ten + ", tuổi: " + str(tuoi))

# f-string — ngắn gọn, rõ ràng, tự chuyển kiểu
print(f"Tên: {ten}, tuổi: {tuoi}")   # Tên: An, tuổi: 25
```

f-string còn tính toán được biểu thức ngay bên trong `{}`:

```python
gia = 50000
so_luong = 3
print(f"Tổng tiền: {gia * so_luong} VNĐ")   # Tổng tiền: 150000 VNĐ
```

Từ giờ, **luôn dùng f-string** để chèn giá trị vào chuỗi — đây cũng chính là quy ước tài liệu senior sẽ nhắc lại ở mục 1.6 của nó.

🔨 **Bài tập 3:** Viết file `chao_hoi.py`:
1. Dùng `input()` hỏi tên và năm sinh của người dùng.
2. Tính tuổi (lấy 2026 trừ năm sinh — dùng số 2026 cố định, chưa cần lấy năm hiện tại thật).
3. In ra một câu chào đầy đủ bằng f-string, ví dụ: `Xin chào An, năm nay bạn 25 tuổi.`
4. Thử in tên người dùng bằng chữ hoa toàn bộ, dùng `.upper()`.

---

## PHẦN 4: CÂU LỆNH ĐIỀU KIỆN — DẠY MÁY TÍNH "RA QUYẾT ĐỊNH"

### 4.1. `if` cơ bản và thụt lề (indentation)

Chương trình cho tới giờ luôn chạy từ trên xuống dưới, tuần tự. `if` cho phép chương trình **chỉ chạy một đoạn code khi một điều kiện đúng**:

```python
tuoi = 20

if tuoi >= 18:
    print("Bạn đã đủ tuổi trưởng thành")
    print("Dòng này cũng thuộc khối if")

print("Dòng này LUÔN chạy, không phụ thuộc if")
```

Đây là điểm **khác biệt lớn nhất** giữa Python và phần lớn ngôn ngữ khác (C, Java, JavaScript...): những ngôn ngữ đó dùng dấu ngoặc `{ }` để xác định một khối code thuộc về `if` nào; **Python dùng thụt lề (khoảng trắng đầu dòng)** để làm việc đó. Quy ước chuẩn: thụt lề bằng **4 dấu cách** (VS Code sẽ tự làm điều này khi bạn nhấn Tab, không cần lo lắng nếu đã cài extension Python).

⚠️ Thụt lề sai (thiếu, thừa, hoặc trộn lẫn tab và space) sẽ khiến Python báo lỗi `IndentationError`. Đây là lỗi cực kỳ phổ biến với người mới — nếu gặp, kiểm tra lại xem dòng đó có thụt đúng 4 space so với dòng `if` không.

### 4.2. `if / elif / else` — nhiều nhánh lựa chọn

```python
diem = 7.5

if diem >= 8.5:
    print("Xếp loại: Giỏi")
elif diem >= 7:
    print("Xếp loại: Khá")
elif diem >= 5:
    print("Xếp loại: Trung bình")
else:
    print("Xếp loại: Yếu")
```

Cách chạy: Python kiểm tra từ trên xuống, **điều kiện nào đúng trước sẽ chạy nhánh đó rồi bỏ qua toàn bộ phần còn lại** — kể cả khi điều kiện phía sau cũng đúng. `elif` là viết tắt của "else if", có thể có bao nhiêu nhánh `elif` cũng được; `else` (không có điều kiện) là nhánh "còn lại tất cả các trường hợp khác", luôn đặt cuối cùng và không bắt buộc phải có.

### 4.3. Lồng điều kiện (nested if)

Bạn có thể đặt `if` bên trong `if` khác khi cần kiểm tra nhiều tầng điều kiện:

```python
tuoi = 20
co_ve = True

if tuoi >= 18:
    if co_ve:
        print("Được vào rạp")
    else:
        print("Đủ tuổi nhưng chưa có vé")
else:
    print("Chưa đủ tuổi")
```

Cách viết trên đúng nhưng hơi rối; thường gọn hơn khi kết hợp bằng `and`:

```python
if tuoi >= 18 and co_ve:
    print("Được vào rạp")
elif tuoi >= 18 and not co_ve:
    print("Đủ tuổi nhưng chưa có vé")
else:
    print("Chưa đủ tuổi")
```

> 💡 Đây là bài học đầu tiên về việc **cùng một logic có nhiều cách viết** — tài liệu senior (mục 1.1) sẽ đi sâu vào việc chọn cách viết nào "đúng chất Python" hơn. Ở giai đoạn này, bạn chỉ cần hiểu và viết được logic đúng; viết "đẹp" sẽ luyện dần.

### 4.4. So sánh với `None`

`None` đại diện cho "không có giá trị gì". Khi so sánh một biến với `None`, quy ước Python là dùng `is` chứ không dùng `==`:

```python
ket_qua = None

if ket_qua is None:
    print("Chưa có kết quả")

if ket_qua is not None:
    print("Đã có kết quả")
```

(Vì sao dùng `is` thay vì `==` cho `None` là kiến thức nâng cao hơn — tạm thời bạn chỉ cần nhớ **quy tắc**: so `None` luôn dùng `is` / `is not`, so giá trị khác dùng `==` / `!=`.)

🔨 **Bài tập 4:** Viết file `phan_loai_bmi.py`:
1. Hỏi người dùng nhập cân nặng (kg) và chiều cao (mét).
2. Tính BMI = cân nặng / (chiều cao * chiều cao).
3. Dùng `if/elif/else` phân loại: BMI < 18.5 → "Thiếu cân"; 18.5-24.9 → "Bình thường"; 25-29.9 → "Thừa cân"; còn lại → "Béo phì".
4. In kết quả bằng f-string, làm tròn BMI 1 chữ số thập phân (gợi ý: `round(bmi, 1)`).

---

## PHẦN 5: VÒNG LẶP — DẠY MÁY TÍNH "LẶP LẠI"

### 5.1. Vì sao cần vòng lặp

Nếu muốn in số từ 1 đến 5, bạn có thể viết 5 dòng `print()` — nhưng nếu là in từ 1 đến 1 triệu thì sao? Vòng lặp giải quyết việc **chạy lại một đoạn code nhiều lần** mà không phải chép tay.

### 5.2. `while` — lặp khi còn thỏa điều kiện

```python
dem = 1
while dem <= 5:
    print(dem)
    dem += 1     # QUAN TRỌNG: phải tự tăng dem, nếu không vòng lặp chạy MÃI MÃI
```

Kết quả: in ra 1, 2, 3, 4, 5, mỗi số một dòng. Cách hoạt động: trước mỗi vòng, Python kiểm tra điều kiện `dem <= 5`; còn đúng thì chạy khối code bên trong, sai thì dừng.

⚠️ **Bẫy kinh điển của người mới — vòng lặp vô hạn (infinite loop):** nếu quên dòng `dem += 1`, điều kiện `dem <= 5` mãi mãi đúng (vì `dem` luôn là 1), chương trình chạy mãi không dừng, treo máy/terminal. Nếu lỡ bị vậy, nhấn `Ctrl + C` trong terminal để dừng chương trình.

### 5.3. `for` — lặp qua một dãy giá trị có sẵn

`for` là loại vòng lặp bạn sẽ dùng nhiều hơn `while` rất nhiều trong thực tế, vì phần lớn việc lặp là để "duyệt qua" một tập dữ liệu có sẵn (chuỗi, list...).

```python
for ky_tu in "Python":
    print(ky_tu)
# In ra từng ký tự: P, y, t, h, o, n (mỗi ký tự 1 dòng)
```

Kết hợp với `range()` để lặp theo số lần cho trước:

```python
for i in range(5):
    print(i)
# In ra: 0, 1, 2, 3, 4   (range(5) sinh ra 0,1,2,3,4 — KHÔNG bao gồm 5, giống quy tắc slicing ở Phần 3)

for i in range(1, 6):
    print(i)
# In ra: 1, 2, 3, 4, 5   (bắt đầu từ 1, kết thúc trước 6)

for i in range(0, 10, 2):
    print(i)
# In ra: 0, 2, 4, 6, 8   (bước nhảy 2, tức mỗi lần +2)
```

So sánh `while` và `for`: dùng `while` khi bạn **không biết trước** sẽ lặp bao nhiêu lần (phụ thuộc điều kiện thay đổi lúc chạy); dùng `for` khi bạn **biết trước** số lần lặp hoặc đang duyệt qua một tập dữ liệu có sẵn. Phần lớn trường hợp thực tế dùng `for` nhiều hơn.

### 5.4. `break` và `continue`

`break` — thoát khỏi vòng lặp ngay lập tức, bỏ qua các lần lặp còn lại:

```python
for i in range(10):
    if i == 5:
        break        # dừng hẳn vòng lặp khi i bằng 5
    print(i)
# In ra: 0, 1, 2, 3, 4
```

`continue` — bỏ qua phần còn lại của lần lặp hiện tại, nhảy sang lần lặp kế tiếp (không thoát hẳn vòng lặp):

```python
for i in range(10):
    if i % 2 != 0:
        continue     # nếu i là số lẻ, bỏ qua, không in
    print(i)
# In ra: 0, 2, 4, 6, 8
```

### 5.5. Vòng lặp lồng nhau (nested loop)

```python
for hang in range(3):
    for cot in range(3):
        print(f"({hang},{cot})", end=" ")
    print()   # xuống dòng sau khi hết 1 hàng
```

Kết quả in ra một lưới 3x3 tọa độ — vòng lặp trong (`cot`) chạy hết trước, rồi vòng lặp ngoài (`hang`) mới sang giá trị tiếp theo. (`end=" "` là tham số của `print()` để thay việc tự xuống dòng bằng in thêm 1 dấu cách — mặc định `print()` luôn tự xuống dòng.)

🔨 **Bài tập 5:** Viết file `bang_cuu_chuong.py`:
1. Hỏi người dùng nhập một số nguyên `n`.
2. Dùng vòng lặp `for` in ra bảng cửu chương của `n`, từ `n x 1` đến `n x 10`, mỗi dòng một phép tính, ví dụ: `3 x 1 = 3`.
3. Thử thêm: chỉ in ra những dòng có kết quả là số chẵn (dùng `if` + `%` đã học).

---

## PHẦN 6: CẤU TRÚC DỮ LIỆU: LIST, TUPLE, DICT, SET

Tới giờ mỗi biến chỉ chứa **một** giá trị (một số, một chuỗi...). Phần này học cách gom **nhiều giá trị** vào một biến duy nhất.

### 6.1. List — danh sách có thứ tự, thay đổi được

List là cấu trúc bạn sẽ dùng nhiều nhất. Nó giống một "hàng" các giá trị, có thứ tự, có thể thêm/bớt/sửa.

```python
trai_cay = ["táo", "cam", "chuối"]
print(trai_cay)           # ['táo', 'cam', 'chuối']
print(len(trai_cay))      # 3 — số phần tử
```

**Truy cập bằng index** — giống hệt quy tắc index của chuỗi ở Phần 3 (bắt đầu từ 0):

```python
print(trai_cay[0])    # táo
print(trai_cay[-1])   # chuối  — phần tử cuối
print(trai_cay[0:2])  # ['táo', 'cam']  — slicing cũng dùng được như chuỗi
```

**Thêm, sửa, xóa phần tử:**

```python
trai_cay.append("xoài")        # thêm vào cuối -> ['táo', 'cam', 'chuối', 'xoài']
trai_cay.insert(1, "nho")      # chèn vào vị trí index 1 -> ['táo', 'nho', 'cam', 'chuối', 'xoài']
trai_cay[0] = "táo đỏ"          # sửa phần tử tại index 0
trai_cay.remove("cam")          # xóa theo GIÁ TRỊ (xóa phần tử "cam" đầu tiên tìm thấy)
phan_tu_cuoi = trai_cay.pop()   # xóa VÀ trả về phần tử cuối cùng
del trai_cay[0]                 # xóa theo INDEX
```

**Kiểm tra tồn tại và duyệt qua list:**

```python
if "xoài" in trai_cay:
    print("Có xoài")

for qua in trai_cay:
    print(qua)
```

**Vài method hữu ích khác:**

```python
so = [5, 2, 8, 1, 9]
so.sort()                 # sắp xếp TẠI CHỖ, tăng dần -> [1, 2, 5, 8, 9]
so.sort(reverse=True)     # giảm dần -> [9, 8, 5, 2, 1]
print(sum(so))            # tổng các phần tử
print(max(so))            # giá trị lớn nhất
print(min(so))            # giá trị nhỏ nhất
```

⚠️ **Điều quan trọng cần nhớ ngay từ đầu (sẽ giải thích sâu hơn ở tài liệu senior mục 1.2):** khi bạn gán một list cho biến khác, cả 2 biến **cùng trỏ tới một list**, không phải bản sao:

```python
a = [1, 2, 3]
b = a
b.append(4)
print(a)    # [1, 2, 3, 4]  <- a cũng bị thay đổi theo, dù bạn chỉ sửa b!
```

Nếu muốn có **bản sao thật sự**, dùng `.copy()` hoặc `list(...)`:

```python
a = [1, 2, 3]
b = a.copy()
b.append(4)
print(a)    # [1, 2, 3]  <- a KHÔNG bị ảnh hưởng
print(b)    # [1, 2, 3, 4]
```

Đây là một trong những nguồn gốc bug phổ biến nhất với người mới học Python — hãy nhớ kỹ hiện tượng này, tài liệu senior sẽ nhắc lại và mở rộng nó ngay từ những dòng đầu.

### 6.2. Tuple — giống list nhưng KHÔNG thể thay đổi sau khi tạo

```python
toa_do = (10, 20)
print(toa_do[0])     # 10 — truy cập giống list

# toa_do[0] = 5      # LỖI! TypeError — tuple không cho sửa phần tử
```

Vì sao cần tuple nếu đã có list? Dùng tuple khi bạn muốn diễn tả một **nhóm giá trị cố định, không nên bị thay đổi** — ví dụ tọa độ (x, y) luôn có đúng 2 giá trị, không có lý do gì để "thêm phần tử thứ 3" vào một tọa độ. Việc Python không cho sửa tuple giúp bạn tránh bug do vô tình sửa nhầm dữ liệu lẽ ra phải cố định.

### 6.3. Dict (dictionary) — ánh xạ khóa → giá trị

List truy cập bằng **vị trí** (index 0, 1, 2...); dict truy cập bằng **tên khóa (key)** do bạn tự đặt — giống một cuốn từ điển thật, tra từ (key) ra nghĩa (value).

```python
sinh_vien = {
    "ten": "An",
    "tuoi": 20,
    "diem": 8.5
}

print(sinh_vien["ten"])     # An — truy cập theo key
print(sinh_vien["tuoi"])    # 20
```

**Thêm, sửa, xóa:**

```python
sinh_vien["lop"] = "K20"          # thêm key mới (key chưa tồn tại -> tự tạo)
sinh_vien["tuoi"] = 21             # sửa (key đã tồn tại -> ghi đè giá trị)
del sinh_vien["diem"]              # xóa 1 key
```

⚠️ Nếu bạn truy cập một key **không tồn tại** bằng `sinh_vien["khong_ton_tai"]`, Python sẽ báo lỗi `KeyError` và dừng chương trình. Cách an toàn hơn là dùng `.get()`, cho phép đặt giá trị mặc định nếu key không có:

```python
print(sinh_vien.get("diem"))            # None (vì đã xóa ở trên) — không báo lỗi
print(sinh_vien.get("diem", 0))         # 0 — trả về giá trị mặc định thay vì None
```

**Duyệt qua dict:**

```python
for key in sinh_vien:
    print(key, "->", sinh_vien[key])

# Cách phổ biến hơn, lấy cả key và value cùng lúc:
for key, value in sinh_vien.items():
    print(f"{key}: {value}")
```

**Kiểm tra key tồn tại:**

```python
if "ten" in sinh_vien:
    print("Có key 'ten'")
```

> 💡 Dict là một trong những cấu trúc quan trọng nhất của Python — dữ liệu thực tế (thông tin 1 người dùng, 1 đơn hàng, kết quả trả về từ 1 API...) gần như luôn được biểu diễn dưới dạng dict.

### 6.4. Set — tập hợp không trùng lặp, không thứ tự

```python
mau_sac = {"đỏ", "xanh", "vàng", "đỏ"}   # phần tử trùng tự động bị loại
print(mau_sac)     # {'đỏ', 'xanh', 'vàng'} — chỉ còn 3 phần tử, thứ tự có thể khác lúc khai báo
```

Set dùng khi bạn cần: (1) loại bỏ trùng lặp, hoặc (2) kiểm tra một giá trị có tồn tại trong tập hợp hay không **rất nhanh** — điều này tài liệu senior sẽ giải thích kỹ hơn ở mục 1.3 (liên quan tới khái niệm "độ phức tạp thuật toán"), ở giai đoạn này bạn chỉ cần biết cách tạo và dùng cơ bản:

```python
danh_sach_co_trung = [1, 2, 2, 3, 3, 3]
danh_sach_khong_trung = list(set(danh_sach_co_trung))   # cách nhanh để loại trùng
print(danh_sach_khong_trung)    # [1, 2, 3]
```

### 6.5. Bảng so sánh nhanh 4 cấu trúc

| Cấu trúc | Ký hiệu tạo | Có thứ tự | Sửa được sau khi tạo | Cho phép trùng | Truy cập bằng |
|---|---|---|---|---|---|
| `list` | `[1, 2, 3]` | Có | Có | Có | index (0, 1, 2...) |
| `tuple` | `(1, 2, 3)` | Có | Không | Có | index (0, 1, 2...) |
| `dict` | `{"a": 1}` | Có (thứ tự chèn) | Có | Value được trùng, key thì không | key |
| `set` | `{1, 2, 3}` | Không | Có (thêm/xóa được, nhưng không sửa "tại chỗ" 1 phần tử) | Không | không truy cập theo vị trí, chỉ kiểm tra `in` |

🔨 **Bài tập 6:** Viết file `quan_ly_diem.py`:
1. Tạo một `dict` tên `diem_so` với key là tên 3 sinh viên (chuỗi), value là điểm số (số thực) của họ.
2. Dùng vòng lặp `for` in ra từng sinh viên và điểm số theo dạng: `An: 8.5`.
3. Tính và in ra điểm trung bình cả lớp (gợi ý: dùng `.values()` để lấy hết giá trị, rồi `sum()` và `len()`).
4. Tìm và in ra tên sinh viên có điểm cao nhất.

---

## PHẦN 7: HÀM (FUNCTION) — TÁI SỬ DỤNG CODE

### 7.1. Vì sao cần hàm

Giả sử bạn cần tính diện tích hình chữ nhật ở 5 chỗ khác nhau trong chương trình. Không có hàm, bạn phải chép đi chép lại công thức `dai * rong` 5 lần — nếu sau này công thức cần sửa, phải sửa ở cả 5 chỗ, dễ sót. **Hàm** cho phép bạn gói một đoạn logic lại, đặt tên, rồi **gọi lại** bao nhiêu lần tùy thích.

### 7.2. Định nghĩa hàm với `def`

```python
def tinh_dien_tich(dai, rong):
    dien_tich = dai * rong
    return dien_tich

ket_qua = tinh_dien_tich(5, 3)
print(ket_qua)     # 15

# Gọi lại nhiều lần, tham số khác nhau
print(tinh_dien_tich(10, 2))   # 20
print(tinh_dien_tich(7, 7))    # 49
```

Các thành phần:
- `def` — từ khóa bắt đầu định nghĩa hàm.
- `tinh_dien_tich` — tên hàm (cùng quy tắc đặt tên như biến: `snake_case`, có ý nghĩa).
- `(dai, rong)` — **tham số** (parameter) — những giá trị hàm cần nhận vào để hoạt động.
- `return` — trả kết quả ra ngoài cho nơi gọi hàm. Nếu không có `return`, hàm tự động trả về `None`.
- Khối code bên trong hàm cũng thụt lề 4 dấu cách, giống `if`/`for`.

Hàm **không tự chạy** khi bạn định nghĩa nó — nó chỉ chạy khi được **gọi** (dòng `tinh_dien_tich(5, 3)`).

### 7.3. Tham số mặc định (default argument)

```python
def chao(ten, loi_chao="Xin chào"):
    return f"{loi_chao}, {ten}!"

print(chao("An"))                    # Xin chào, An!  — dùng giá trị mặc định
print(chao("Bình", "Chào buổi sáng")) # Chào buổi sáng, Bình!  — ghi đè giá trị mặc định
```

⚠️ **Lưu ý quan trọng — bạn sẽ gặp lại điều này ngay ở những dòng đầu tiên của tài liệu senior (mục 1.2), nên cần hiểu kỹ ngay bây giờ:** nếu giá trị mặc định là một **list** hoặc **dict** (kiểu dữ liệu "mutable", nhớ lại Phần 6.1), hành vi sẽ rất khác với những gì bạn tưởng:

```python
# Đoạn code này CÓ BUG, dù trông có vẻ hợp lý:
def them_item(item, gio_hang=[]):
    gio_hang.append(item)
    return gio_hang

print(them_item("táo"))    # ['táo']
print(them_item("cam"))    # ['táo', 'cam']  <- SAI! Lẽ ra phải là ['cam'] vì đây là lần gọi mới
```

Lý do (bạn chưa cần hiểu sâu tại sao ngay bây giờ — tài liệu senior sẽ giải thích cặn kẽ): giá trị mặc định chỉ được Python tạo ra **một lần duy nhất**, không phải mỗi lần gọi hàm. Bài học thực dụng ở giai đoạn này: **đừng bao giờ dùng `[]` hoặc `{}` làm giá trị mặc định của tham số.** Nếu cần một list "rỗng" mặc định, viết như sau:

```python
def them_item(item, gio_hang=None):
    if gio_hang is None:
        gio_hang = []
    gio_hang.append(item)
    return gio_hang
```

### 7.4. Biến cục bộ (local) và biến toàn cục (global)

```python
so_lan_goi = 0     # biến TOÀN CỤC — tồn tại ngoài mọi hàm

def dem():
    ket_qua = 1     # biến CỤC BỘ — chỉ tồn tại BÊN TRONG hàm dem(), mất đi khi hàm chạy xong
    return ket_qua

dem()
# print(ket_qua)    # LỖI! NameError — ket_qua không tồn tại ở ngoài hàm
print(so_lan_goi)   # OK, 0 — biến toàn cục truy cập được từ mọi nơi
```

Quy tắc thực dụng cho người mới: **biến tạo bên trong hàm chỉ "sống" bên trong hàm đó.** Muốn dùng giá trị tính được trong hàm ở bên ngoài, phải `return` nó ra rồi gán cho một biến ở ngoài:

```python
def tinh(a, b):
    tong = a + b       # cục bộ
    return tong

ket_qua = tinh(2, 3)   # gán giá trị return vào biến ở ngoài
print(ket_qua)          # 5
```

(Khái niệm này còn sâu hơn — quy tắc LEGB và closure — tài liệu senior sẽ mở rộng ở mục 1.10. Ở đây bạn chỉ cần nắm quy tắc thực dụng trên.)

### 7.5. Docstring — ghi chú hàm dùng để làm gì

```python
def tinh_dien_tich(dai, rong):
    """Tính diện tích hình chữ nhật từ chiều dài và chiều rộng."""
    return dai * rong
```

Chuỗi trong 3 dấu nháy kép ngay dòng đầu tiên bên trong hàm gọi là **docstring** — không bắt buộc, nhưng là thói quen tốt nên có ngay từ đầu: giúp người khác (và chính bạn sau này) hiểu hàm làm gì mà không cần đọc hết code bên trong.

🔨 **Bài tập 7:** Viết file `may_tinh_don_gian.py`:
1. Viết 4 hàm: `cong(a, b)`, `tru(a, b)`, `nhan(a, b)`, `chia(a, b)` — mỗi hàm nhận 2 số, trả về kết quả phép tính tương ứng.
2. Hàm `chia` cần kiểm tra: nếu `b == 0`, trả về chuỗi `"Không thể chia cho 0"` thay vì tính toán.
3. Viết thêm 1 vòng lặp `while` cho phép người dùng nhập liên tục: 2 số và 1 phép tính (`+`, `-`, `*`, `/`), in kết quả, lặp lại cho tới khi người dùng gõ `"thoat"`.

---

## PHẦN 8: XỬ LÝ LỖI CƠ BẢN — KHI CHƯƠNG TRÌNH "NỔ"

### 8.1. Hai loại lỗi: SyntaxError và Exception (runtime error)

**Lỗi cú pháp (SyntaxError):** xảy ra khi code vi phạm quy tắc ngữ pháp Python, Python **không chạy được dù chỉ 1 dòng** — phải sửa hết lỗi cú pháp trước khi chương trình chạy được:

```python
if tuoi >= 18
    print("Đủ tuổi")
# SyntaxError: expected ':'   <- thiếu dấu ':' sau điều kiện if
```

**Lỗi lúc chạy (Exception/runtime error):** cú pháp đúng, chương trình bắt đầu chạy, nhưng gặp tình huống không xử lý được giữa chừng thì dừng lại:

```python
so = int("hai mươi lăm")
# ValueError: invalid literal for int() with base 10: 'hai mươi lăm'
```

### 8.2. Đọc traceback — kỹ năng sống còn

Khi có lỗi, Python in ra một khối gọi là **traceback**, trông đáng sợ nhưng thực ra rất có cấu trúc. Ví dụ:

```
Traceback (most recent call last):
  File "chuong_trinh.py", line 5, in <module>
    ket_qua = 10 / so
              ~~~^~~~
ZeroDivisionError: division by zero
```

Cách đọc: **luôn đọc dòng CUỐI CÙNG trước tiên** — đó là tên loại lỗi (`ZeroDivisionError`) và mô tả ngắn gọn (`division by zero` — chia cho 0). Sau đó nhìn phần `line 5` để biết chính xác dòng nào trong file gây lỗi. Người mới thường hoảng và đọc lướt toàn bộ khối chữ đỏ — thói quen đúng là: **đọc dòng cuối trước, tìm số dòng lỗi, rồi mới quay lại đọc chi tiết nếu cần.**

### 8.3. Các lỗi (Exception) thường gặp nhất

| Tên lỗi | Xảy ra khi nào | Ví dụ |
|---|---|---|
| `NameError` | Dùng biến chưa được định nghĩa | `print(x)` khi chưa từng có `x = ...` |
| `TypeError` | Thao tác sai kiểu dữ liệu | `"5" + 5` (không cộng được str với int) |
| `ValueError` | Đúng kiểu nhưng giá trị không hợp lệ | `int("hai mươi")` |
| `IndexError` | Truy cập index không tồn tại trong list/chuỗi | `[1,2,3][10]` |
| `KeyError` | Truy cập key không tồn tại trong dict | `{"a":1}["b"]` |
| `ZeroDivisionError` | Chia cho 0 | `10 / 0` |

### 8.4. `try / except` — bắt lỗi để chương trình không "chết"

Nếu không xử lý, một Exception sẽ làm chương trình **dừng đột ngột**. `try/except` cho phép bạn "đón" lỗi và quyết định làm gì tiếp, thay vì để chương trình sập:

```python
try:
    so = int(input("Nhập một số: "))
    print(f"Số bạn nhập gấp đôi là: {so * 2}")
except ValueError:
    print("Bạn phải nhập một số hợp lệ!")
```

Cách hoạt động: Python chạy khối `try` trước; nếu **không** có lỗi, khối `except` bị bỏ qua hoàn toàn; nếu **có** lỗi đúng loại đã khai báo (ở đây là `ValueError`), Python nhảy ngay vào khối `except` thay vì làm chương trình sập.

Có thể bắt nhiều loại lỗi khác nhau:

```python
try:
    a = int(input("Nhập số thứ nhất: "))
    b = int(input("Nhập số thứ hai: "))
    print(a / b)
except ValueError:
    print("Phải nhập số nguyên hợp lệ")
except ZeroDivisionError:
    print("Không thể chia cho 0")
```

`finally` — khối luôn chạy dù có lỗi hay không, thường dùng để "dọn dẹp" (ví dụ đóng file — sẽ thấy rõ hơn ở Phần 9):

```python
try:
    so = int(input("Nhập số: "))
except ValueError:
    print("Không hợp lệ")
finally:
    print("Đã kết thúc lần thử nhập")   # luôn chạy, dù try thành công hay lỗi
```

> ⚠️ **Thói quen cần tránh ngay từ đầu:** đừng viết `except:` trống (bắt "mọi lỗi" mà không nói rõ loại nào) hoặc `except Exception: pass` (bắt lỗi rồi lờ đi, không làm gì). Cách này che giấu cả những lỗi bạn không lường trước, khiến chương trình chạy sai âm thầm mà không biết. Tài liệu senior (mục 1.8) gọi đây là một trong những "code smell" tệ nhất — nên tập thói quen đúng ngay từ bây giờ: **chỉ bắt loại lỗi bạn thực sự dự đoán được và biết cách xử lý.**

🔨 **Bài tập 8:** Sửa lại file `may_tinh_don_gian.py` ở bài tập 7:
1. Bọc phần nhập số bằng `try/except` để bắt `ValueError` khi người dùng gõ không phải số — in thông báo lỗi thân thiện thay vì để chương trình sập.
2. Test thử: chạy chương trình, cố tình gõ chữ thay vì số, xác nhận chương trình vẫn tiếp tục chạy chứ không dừng đột ngột.

---

## PHẦN 9: LÀM VIỆC VỚI FILE

### 9.1. `open()`, đọc và ghi file

Để làm việc với 1 file trên máy (đọc nội dung, hoặc ghi dữ liệu ra), dùng hàm `open()`:

```python
f = open("ghi_chu.txt", "w")   # "w" = write (ghi) — nếu file chưa có, tự tạo mới; nếu đã có, XÓA nội dung cũ
f.write("Xin chào\n")
f.write("Dòng thứ hai\n")
f.close()      # QUAN TRỌNG: phải đóng file sau khi dùng xong
```

Đọc lại file:

```python
f = open("ghi_chu.txt", "r")   # "r" = read (đọc) — mặc định nếu không ghi rõ mode
noi_dung = f.read()
print(noi_dung)
f.close()
```

Các **mode** thường dùng khi mở file:

| Mode | Ý nghĩa |
|---|---|
| `"r"` | Đọc (read) — file phải đã tồn tại |
| `"w"` | Ghi (write) — tạo mới, hoặc **xóa sạch** nội dung cũ nếu file đã có |
| `"a"` | Ghi nối tiếp (append) — thêm vào cuối file, không xóa nội dung cũ |

### 9.2. `with` — cách chuẩn để làm việc với file

Vấn đề của cách `open()`/`close()` thủ công ở trên: nếu có lỗi xảy ra **giữa** lúc mở và lúc đóng file, dòng `f.close()` có thể không bao giờ được chạy tới, khiến file bị "treo" ở trạng thái mở. Cách chuẩn, luôn nên dùng ngay từ đầu, là câu lệnh `with`:

```python
with open("ghi_chu.txt", "r") as f:
    noi_dung = f.read()
    print(noi_dung)
# Ra khỏi khối with, file TỰ ĐỘNG được đóng — kể cả khi có lỗi xảy ra bên trong khối with
```

Từ giờ, **luôn dùng `with open(...) as f:`** thay vì gọi `open()`/`close()` riêng lẻ — đây cũng là quy ước tài liệu senior sẽ nhấn mạnh lại ở mục 3.3 khi nói về khái niệm rộng hơn gọi là "context manager".

**Đọc file theo từng dòng** (hữu ích khi file lớn, không muốn load hết vào bộ nhớ cùng lúc):

```python
with open("ghi_chu.txt", "r") as f:
    for dong in f:
        print(dong.strip())     # .strip() để bỏ ký tự xuống dòng thừa ở cuối mỗi dòng
```

### 9.3. Sơ lược về file CSV

CSV (Comma-Separated Values) là định dạng file văn bản phổ biến để lưu dữ liệu dạng bảng (giống Excel nhưng đơn giản hơn), mỗi dòng là 1 bản ghi, các giá trị cách nhau bằng dấu phẩy:

```
ten,tuoi,diem
An,20,8.5
Binh,21,7.0
```

Có thể đọc thủ công bằng cách kết hợp kiến thức đã học (đọc từng dòng + `.split(",")`):

```python
with open("sinh_vien.csv", "r") as f:
    dong_dau = True
    for dong in f:
        if dong_dau:            # bỏ qua dòng tiêu đề đầu tiên
            dong_dau = False
            continue
        ten, tuoi, diem = dong.strip().split(",")
        print(f"{ten} - {tuoi} tuổi - điểm {diem}")
```

Python có sẵn module `csv` chuyên dụng làm việc này gọn hơn nhiều — bạn sẽ gặp lại nó khi thực hành Giai đoạn 1 của tài liệu senior (chương trình quản lý chi tiêu cá nhân). Ở đây chỉ cần hiểu nguyên lý cơ bản.

🔨 **Bài tập 9:** Viết file `nhat_ky.py`:
1. Cho phép người dùng nhập một dòng nhật ký (`input()`), rồi ghi (ở chế độ **append**, không xóa nội dung cũ) dòng đó vào file `nhat_ky.txt`, kèm số thứ tự.
2. Sau khi ghi, đọc lại toàn bộ file và in ra màn hình tất cả các dòng đã lưu (kể cả những lần chạy chương trình trước đó).
3. Chạy chương trình 3 lần, xác nhận nội dung được cộng dồn qua mỗi lần chạy chứ không bị mất.

---

## PHẦN 10: MODULE VÀ THƯ VIỆN

### 10.1. Module là gì

Cho tới giờ, mọi hàm bạn dùng (`print`, `len`, `int`...) đều có sẵn không cần khai báo gì thêm — đó gọi là **built-in function**. Nhưng Python còn đi kèm rất nhiều chức năng khác **không tự động có sẵn**, phải "gọi" ra bằng `import` trước khi dùng được. Một **module** là một file `.py` chứa sẵn các hàm/class hữu ích, được đóng gói lại để tái sử dụng — có thể do chính Python cung cấp (gọi là **standard library** — thư viện chuẩn, luôn có sẵn khi cài Python) hoặc do người khác viết và bạn cài thêm.

### 10.2. Cách `import`

```python
import math

print(math.sqrt(16))     # 4.0  — căn bậc 2
print(math.pi)             # 3.141592653589793
print(math.ceil(4.2))      # 5   — làm tròn lên
print(math.floor(4.8))     # 4   — làm tròn xuống
```

Cú pháp `import ten_module` rồi gọi hàm bằng `ten_module.ten_ham(...)`.

Có thể import riêng lẻ 1 hàm/giá trị cụ thể để gọi ngắn gọn hơn, không cần viết `math.` phía trước:

```python
from math import sqrt, pi

print(sqrt(16))    # 4.0
print(pi)           # 3.141592653589793
```

Đặt tên khác (alias) khi tên module dài hoặc để tránh trùng tên:

```python
import math as m
print(m.sqrt(16))
```

⚠️ Tránh dùng `from module import *` (import tất cả) — cách này khiến bạn không biết một hàm đến từ module nào, dễ gây trùng tên. Tài liệu senior (mục 1.11) sẽ nhắc lại quy tắc này. Từ đầu, hãy tập thói quen `import module` rồi gọi rõ ràng `module.ham(...)`, hoặc `from module import ten_cu_the` khi chỉ cần 1-2 thứ cụ thể.

### 10.3. Vài module thư viện chuẩn hay dùng

```python
import random
print(random.randint(1, 10))        # số nguyên ngẫu nhiên từ 1 đến 10 (bao gồm cả 2 đầu)
danh_sach = [1, 2, 3, 4, 5]
print(random.choice(danh_sach))     # chọn ngẫu nhiên 1 phần tử trong list
random.shuffle(danh_sach)            # xáo trộn list TẠI CHỖ

import datetime
hom_nay = datetime.date.today()
print(hom_nay)                        # ví dụ: 2026-07-10
```

### 10.4. `pip` — cài thư viện bên ngoài standard library

Standard library rất phong phú nhưng không có tất cả mọi thứ — ví dụ muốn gọi API qua Internet cần thư viện `requests`, thư viện này **không có sẵn**, phải cài thêm bằng công cụ tên **pip** (đi kèm sẵn khi bạn cài Python):

```bash
pip install requests
```

Sau khi cài, `import requests` dùng được bình thường như module chuẩn.

> 💡 Đây chỉ là giới thiệu khái niệm ở mức tối thiểu để bạn không bỡ ngỡ khi thấy lệnh `pip install` trong tài liệu senior. Tài liệu đó (mục 1.12) sẽ dạy bạn một khái niệm quan trọng hơn đi kèm với `pip`: **virtual environment (môi trường ảo)** — vì sao không nên `pip install` trực tiếp vào Python "hệ thống". Ở giai đoạn mới bắt đầu này, bạn chưa cần dùng `pip` ngay; cứ tập trung làm chủ syntax cơ bản trước.

🔨 **Bài tập 10:** Viết file `doan_so.py` — trò chơi đoán số đơn giản, kết hợp toàn bộ kiến thức từ Phần 4 đến Phần 10:
1. Dùng `random.randint(1, 100)` để máy tự chọn 1 số bí mật từ 1-100.
2. Dùng vòng lặp `while` cho người chơi đoán liên tục.
3. Mỗi lần đoán, dùng `try/except` để bắt lỗi nếu người dùng gõ không phải số.
4. So sánh số đoán với số bí mật: in `"Quá cao"`, `"Quá thấp"`, hoặc `"Chính xác!"` rồi dừng vòng lặp (`break`).
5. Đếm và in ra tổng số lần đoán khi người chơi thắng.

---

## PHẦN 11: LẬP TRÌNH HƯỚNG ĐỐI TƯỢNG (OOP) CƠ BẢN

### 11.1. Vì sao cần OOP

Hãy tưởng tượng bạn cần quản lý thông tin nhiều tài khoản ngân hàng: mỗi tài khoản có chủ sở hữu, số dư, và các hành động như nạp tiền, rút tiền. Dùng những gì học tới giờ, bạn có thể làm bằng nhiều biến/dict riêng lẻ, nhưng sẽ rất lộn xộn khi số lượng tài khoản tăng lên. **Lập trình hướng đối tượng (OOP)** cho phép bạn gom **dữ liệu** (số dư, chủ sở hữu) và **hành vi** (nạp tiền, rút tiền) hoạt động trên dữ liệu đó lại thành **một khối** gọi là **class**.

### 11.2. `class` và `object` là gì

**Class** giống một "bản thiết kế" (khuôn mẫu); **object** (hay còn gọi là **instance**) là một "sản phẩm cụ thể" được tạo ra từ bản thiết kế đó. Ví dụ: `class Cho` (Dog) là bản thiết kế mô tả "một con chó nói chung"; `con_cho_cua_toi = Cho()` là một object cụ thể — một con chó thật, khác với con chó của người khác dù cùng là "chó".

```python
class TaiKhoan:
    def __init__(self, chu_so_huu, so_du):
        self.chu_so_huu = chu_so_huu
        self.so_du = so_du

    def nap_tien(self, so_tien):
        self.so_du += so_tien

    def rut_tien(self, so_tien):
        if so_tien > self.so_du:
            print("Số dư không đủ")
        else:
            self.so_du -= so_tien

# Tạo 2 object (instance) khác nhau từ cùng 1 class
tk_an = TaiKhoan("An", 1000000)
tk_binh = TaiKhoan("Bình", 500000)

tk_an.nap_tien(200000)
print(tk_an.so_du)      # 1200000
print(tk_binh.so_du)    # 500000 — hoàn toàn độc lập với tk_an
```

### 11.3. `__init__` và `self`

`__init__` là một **method đặc biệt**, tự động chạy **ngay khi bạn tạo object mới** (dòng `TaiKhoan("An", 1000000)`) — dùng để thiết lập dữ liệu ban đầu cho object đó. Tên gọi khác của nó là "constructor" (hàm khởi tạo).

`self` là tham số đầu tiên của **mọi method** trong class, đại diện cho **chính object đang được thao tác**. Khi bạn gọi `tk_an.nap_tien(200000)`, Python tự động truyền `tk_an` vào làm `self` — bạn không cần (và không nên) tự truyền tay tham số này.

```python
class TaiKhoan:
    def __init__(self, chu_so_huu, so_du):
        # self.chu_so_huu nghĩa là: "gắn thuộc tính chu_so_huu VÀO object này"
        self.chu_so_huu = chu_so_huu
        self.so_du = so_du
```

Nếu chưa quen, hãy hình dung: `self.so_du = so_du` giống việc dán nhãn "so_du" lên một ngăn kéo *thuộc riêng về object này*, khác với ngăn kéo "so_du" của object khác dù cùng class.

`self.chu_so_huu` và `self.so_du` gọi là **attribute** (thuộc tính) — dữ liệu gắn liền với object. `nap_tien` và `rut_tien` gọi là **method** — hành vi (hàm) gắn liền với object, luôn nhận `self` làm tham số đầu tiên để biết đang thao tác trên object nào.

### 11.4. Truy cập và thay đổi attribute

```python
print(tk_an.chu_so_huu)    # An      — đọc attribute bằng dấu chấm
tk_an.chu_so_huu = "An Nguyễn"   # sửa attribute trực tiếp (dùng cẩn thận — tài liệu senior mục 2.4
                                    # sẽ dạy cách kiểm soát việc này an toàn hơn bằng @property)
```

### 11.5. Kế thừa (inheritance) cơ bản

Kế thừa cho phép một class **mới** tái sử dụng attribute/method của một class **đã có**, rồi thêm/sửa những gì riêng của nó — tránh chép lại code giống nhau.

```python
class TaiKhoan:
    def __init__(self, chu_so_huu, so_du):
        self.chu_so_huu = chu_so_huu
        self.so_du = so_du

    def nap_tien(self, so_tien):
        self.so_du += so_tien

    def thong_tin(self):
        return f"{self.chu_so_huu}: {self.so_du} VNĐ"


class TaiKhoanTietKiem(TaiKhoan):     # kế thừa từ TaiKhoan — trong ngoặc là "class cha"
    def __init__(self, chu_so_huu, so_du, lai_suat):
        super().__init__(chu_so_huu, so_du)   # gọi __init__ của class cha để không phải viết lại
        self.lai_suat = lai_suat               # thêm attribute RIÊNG của class con

    def tinh_lai(self):
        return self.so_du * self.lai_suat


tk = TaiKhoanTietKiem("Chi", 10000000, 0.05)
tk.nap_tien(500000)             # dùng LẠI method của class cha, không cần viết lại
print(tk.thong_tin())            # dùng LẠI method của class cha
print(tk.tinh_lai())             # 525000.0 — method RIÊNG của class con
```

`class TaiKhoanTietKiem(TaiKhoan):` nghĩa là "TaiKhoanTietKiem **kế thừa** từ TaiKhoan" — mọi attribute và method của `TaiKhoan` đều tự động có sẵn trong `TaiKhoanTietKiem`, không cần viết lại. `super().__init__(...)` gọi tới `__init__` của class cha để tái sử dụng logic khởi tạo đã có, thay vì chép lại 2 dòng `self.chu_so_huu = ...` / `self.so_du = ...`.

> 💡 Đây chỉ là kế thừa ở mức cơ bản nhất. Tài liệu senior (mục 2.2, 2.3, 2.6) sẽ đi sâu hơn nhiều: dunder method khác ngoài `__init__`, khi nào nên dùng kế thừa và khi nào nên dùng **composition** (một cách tổ chức khác, thường được ưu tiên hơn), abstract base class... Ở đây bạn chỉ cần nắm được **class/object/`__init__`/`self`/method/kế thừa cơ bản là gì** để đọc hiểu cú pháp — phần *tại sao chọn cách này thay vì cách kia* nằm ở tài liệu senior.

🔨 **Bài tập 11:** Viết file `quan_ly_thu_vien.py`:
1. Viết class `Sach` với `__init__` nhận `ten_sach`, `tac_gia`, và attribute `da_muon` mặc định là `False`.
2. Viết method `muon()` — nếu `da_muon` đang là `False`, đổi thành `True` và in `"Đã mượn sách"`; nếu đã `True` rồi, in `"Sách đã có người mượn"`.
3. Viết method `tra()` — đổi `da_muon` về `False`, in `"Đã trả sách"`.
4. Tạo 3 object `Sach` khác nhau, thử gọi `muon()` và `tra()`, in `__dict__` của từng object (gợi ý: `print(sach1.__dict__)` cho bạn xem toàn bộ attribute hiện tại của object dưới dạng dict) để xác nhận mỗi object độc lập với nhau.

---

## PHẦN 12: BA DỰ ÁN NHỎ TỔNG HỢP

Đọc lý thuyết xong mà không tự ráp lại thành một chương trình hoàn chỉnh thì kiến thức sẽ rời rạc. Ba dự án dưới đây **cố tình** buộc bạn dùng lại gần như mọi phần đã học. Làm theo thứ tự, đừng nhìn đáp án (không có đáp án đính kèm — đây là bài tập tự luyện thật sự).

### Dự án 1 — Quản lý danh sách việc cần làm (To-do list CLI)

Yêu cầu:
1. Chương trình chạy trong một vòng lặp `while` liên tục, hiển thị menu: `1. Thêm việc`, `2. Xem danh sách`, `3. Đánh dấu hoàn thành`, `4. Xóa việc`, `5. Thoát`.
2. Dữ liệu lưu trong một `list` chứa các `dict`, mỗi dict có dạng `{"noi_dung": "...", "xong": False}`.
3. Người dùng nhập số (1-5) để chọn hành động, dùng `try/except` bắt lỗi nếu nhập không phải số.
4. Khi "Xem danh sách", in từng việc kèm số thứ tự và trạng thái (`[x]` nếu xong, `[ ]` nếu chưa).
5. Khi thoát chương trình (chọn 5), ghi toàn bộ danh sách ra file `todo.txt` (mỗi dòng 1 việc), dùng `with open(...)`.
6. Khi chương trình khởi động lại, đọc file `todo.txt` nếu đã tồn tại để khôi phục danh sách cũ (gợi ý: cần `try/except` bắt `FileNotFoundError` cho lần chạy đầu tiên khi file chưa tồn tại).

*Kỹ năng được luyện: vòng lặp, dict, list, hàm, try/except, file I/O.*

### Dự án 2 — Quản lý điểm sinh viên (dùng class)

Yêu cầu:
1. Viết class `SinhVien` có `__init__` nhận `ten` và một `list` điểm số rỗng ban đầu.
2. Method `them_diem(diem)` — thêm 1 điểm vào list điểm của sinh viên đó.
3. Method `diem_trung_binh()` — trả về điểm trung bình (trả về `0` nếu chưa có điểm nào, tránh lỗi chia cho 0).
4. Method `xep_loai()` — dựa trên điểm trung bình, trả về chuỗi xếp loại (tái sử dụng logic if/elif từ Bài tập 4).
5. Viết một `list` chứa nhiều object `SinhVien`, nhập dữ liệu mẫu ít nhất 3 sinh viên, mỗi người 2-3 điểm.
6. Duyệt qua list, in ra bảng: tên, điểm trung bình, xếp loại — dùng f-string căn chỉnh đẹp (gợi ý tìm hiểu thêm: `f"{ten:<10}"` để căn trái, chiếm 10 ký tự).
7. Tìm và in ra sinh viên có điểm trung bình cao nhất.

*Kỹ năng được luyện: class, method, list, vòng lặp, xử lý biên (chia cho 0), f-string nâng cao.*

### Dự án 3 — Trò chơi đoán từ (Hangman đơn giản, dạng text)

Yêu cầu:
1. Chương trình chọn ngẫu nhiên 1 từ trong một `list` các từ có sẵn (ví dụ: `["python", "lambda", "class", "vòng lặp"]`), dùng `random.choice()`.
2. Người chơi đoán từng **ký tự** một, trong vòng lặp `while`, tối đa 6 lần đoán sai.
3. Dùng `set` để lưu các ký tự đã đoán đúng, hiển thị từ dưới dạng `_ _ t _ _ n` (ký tự chưa đoán ra thay bằng `_`).
4. Nếu đoán sai, giảm số lượt còn lại; nếu hết lượt, in `"Bạn đã thua! Từ đúng là: ..."`.
5. Nếu đoán đủ hết ký tự, in `"Chúc mừng, bạn đã thắng!"`.
6. Bọc phần input trong `try/except` để chương trình không sập nếu người dùng nhập rỗng hoặc nhiều hơn 1 ký tự.

*Kỹ năng được luyện: string (index, so sánh ký tự), set, list, vòng lặp có điều kiện dừng phức tạp, random, try/except.*

> Nếu bạn hoàn thành cả 3 dự án mà không phải quay lại đọc lý thuyết quá nhiều lần — bạn đã sẵn sàng cho tài liệu senior.

---

## PHẦN 13: BẢN ĐỒ NỐI SANG TÀI LIỆU SENIOR

### 13.1. Đối chiếu: bạn vừa học gì → tài liệu senior dùng nó ở đâu

Bảng dưới đây giúp bạn thấy rõ mỗi phần vừa học chuẩn bị cho phần nào trong `huong-dan-python-senior.md`, để khi đọc tới đó bạn nhận ra ngay "à, cái này mình đã biết nền tảng rồi, giờ học phần *tại sao* và *khi nào nên dùng*":

| Bạn vừa học (tài liệu này) | Chuẩn bị cho (tài liệu senior) |
|---|---|
| Phần 2 — biến, kiểu dữ liệu, `list`/`dict` sơ lược | Mục 1.2, 1.3 — mutable/immutable, chọn cấu trúc dữ liệu theo độ phức tạp |
| Phần 6.1 — list và hiện tượng "2 biến cùng trỏ 1 list" | Mục 1.2 — giải thích sâu vì sao, và các trường hợp bug liên quan |
| Phần 5 — vòng lặp `for` cơ bản | Mục 1.4, 1.5 — comprehension, `enumerate`/`zip`/`itertools` (viết lại vòng lặp "chuẩn Python" hơn) |
| Phần 3.4 — f-string cơ bản | Mục 1.6 — f-string nâng cao, mẹo debug `f"{bien=}"` |
| Phần 4 — if/else, so sánh | Mục 1.7 — truthy/falsy, viết điều kiện ngắn gọn kiểu Python |
| Phần 8 — try/except cơ bản | Mục 1.8 — triết lý EAFP vs LBYL, custom exception |
| Phần 7 — hàm, tham số mặc định | Mục 1.9 — `*args`/`**kwargs`, hàm là "công dân hạng nhất", lambda |
| Phần 7.4 — biến cục bộ/toàn cục | Mục 1.10 — LEGB đầy đủ, closure, bẫy late binding |
| Phần 10 — `import`, module | Mục 1.11, 1.12 — cấu trúc project, virtual environment |
| Phần 11 — class, `__init__`, `self`, kế thừa | Toàn bộ PHẦN 2 của tài liệu senior — dunder method, composition, `@property`, `@dataclass`, SOLID |
| Phần 9 — file, `with` | Mục 3.3 — khái niệm tổng quát "context manager" (file chỉ là 1 ví dụ) |
| — (khái niệm mới hoàn toàn) | PHẦN 3 senior — generator, decorator: đây là kỹ thuật *nâng cao hơn* những gì tài liệu này dạy, cứ đọc tuần tự, sẽ hiểu được vì bạn đã nắm chắc hàm và vòng lặp |

### 13.2. Checklist tự kiểm tra trước khi chuyển sang tài liệu senior

Đánh dấu được hết các mục sau, bạn đã sẵn sàng:

- [ ] Tự chạy được 1 file `.py` từ terminal mà không cần tra cứu lại
- [ ] Phân biệt được `=` (gán) và `==` (so sánh) mà không cần suy nghĩ
- [ ] Đọc hiểu và tự viết được `if/elif/else` nhiều nhánh
- [ ] Viết được `for` với `range()`, biết khi nào dùng `for` khi nào dùng `while`
- [ ] Phân biệt được `list`, `tuple`, `dict`, `set` — biết cái nào dùng khi nào ở mức cơ bản
- [ ] Tự viết được 1 hàm có tham số, có `return`, có giá trị mặc định
- [ ] Biết `try/except` bắt lỗi cụ thể, không viết `except:` trống
- [ ] Đọc được traceback, biết tìm số dòng lỗi và tên loại lỗi
- [ ] Dùng được `with open(...)` để đọc/ghi file
- [ ] Tự viết được 1 class đơn giản với `__init__`, `self`, ít nhất 1 method, hiểu vì sao cần `self`
- [ ] Đã hoàn thành ít nhất 2/3 dự án ở Phần 12 mà không phải mở lại lý thuyết liên tục

Nếu còn mục nào chưa chắc — không sao cả, quay lại phần tương ứng, làm lại bài tập 🔨 của phần đó, rồi tiếp tục. Không cần thuộc lòng mọi cú pháp; điều quan trọng là **quen tay** và **biết tra cứu đúng chỗ khi quên**.

### 13.3. Bước tiếp theo

Mở lại file `huong-dan-python-senior.md`, bắt đầu đọc từ **"Cách dùng tài liệu này"** rồi vào thẳng **PHẦN 1: TƯ DUY PYTHONIC**. Mọi cú pháp trong đó (list comprehension, EAFP, `*args`, dunder method...) giờ sẽ không còn xa lạ về mặt hình thức — tài liệu đó sẽ dạy bạn **tại sao** và **khi nào** nên viết theo cách này thay vì cách kia, điều mà tài liệu hiện tại (dạy *cú pháp*) chưa đề cập tới.

Chúc bạn học tốt — và như tài liệu senior sẽ nhắc lại ở cuối: đọc xong không biến bạn thành lập trình viên giỏi, chỉ có gõ code thật, sai thật, tự sửa thật mới làm được điều đó. Giờ thì mở VS Code lên và bắt đầu Dự án 1 thôi.
