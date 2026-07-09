# Từ Python Yếu Đến Senior: Hướng Dẫn Toàn Diện

> **Dành cho ai:** Bạn đã biết lập trình (biết biến, vòng lặp, hàm là gì, đã từng code C/Java/PHP/JS...), nhưng Python thì vẫn còn non — viết code "chạy được" chứ chưa "chuẩn", chưa biết vì sao senior lại viết khác mình.
>
> **Mục tiêu:** Sau khi đọc và **thực hành theo** (không chỉ đọc suông), bạn sẽ hiểu *tại sao* Python được viết theo cách nó được viết, và có đủ trực giác kỹ thuật để tự ra quyết định như một senior — thay vì chỉ copy pattern.

---

## Cách dùng tài liệu này (đọc phần này trước, đừng bỏ qua)

Ba nguyên tắc:

1. **Đừng đọc lướt code mẫu — gõ lại tay.** Não người học vận động (gõ, gõ sai, sửa lỗi) chứ không học qua đọc mắt. Mỗi phần đều có bài tập nhỏ (🔨), hãy làm trước khi đọc tiếp.
2. **Senior không phải người biết nhiều cú pháp hơn — là người biết *khi nào dùng cái gì và tại sao*.** Vì vậy tài liệu này với mỗi kỹ thuật đều giải thích: dùng để làm gì, khi nào NÊN dùng, khi nào KHÔNG nên.
3. **Đọc một lượt sẽ không biến bạn thành senior.** Senior là kết quả của việc *lặp lại* quyết định đúng hàng trăm lần cho tới khi nó thành phản xạ. Tài liệu này cho bạn bản đồ và phản xạ ban đầu; quãng đường còn lại là số giờ bạn code thật.

Tài liệu chia làm 10 phần, đọc theo thứ tự vì phần sau dựa vào phần trước:

0. (Bạn đang ở đây) Cách dùng tài liệu
1. Tư duy Pythonic — nền tảng đúng chuẩn
2. OOP kiểu Python
3. Kỹ thuật nâng cao: generator, decorator, context manager
4. Kiến trúc & Clean Code
5. Testing & Debugging chuyên nghiệp
6. Performance & Concurrency
7. Quy trình làm việc chuyên nghiệp (Git, tooling, CI/CD, bảo mật)
8. Tư duy giải quyết vấn đề như Senior
9. Lộ trình luyện tập thực chiến
10. Checklist Senior & tài nguyên học tiếp

---

## PHẦN 1: TƯ DUY PYTHONIC — NỀN TẢNG ĐÚNG CHUẨN

### 1.1. "Pythonic" nghĩa là gì?

Mọi ngôn ngữ đều có "giọng văn" riêng. Code Java viết trong Python vẫn chạy được, nhưng người khác đọc vào sẽ biết ngay bạn "dịch" từ ngôn ngữ khác. Ví dụ kinh điển:

```python
# Không Pythonic (tư duy Java/C)
i = 0
result = []
while i < len(numbers):
    if numbers[i] % 2 == 0:
        result.append(numbers[i] * 2)
    i += 1

# Pythonic
result = [n * 2 for n in numbers if n % 2 == 0]
```

Cả hai đều ra cùng kết quả. Nhưng bản Pythonic:
- Ít chỗ để tạo bug (không có `i`, không có lỗi off-by-one)
- Đọc gần như tiếng Anh: "n nhân 2, cho mỗi n trong numbers, nếu n chia hết cho 2"
- Nhanh hơn vì list comprehension được tối ưu ở tầng C

**Nguyên tắc cốt lõi:** Python có một "cách làm hiển nhiên" (obvious way) cho phần lớn tác vụ phổ biến. Gõ `import this` vào Python để đọc "Zen of Python" — 19 câu triết lý thiết kế ngôn ngữ này. Hai câu quan trọng nhất với người mới:
- "There should be one — and preferably only one — obvious way to do it."
- "Readability counts."

🔨 **Bài tập:** Mở terminal, gõ `python3 -c "import this"`, đọc hết 19 dòng đó một lần.

### 1.2. Biến và kiểu dữ liệu: hiểu đúng bản chất

Python là **dynamically typed** (kiểu được xác định lúc chạy) nhưng **strongly typed** (không tự ý ép kiểu ngầm nguy hiểm như JS). Khác biệt lớn nhất so với C/Java: **biến trong Python chỉ là cái tên trỏ tới object**, không phải "hộp chứa giá trị".

```python
a = [1, 2, 3]
b = a          # b trỏ tới CÙNG object với a, không phải bản copy
b.append(4)
print(a)       # [1, 2, 3, 4]  <- a cũng bị thay đổi!
```

Đây là nguồn gốc của rất nhiều bug người mới gặp phải. Để hiểu rõ, bạn cần phân biệt **mutable** (có thể thay đổi tại chỗ) và **immutable** (không thể):

| Immutable | Mutable |
|---|---|
| `int`, `float`, `str`, `tuple`, `frozenset`, `bool` | `list`, `dict`, `set`, hầu hết custom class |

```python
# Immutable: "thay đổi" thực ra là tạo object mới
s = "hello"
s2 = s
s += " world"   # tạo string MỚI, gán lại cho s
print(s2)       # vẫn là "hello", không đổi

# Mutable: thay đổi tại chỗ ảnh hưởng mọi tham chiếu
lst = [1, 2]
lst2 = lst
lst.append(3)
print(lst2)     # [1, 2, 3] — bị ảnh hưởng
```

**Bẫy kinh điển #1 — mutable default argument:**

```python
# SAI — bug ẩn rất khó phát hiện
def add_item(item, basket=[]):
    basket.append(item)
    return basket

add_item("táo")     # ['táo']
add_item("cam")     # ['táo', 'cam']  <- lẽ ra phải là ['cam']!
```

Lý do: giá trị mặc định `[]` chỉ được tạo **một lần duy nhất** khi hàm được định nghĩa, không phải mỗi lần gọi. Mọi lần gọi hàm mà không truyền `basket` đều dùng chung một list đó.

```python
# ĐÚNG
def add_item(item, basket=None):
    if basket is None:
        basket = []
    basket.append(item)
    return basket
```

Đây là một trong những dấu hiệu rõ nhất phân biệt code junior và senior: senior nhìn thấy `def f(x, lst=[])` là lập tức nghi ngờ.

### 1.3. Cấu trúc dữ liệu: chọn đúng, không phải chọn quen

Senior không dùng `list` cho mọi thứ. Mỗi cấu trúc có độ phức tạp và ngữ nghĩa riêng:

| Cấu trúc | Khi nào dùng | Tra cứu theo index/key | Kiểm tra tồn tại (`in`) | Cho phép trùng | Có thứ tự |
|---|---|---|---|---|---|
| `list` | Dãy có thứ tự, hay thay đổi | O(1) theo index | O(n) — chậm với list lớn | Có | Có |
| `tuple` | Dữ liệu cố định, nhóm giá trị (như 1 "record") | O(1) | O(n) | Có | Có |
| `dict` | Ánh xạ key→value, tra cứu nhanh | O(1) theo key | O(1) theo key | Value có thể trùng | Có (từ Python 3.7+, giữ thứ tự chèn) |
| `set` | Tập hợp duy nhất, phép toán tập hợp | Không áp dụng | O(1) | Không | Không |

Ví dụ thực tế cho thấy tầm quan trọng:

```python
# Junior: kiểm tra tồn tại bằng list -> O(n) mỗi lần check
allowed_users = ["an", "binh", "chi", ...]  # 10,000 phần tử
if username in allowed_users:   # chậm dần khi list càng lớn
    ...

# Senior: dùng set -> O(1) bất kể tập hợp lớn cỡ nào
allowed_users = {"an", "binh", "chi", ...}
if username in allowed_users:   # nhanh, không phụ thuộc kích thước
    ...
```

Đây không phải tiểu tiết — khi tập dữ liệu lớn lên (production scale), sự khác biệt là giữa "chạy tức thì" và "server đơ".

**Tuple vs List — đừng chỉ nghĩ "tuple là list không đổi được".** Ý nghĩa thật sự: tuple diễn tả một **cấu trúc cố định** (như một record/struct), list diễn tả một **chuỗi đồng nhất, có thể tăng giảm**.

```python
# Đúng ngữ nghĩa: tọa độ luôn có đúng 2 phần tử, không đổi cấu trúc
point = (10, 20)

# Đúng ngữ nghĩa: danh sách người dùng, số lượng thay đổi liên tục
users = ["An", "Bình", "Chi"]
```

### 1.4. Comprehensions — không chỉ để "ngắn gọn"

List/dict/set comprehension tồn tại vì chúng diễn tả rõ **ý định** (intent): "tạo ra một tập hợp mới bằng cách biến đổi/lọc tập hợp cũ" — khác với vòng lặp thủ công vốn không nói lên ý định gì cho tới khi đọc hết thân vòng lặp.

```python
# List comprehension
squares = [x**2 for x in range(10)]

# Có điều kiện lọc
evens = [x for x in range(20) if x % 2 == 0]

# Dict comprehension
name_lengths = {name: len(name) for name in ["An", "Bình", "Chi"]}

# Set comprehension
unique_domains = {email.split("@")[1] for email in emails}
```

**Quy tắc senior tự đặt ra:** nếu comprehension dài quá 1 dòng hoặc lồng quá 2 tầng, đổi lại thành vòng lặp thường + hàm riêng. Comprehension khó đọc còn tệ hơn vòng lặp dễ đọc.

```python
# Đừng làm thế này (khó đọc dù "ngắn")
result = [transform(x) for sublist in data for x in sublist if x is not None if validate(x)]

# Senior sẽ viết:
def process(data):
    result = []
    for sublist in data:
        for x in sublist:
            if x is not None and validate(x):
                result.append(transform(x))
    return result
```

🔨 **Bài tập:** Viết một dict comprehension chuyển list `["a", "bb", "ccc"]` thành `{"a": 1, "bb": 2, "ccc": 3}` (key là chuỗi, value là độ dài).

### 1.5. Vòng lặp Pythonic: enumerate, zip, itertools

```python
# Không Pythonic
for i in range(len(names)):
    print(i, names[i])

# Pythonic
for i, name in enumerate(names):
    print(i, name)

# Lặp qua 2 list song song — không Pythonic
for i in range(len(names)):
    print(names[i], ages[i])

# Pythonic
for name, age in zip(names, ages):
    print(name, age)
```

Module `itertools` là công cụ senior hay dùng để tránh viết lại logic lặp phức tạp:

```python
from itertools import chain, groupby, islice, combinations

# Nối nhiều iterable mà không tạo list trung gian tốn bộ nhớ
for item in chain(list1, list2, list3):
    ...

# Lấy 10 phần tử đầu của 1 generator (không cần list hóa)
first_10 = list(islice(infinite_generator(), 10))

# Nhóm dữ liệu đã sort theo key
for key, group in groupby(sorted(data, key=lambda x: x.category), key=lambda x: x.category):
    print(key, list(group))
```

### 1.6. String formatting: luôn dùng f-string

```python
name, age = "An", 25

# Cũ, tránh dùng trong code mới
"Tên: %s, tuổi: %d" % (name, age)
"Tên: {}, tuổi: {}".format(name, age)

# Chuẩn hiện đại (Python 3.6+)
f"Tên: {name}, tuổi: {age}"

# f-string còn tính toán được biểu thức, format số
price = 1234567.891
f"Giá: {price:,.2f} VNĐ"     # "Giá: 1,234,567.89 VNĐ"
f"{age=}"                     # debug nhanh: "age=25" (Python 3.8+)
```

`f"{age=}"` là mẹo debug senior hay dùng — in ra cả tên biến lẫn giá trị, tiện hơn `print("age:", age)`.

### 1.7. Truthy/Falsy — viết điều kiện như dân bản xứ

Trong Python, các giá trị sau được coi là "falsy": `False`, `None`, `0`, `0.0`, `""`, `[]`, `{}`, `()`, `set()`. Mọi thứ khác là "truthy".

```python
# Không Pythonic
if len(my_list) == 0:
    ...
if my_list == []:
    ...
if my_string == "" or my_string is None:
    ...

# Pythonic
if not my_list:
    ...
if not my_string:
    ...
```

**Nhưng cẩn thận:** `if not my_list` sẽ True cho cả `None` lẫn `[]` lẫn số 0. Khi bạn cần phân biệt "chưa có giá trị" (`None`) với "có giá trị nhưng rỗng/bằng 0", phải dùng `is None` tường minh:

```python
def set_discount(discount=None):
    if discount is None:        # phân biệt "không truyền" với "truyền 0"
        discount = get_default_discount()
    ...
```

Đây là chỗ rất nhiều junior code sai: `if not discount:` sẽ vô tình ghi đè cả khi người dùng cố tình truyền `discount=0`.

### 1.8. Xử lý lỗi: EAFP vs LBYL

Python ưu tiên triết lý **EAFP** (Easier to Ask Forgiveness than Permission — dễ xin lỗi hơn xin phép) thay vì **LBYL** (Look Before You Leap — nhìn trước khi nhảy) phổ biến ở C/Java.

```python
# LBYL (kiểu C/Java — có "race condition": key có thể bị xóa giữa lúc check và lúc lấy)
if "name" in data:
    value = data["name"]
else:
    value = "unknown"

# EAFP (Pythonic — nhanh hơn trong đa số trường hợp, tránh race condition)
try:
    value = data["name"]
except KeyError:
    value = "unknown"

# Nhưng thực ra ở đây, cách ngắn gọn nhất là:
value = data.get("name", "unknown")
```

**Quy tắc chọn except:**

```python
# SAI NGHIÊM TRỌNG — bắt hết mọi lỗi, nuốt luôn cả lỗi lập trình (bug thật)
try:
    result = risky_operation()
except Exception:
    pass   # <- không bao giờ làm thế này, bạn sẽ không biết code đang lỗi gì

# ĐÚNG — chỉ bắt lỗi bạn thực sự lường trước và biết cách xử lý
try:
    result = risky_operation()
except (ConnectionError, TimeoutError) as e:
    logger.warning(f"Không kết nối được: {e}")
    result = None
```

**Nguyên tắc vàng:** except càng cụ thể càng tốt. `except Exception: pass` là một trong những "code smell" tệ nhất — nó che giấu bug thay vì xử lý lỗi. Senior review code sẽ luôn từ chối merge PR có pattern này.

Custom exception — khi hàm của bạn cần báo lỗi nghiệp vụ (business logic), đừng dùng exception built-in chung chung:

```python
class InsufficientFundsError(Exception):
    """Ném ra khi số dư không đủ để thực hiện giao dịch."""
    def __init__(self, balance, amount):
        self.balance = balance
        self.amount = amount
        super().__init__(f"Số dư {balance} không đủ để rút {amount}")

def withdraw(account, amount):
    if account.balance < amount:
        raise InsufficientFundsError(account.balance, amount)
    account.balance -= amount
```

Lợi ích: người gọi hàm có thể `except InsufficientFundsError` riêng biệt, xử lý khác với lỗi kết nối database, khác với lỗi validate input.

### 1.9. Hàm: *args, **kwargs, và hàm là "công dân hạng nhất"

```python
def log(message, *args, **kwargs):
    """
    *args: gom mọi positional argument thừa thành tuple
    **kwargs: gom mọi keyword argument thừa thành dict
    """
    print(message.format(*args, **kwargs))

log("Xin chào {}, bạn {} tuổi", "An", 25)
log("User: {name}", name="Bình")
```

Trong Python, **hàm là object** — có thể gán cho biến, truyền làm tham số, trả về từ hàm khác. Đây là nền tảng cho decorator, callback, và lập trình hàm:

```python
def apply_discount(price, discount_fn):
    return discount_fn(price)

def ten_percent_off(price):
    return price * 0.9

apply_discount(100, ten_percent_off)   # 90.0

# Hàm ẩn danh cho logic đơn giản, dùng 1 lần
apply_discount(100, lambda p: p * 0.9)
```

**Quy tắc:** `lambda` chỉ nên dùng cho biểu thức 1 dòng, không có tên gọi rõ ràng, dùng ngay tại chỗ (thường làm `key=` cho `sorted`, `map`, `filter`). Nếu logic phức tạp hơn 1 dòng hoặc bạn dùng lại nhiều lần → đặt tên bằng `def`.

```python
# Hợp lý
students.sort(key=lambda s: s.gpa, reverse=True)

# Không hợp lý — nên đặt tên hàm riêng
process = lambda x: (x.strip().lower().replace(" ", "_") if x else "unknown")
```

### 1.10. Scope và closure

Python có quy tắc tìm biến theo thứ tự **LEGB**: Local → Enclosing → Global → Built-in.

```python
x = "global"

def outer():
    x = "enclosing"
    def inner():
        x = "local"
        print(x)          # "local"
    inner()
    print(x)               # "enclosing" — không bị inner() ảnh hưởng
outer()
print(x)                   # "global"
```

Closure là khi hàm con "nhớ" biến của hàm cha ngay cả sau khi hàm cha đã chạy xong — nền tảng để hiểu decorator (Phần 3):

```python
def make_counter():
    count = 0
    def counter():
        nonlocal count     # cho phép sửa biến của scope ngoài
        count += 1
        return count
    return counter

c = make_counter()
print(c(), c(), c())   # 1 2 3
```

**Bẫy kinh điển #2 — late binding trong closure/lambda tạo trong vòng lặp:**

```python
# SAI — mọi lambda đều in ra 2 (giá trị cuối cùng của i)
funcs = [lambda: i for i in range(3)]
print([f() for f in funcs])   # [2, 2, 2] — không phải [0, 1, 2]!

# ĐÚNG — ép giá trị i vào tại thời điểm tạo lambda bằng default argument
funcs = [lambda i=i: i for i in range(3)]
print([f() for f in funcs])   # [0, 1, 2]
```

Lý do: lambda không "chụp ảnh" giá trị của `i` lúc tạo ra, nó chỉ giữ tham chiếu tới biến `i`. Khi vòng lặp kết thúc, `i` bằng 2, nên mọi lambda đều trả về 2.

### 1.11. Module, package và import — hiểu cách Python tìm code

```python
# Cấu trúc project chuẩn
myproject/
├── myapp/
│   ├── __init__.py
│   ├── models.py
│   ├── services.py
│   └── utils/
│       ├── __init__.py
│       └── validators.py
├── tests/
│   └── test_services.py
├── pyproject.toml
└── README.md
```

```python
# Trong services.py
from myapp.models import User            # import tuyệt đối — LUÔN ưu tiên cách này
from myapp.utils.validators import validate_email

from .models import User                  # import tương đối — chỉ dùng trong package nội bộ, hạn chế lạm dụng
```

**Quy tắc senior:** tránh `from module import *` — nó làm ô nhiễm namespace, gây khó debug khi 2 module có hàm trùng tên, và IDE/linter không biết bạn đang dùng cái gì từ đâu.

```python
# Tránh
from os import *

# Nên
import os
os.path.join(...)
```

### 1.12. Virtual environment & quản lý dependency

Đây là kỹ năng senior coi là "hiển nhiên" nhưng cực nhiều junior bỏ qua rồi gặp lỗi "works on my machine". Mỗi project Python nên có **môi trường ảo riêng** để version các thư viện không xung đột giữa các project.

```bash
# Cách cơ bản nhất — venv (có sẵn trong Python, không cần cài thêm)
python3 -m venv .venv
source .venv/bin/activate       # Linux/Mac
.venv\Scripts\activate          # Windows

pip install requests
pip freeze > requirements.txt   # lưu lại danh sách dependency

# Ở project khác, hoặc máy khác:
pip install -r requirements.txt
```

Công cụ hiện đại senior hay dùng thay cho pip/venv thuần: **uv** (nhanh, hiện đại, đang là xu hướng 2025-2026) hoặc **poetry** (quản lý dependency + build + publish trong 1 công cụ). Nếu bạn mới, hãy thành thạo `venv` + `pip` trước, rồi học `uv` hoặc `poetry` sau — nguyên lý là như nhau, chỉ khác cú pháp.

**Nguyên tắc bất di bất dịch:** không bao giờ `pip install` trực tiếp vào Python hệ thống (global). Luôn tạo venv trước, dù project nhỏ tới đâu.

---

## PHẦN 2: OOP KIỂU PYTHON

### 2.1. Class cơ bản, đúng chuẩn

```python
class BankAccount:
    """Đại diện cho một tài khoản ngân hàng."""

    def __init__(self, owner: str, balance: float = 0):
        self.owner = owner
        self.balance = balance

    def deposit(self, amount: float) -> None:
        if amount <= 0:
            raise ValueError("Số tiền nạp phải dương")
        self.balance += amount

    def withdraw(self, amount: float) -> None:
        if amount > self.balance:
            raise InsufficientFundsError(self.balance, amount)
        self.balance -= amount

    def __repr__(self) -> str:
        return f"BankAccount(owner={self.owner!r}, balance={self.balance})"
```

Vài điểm senior luôn để ý:
- **Type hint** (`owner: str`, `-> None`) — không bắt buộc để chạy, nhưng giúp IDE gợi ý, giúp người khác đọc hiểu ngay, và bắt lỗi sớm với công cụ như `mypy`.
- **Docstring** ngay dưới tên class/hàm — giải thích class này *đại diện cho cái gì*, không phải *nó làm gì* (đó là việc của tên hàm).
- **`__repr__`** — luôn định nghĩa cho class của bạn. Không có nó, khi debug bạn chỉ thấy `<BankAccount object at 0x7f...>` vô nghĩa.

### 2.2. Dunder methods (magic methods) — Python "lắng nghe" chúng ở đâu

```python
class Money:
    def __init__(self, amount, currency="VND"):
        self.amount = amount
        self.currency = currency

    def __repr__(self):
        return f"Money({self.amount}, {self.currency!r})"

    def __eq__(self, other):
        return self.amount == other.amount and self.currency == other.currency

    def __add__(self, other):
        if self.currency != other.currency:
            raise ValueError("Không thể cộng 2 loại tiền tệ khác nhau")
        return Money(self.amount + other.amount, self.currency)

    def __lt__(self, other):
        return self.amount < other.amount

m1 = Money(100)
m2 = Money(50)
print(m1 + m2)        # Money(150, 'VND')
print(m1 == Money(100))  # True
print(m1 > m2)         # True — Python tự suy ra từ __lt__ khi dùng functools.total_ordering
```

Bảng dunder phổ biến nhất senior hay implement:

| Dunder | Kích hoạt khi nào |
|---|---|
| `__init__` | Khởi tạo object |
| `__repr__` | `repr(obj)`, hiển thị trong debugger, console |
| `__str__` | `str(obj)`, `print(obj)` |
| `__eq__`, `__lt__`... | So sánh `==`, `<`, `>`... |
| `__len__` | `len(obj)` |
| `__getitem__` | `obj[key]` |
| `__iter__` | `for x in obj` |
| `__enter__`/`__exit__` | `with obj:` (context manager, xem Phần 3) |
| `__call__` | Gọi object như hàm: `obj()` |

**Tại sao quan trọng:** dunder methods giúp custom class của bạn "hòa nhập" với cú pháp built-in của Python, thay vì buộc người dùng phải nhớ API riêng (`obj.length()` thay vì `len(obj)`). Đây chính là điều làm code Python nhất quán trên toàn hệ sinh thái.

### 2.3. Composition over Inheritance

Đây là một trong những nguyên tắc thiết kế OOP quan trọng nhất mà rất nhiều junior học OOP qua sách giáo khoa hiểu sai — họ nghĩ OOP = phân cấp kế thừa càng sâu càng "chuẩn". Thực tế: **kế thừa tạo ra ràng buộc chặt** (tight coupling); **composition** (một class chứa instance của class khác) linh hoạt hơn nhiều.

```python
# Kế thừa lạm dụng — dễ dẫn tới "cây kế thừa" phình to, khó bảo trì
class Bird:
    def fly(self):
        print("Bay")

class Penguin(Bird):     # SAI về ngữ nghĩa — chim cánh cụt không bay được!
    def fly(self):
        raise NotImplementedError("Chim cánh cụt không bay được")

# Composition — linh hoạt, đúng ngữ nghĩa hơn
class FlyingAbility:
    def fly(self):
        print("Bay")

class SwimmingAbility:
    def swim(self):
        print("Bơi")

class Penguin:
    def __init__(self):
        self.swimming = SwimmingAbility()   # penguin CÓ khả năng bơi

    def swim(self):
        self.swimming.swim()

class Eagle:
    def __init__(self):
        self.flying = FlyingAbility()       # eagle CÓ khả năng bay

    def fly(self):
        self.flying.fly()
```

**Quy tắc thực dụng:** chỉ dùng kế thừa khi quan hệ thực sự là "is-a" (Penguin IS-A Bird) VÀ class con không cần "phá vỡ" hành vi của class cha (như ví dụ `fly()` ở trên). Nếu bạn thấy mình đang override một method chỉ để `raise NotImplementedError` hoặc làm ngược lại hoàn toàn — đó là dấu hiệu bạn nên dùng composition.

### 2.4. `@property` — kiểm soát truy cập attribute mà không phá API

```python
class Circle:
    def __init__(self, radius):
        self._radius = radius

    @property
    def radius(self):
        return self._radius

    @radius.setter
    def radius(self, value):
        if value <= 0:
            raise ValueError("Bán kính phải dương")
        self._radius = value

    @property
    def area(self):                # thuộc tính tính toán, không lưu trữ trực tiếp
        return 3.14159 * self._radius ** 2

c = Circle(5)
print(c.area)        # gọi như attribute, không phải c.area()
c.radius = 10         # đi qua validation trong setter
c.radius = -5         # ValueError
```

Lợi ích so với `get_radius()`/`set_radius()` kiểu Java: người dùng class vẫn viết `c.radius` như một attribute bình thường, nhưng bạn (người viết class) toàn quyền thêm validate/logic phía sau mà **không phải sửa code ở nơi khác đang dùng class này**. Đây là tính đóng gói (encapsulation) đúng nghĩa.

### 2.5. `@dataclass` — giảm boilerplate cho class chỉ chứa dữ liệu

```python
from dataclasses import dataclass, field

@dataclass
class Product:
    name: str
    price: float
    tags: list[str] = field(default_factory=list)   # tránh bẫy mutable default (mục 1.2)

p1 = Product("Áo thun", 150000)
p2 = Product("Áo thun", 150000)
print(p1 == p2)      # True — __eq__ tự sinh ra
print(p1)            # Product(name='Áo thun', price=150000, tags=[])
```

`@dataclass` tự sinh `__init__`, `__repr__`, `__eq__` cho bạn — dùng khi class chủ yếu là "cái túi đựng dữ liệu" (data holder), không cần viết tay các dunder ở trên.

### 2.6. Abstract Base Class & Protocol — định nghĩa "hợp đồng" (interface)

```python
from abc import ABC, abstractmethod

class PaymentProcessor(ABC):
    @abstractmethod
    def process(self, amount: float) -> bool:
        """Mọi class con BẮT BUỘC phải implement hàm này."""
        ...

class MomoProcessor(PaymentProcessor):
    def process(self, amount: float) -> bool:
        print(f"Xử lý {amount} qua Momo")
        return True

# PaymentProcessor()          # TypeError — không thể khởi tạo class abstract
processor = MomoProcessor()   # OK
```

Dùng `ABC` khi bạn muốn ép buộc mọi class con phải implement một số hàm nhất định — hữu ích khi thiết kế hệ thống có nhiều "plugin" cùng tuân theo 1 interface (ví dụ nhiều cổng thanh toán, nhiều nguồn dữ liệu).

`Protocol` (từ `typing`) là cách "hiện đại" hơn — kiểm tra theo **structural typing** (duck typing có kiểm tra tĩnh), không cần kế thừa:

```python
from typing import Protocol

class Drawable(Protocol):
    def draw(self) -> None: ...

class Circle:                 # không cần kế thừa Drawable
    def draw(self) -> None:
        print("Vẽ hình tròn")

def render(shape: Drawable) -> None:   # mypy chấp nhận Circle vì nó "khớp hình dạng"
    shape.draw()
```

### 2.7. SOLID — 5 nguyên tắc áp dụng thực tế trong Python

- **S — Single Responsibility:** một class chỉ nên có 1 lý do để thay đổi. Nếu class `User` vừa lưu dữ liệu, vừa gửi email, vừa ghi log — tách thành `User`, `EmailService`, `Logger`.
- **O — Open/Closed:** mở rộng được mà không sửa code cũ. Ví dụ `PaymentProcessor` ở trên — thêm `ZaloPayProcessor` mới mà không đụng vào `MomoProcessor`.
- **L — Liskov Substitution:** class con phải dùng thay class cha được mà không phá vỡ logic (đây là lý do ví dụ `Penguin(Bird)` ở mục 2.3 là thiết kế tồi).
- **I — Interface Segregation:** đừng ép class implement những method nó không cần. Interface nhỏ, chuyên biệt tốt hơn interface "to và tất cả".
- **D — Dependency Inversion:** phụ thuộc vào abstraction (interface), không phụ thuộc vào class cụ thể.

```python
# Vi phạm Dependency Inversion — OrderService bị khóa cứng vào MomoProcessor
class OrderService:
    def __init__(self):
        self.payment = MomoProcessor()    # không thể đổi sang ZaloPay mà không sửa code này

# Tuân thủ Dependency Inversion
class OrderService:
    def __init__(self, payment_processor: PaymentProcessor):   # phụ thuộc vào abstraction
        self.payment = payment_processor

order_service = OrderService(MomoProcessor())     # dễ dàng đổi sang ZaloPayProcessor(), hoặc dùng cho test
```

Đây gọi là **Dependency Injection** — "tiêm" phụ thuộc từ bên ngoài vào thay vì tự tạo bên trong. Lợi ích lớn nhất: viết unit test dễ dàng (Phần 5) vì bạn có thể "tiêm" một processor giả (mock) vào để test mà không cần gọi API thanh toán thật.

---

## PHẦN 3: KỸ THUẬT NÂNG CAO — ĐIỀU LÀM PYTHON KHÁC BIỆT

### 3.1. Iterator & Generator — xử lý dữ liệu lớn mà không "nổ" RAM

Vấn đề: nếu bạn có 10 triệu dòng dữ liệu cần xử lý, tạo hẳn 1 list 10 triệu phần tử trong RAM là lãng phí — nhất là khi bạn chỉ cần xử lý từng phần tử một lần rồi bỏ.

```python
# Cách "tốn RAM" — toàn bộ list nằm trong bộ nhớ cùng lúc
def get_squares(n):
    return [i ** 2 for i in range(n)]

squares = get_squares(10_000_000)   # chiếm hàng trăm MB ngay lập tức

# Generator — tạo giá trị "lười" (lazy), từng phần tử một, gần như không tốn RAM
def get_squares(n):
    for i in range(n):
        yield i ** 2

squares = get_squares(10_000_000)   # chưa tính toán gì cả, chỉ là 1 "kế hoạch"
for sq in squares:                  # tính từng giá trị khi cần
    process(sq)
```

`yield` biến hàm thường thành generator function. Khác biệt cốt lõi với `return`: `return` kết thúc hàm và trả về 1 giá trị; `yield` **tạm dừng** hàm, trả về 1 giá trị, và có thể tiếp tục từ đúng chỗ đó ở lần gọi tiếp theo.

```python
def read_large_file(path):
    """Đọc file lớn từng dòng, không load hết file vào RAM."""
    with open(path) as f:
        for line in f:
            yield line.strip()

for line in read_large_file("huge_log.txt"):   # xử lý từng dòng, dù file 50GB
    if "ERROR" in line:
        print(line)
```

**Khi nào dùng generator:** dữ liệu lớn/vô hạn, chỉ cần duyệt qua 1 lần, không cần truy cập ngẫu nhiên theo index, muốn tiết kiệm RAM hoặc "stream" dữ liệu (đọc file, gọi API phân trang, xử lý dòng theo dòng).

**Khi nào KHÔNG dùng generator:** cần duyệt qua dữ liệu nhiều lần (generator chỉ dùng được 1 lần rồi "cạn"), cần biết `len()`, cần index ngẫu nhiên `data[5]`.

### 3.2. Decorator — "bọc" hành vi thêm vào hàm mà không sửa hàm gốc

Decorator tận dụng việc hàm là object (mục 1.9) + closure (mục 1.10). Cú pháp `@decorator` chỉ là "đường tắt" (syntactic sugar):

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print(f"Gọi hàm {func.__name__}")
        result = func(*args, **kwargs)
        print(f"Hàm {func.__name__} chạy xong")
        return result
    return wrapper

@my_decorator
def greet(name):
    print(f"Xin chào, {name}")

greet("An")
# tương đương với: greet = my_decorator(greet)
```

Decorator thực tế senior hay viết — đo thời gian chạy hàm:

```python
import time
import functools

def timeit(func):
    @functools.wraps(func)     # giữ lại __name__, __doc__ gốc — LUÔN dùng cái này
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        result = func(*args, **kwargs)
        elapsed = time.perf_counter() - start
        print(f"{func.__name__} chạy trong {elapsed:.4f}s")
        return result
    return wrapper

@timeit
def slow_function():
    time.sleep(1)
```

**Lưu ý quan trọng:** luôn dùng `@functools.wraps(func)` trong wrapper — nếu không, `slow_function.__name__` sẽ bị đổi thành `"wrapper"`, phá vỡ debugging, docstring, và các công cụ giới thiệu (introspection) khác.

Decorator có tham số (decorator factory):

```python
def retry(times=3):
    def decorator(func):
        @functools.wraps(func)
        def wrapper(*args, **kwargs):
            for attempt in range(times):
                try:
                    return func(*args, **kwargs)
                except ConnectionError:
                    print(f"Thử lại lần {attempt + 1}/{times}")
            raise ConnectionError("Đã thử hết số lần cho phép")
        return wrapper
    return decorator

@retry(times=5)
def call_api():
    ...
```

Decorator built-in cực kỳ quan trọng cần thuộc lòng:
- `@property` — đã học ở mục 2.4
- `@staticmethod` — hàm trong class không cần `self`, không truy cập instance/class state, chỉ nằm trong class vì liên quan logic
- `@classmethod` — hàm nhận `cls` thay vì `self`, thường dùng làm "alternative constructor"
- `@functools.lru_cache` — cache kết quả hàm tự động (xem mục 6.1)

```python
class Pizza:
    def __init__(self, size, toppings):
        self.size = size
        self.toppings = toppings

    @classmethod
    def margherita(cls):                          # constructor "đặt sẵn"
        return cls(size="medium", toppings=["cheese", "tomato"])

    @staticmethod
    def is_valid_size(size):                       # không cần self, chỉ liên quan logic
        return size in ("small", "medium", "large")

p = Pizza.margherita()
```

### 3.3. Context Manager — đảm bảo dọn dẹp tài nguyên, luôn luôn

```python
# Vấn đề: nếu có exception giữa chừng, file có thể không được đóng
f = open("data.txt")
data = f.read()
f.close()          # nếu dòng trên lỗi, dòng này KHÔNG BAO GIỜ chạy!

# Giải pháp: with statement — đảm bảo __exit__ luôn chạy dù có lỗi hay không
with open("data.txt") as f:
    data = f.read()
# file tự động đóng ngay khi ra khỏi block with, kể cả khi có exception
```

Tự viết context manager riêng — hữu ích cho: kết nối database, lock, đo thời gian, transaction:

```python
from contextlib import contextmanager

@contextmanager
def db_transaction(connection):
    connection.begin()
    try:
        yield connection
        connection.commit()
    except Exception:
        connection.rollback()
        raise
    finally:
        connection.close()

with db_transaction(conn) as tx:
    tx.execute("INSERT INTO users ...")
    # commit tự động nếu không lỗi, rollback tự động nếu có lỗi
```

Hoặc viết bằng class (khi logic phức tạp hơn 1 hàm generator có thể diễn tả gọn):

```python
class Timer:
    def __enter__(self):
        self.start = time.perf_counter()
        return self

    def __exit__(self, exc_type, exc_value, traceback):
        self.elapsed = time.perf_counter() - self.start
        print(f"Mất {self.elapsed:.4f}s")
        return False   # False = không "nuốt" exception, để nó tiếp tục lan truyền

with Timer() as t:
    slow_function()
```

**Nguyên tắc senior:** bất cứ khi nào bạn thấy pattern "mở → dùng → phải đóng/dọn dẹp" (file, socket, lock, connection, transaction), hãy nghĩ ngay tới context manager thay vì try/finally thủ công lặp lại nhiều nơi.

### 3.4. Type hints — giao tiếp ý định, bắt lỗi sớm

```python
from typing import Optional, Union

def find_user(user_id: int) -> Optional[dict]:
    """Trả về dict thông tin user, hoặc None nếu không tìm thấy."""
    ...

def parse_input(value: Union[str, int]) -> int:
    ...

# Python 3.10+: cú pháp mới gọn hơn
def find_user(user_id: int) -> dict | None:
    ...
```

Type hint không được Python kiểm tra lúc chạy (runtime) — chúng chỉ là "tài liệu sống" cho IDE và cho công cụ kiểm tra tĩnh như `mypy` hoặc `pyright`. Nhưng đây là công cụ senior dùng hàng ngày vì:

1. IDE gợi ý autocomplete chính xác hơn nhiều
2. Bắt được lỗi kiểu dữ liệu **trước khi chạy code**, không phải khi crash ở production
3. Là tài liệu "không bao giờ lỗi thời" — không như comment (comment có thể bị quên cập nhật, type hint sai sẽ bị mypy báo lỗi ngay)

```bash
pip install mypy
mypy myfile.py    # kiểm tra kiểu tĩnh, báo lỗi mà không cần chạy code
```

🔨 **Bài tập:** Thêm type hint đầy đủ cho `BankAccount` ở mục 2.1, chạy `mypy` để kiểm tra.

### 3.5. Functional tools: `functools`, `map`/`filter`, khi nào nên và không nên

```python
from functools import reduce, partial

# map/filter — tồn tại nhưng list comprehension thường Pythonic hơn
nums = [1, 2, 3, 4, 5]
doubled = list(map(lambda x: x * 2, nums))     # ít Pythonic
doubled = [x * 2 for x in nums]                 # ưu tiên cách này

# reduce — hữu ích khi "gộp" 1 danh sách thành 1 giá trị
total = reduce(lambda acc, x: acc + x, nums, 0)
total = sum(nums)                                # có hàm built-in thì luôn ưu tiên built-in

# partial — "đóng băng" trước 1 số tham số của hàm
def power(base, exponent):
    return base ** exponent

square = partial(power, exponent=2)
print(square(5))    # 25
```

**Quy tắc thực dụng:** Python KHÔNG phải ngôn ngữ hàm thuần túy như Haskell. Đừng cố "functional hóa" mọi thứ. Ưu tiên thứ tự: hàm built-in có sẵn (`sum`, `max`, `sorted`) → comprehension → `map`/`filter`/`reduce` chỉ khi thực sự rõ ràng hơn.

---

## PHẦN 4: KIẾN TRÚC & CLEAN CODE

### 4.1. Cấu trúc project theo layer (tách lớp trách nhiệm)

Junior thường viết mọi logic vào 1 file, hoặc trộn lẫn logic xử lý business với logic truy cập database, với logic hiển thị API response. Senior tách rõ theo tầng:

```
myapp/
├── api/              # tầng giao tiếp — nhận request, trả response (FastAPI/Flask routes)
│   └── routes.py
├── services/          # tầng logic nghiệp vụ — "luật chơi" của ứng dụng
│   └── order_service.py
├── repositories/       # tầng truy cập dữ liệu — CHỈ nói chuyện với database
│   └── order_repository.py
├── models/             # định nghĩa cấu trúc dữ liệu (dataclass, ORM model)
│   └── order.py
└── utils/              # hàm tiện ích dùng chung, không phụ thuộc business logic
```

```python
# repositories/order_repository.py — CHỈ biết cách lấy/lưu dữ liệu, không biết luật nghiệp vụ
class OrderRepository:
    def __init__(self, db_connection):
        self.db = db_connection

    def get_by_id(self, order_id: int) -> Order | None:
        row = self.db.execute("SELECT * FROM orders WHERE id = ?", order_id)
        return Order(**row) if row else None

    def save(self, order: Order) -> None:
        self.db.execute("INSERT INTO orders ...", order)

# services/order_service.py — biết LUẬT NGHIỆP VỤ, không biết chi tiết SQL
class OrderService:
    def __init__(self, order_repo: OrderRepository, payment: PaymentProcessor):
        self.order_repo = order_repo
        self.payment = payment

    def checkout(self, order_id: int) -> bool:
        order = self.order_repo.get_by_id(order_id)
        if order is None:
            raise OrderNotFoundError(order_id)
        if order.total <= 0:
            raise InvalidOrderError("Đơn hàng không hợp lệ")
        success = self.payment.process(order.total)
        if success:
            order.status = "paid"
            self.order_repo.save(order)
        return success
```

**Lợi ích thấy rõ ngay:** nếu ngày mai đổi từ SQL sang MongoDB, bạn chỉ sửa `OrderRepository`, không đụng vào `OrderService`. Nếu cần viết unit test cho `OrderService`, bạn "tiêm" một `OrderRepository` giả (mock), không cần database thật chạy trong lúc test.

### 4.2. Design patterns thường gặp trong Python (không học vẹt, học vì sao cần)

**Strategy Pattern** — khi bạn có nhiều cách làm 1 việc, muốn chọn 1 trong số đó lúc chạy:

```python
class DiscountStrategy(Protocol):
    def calculate(self, price: float) -> float: ...

class NoDiscount:
    def calculate(self, price): return price

class PercentageDiscount:
    def __init__(self, percent): self.percent = percent
    def calculate(self, price): return price * (1 - self.percent / 100)

class Order:
    def __init__(self, price, discount_strategy: DiscountStrategy = NoDiscount()):
        self.price = price
        self.discount_strategy = discount_strategy

    def total(self):
        return self.discount_strategy.calculate(self.price)
```

Đây thực chất là ví dụ cụ thể hóa Dependency Injection (mục 2.7) — "chiến lược" giảm giá được "tiêm" vào từ ngoài.

**Factory Pattern** — khi việc khởi tạo object phức tạp hoặc phụ thuộc điều kiện:

```python
def create_payment_processor(method: str) -> PaymentProcessor:
    processors = {
        "momo": MomoProcessor,
        "zalopay": ZaloPayProcessor,
        "visa": VisaProcessor,
    }
    processor_class = processors.get(method)
    if processor_class is None:
        raise ValueError(f"Phương thức thanh toán không hỗ trợ: {method}")
    return processor_class()
```

**Singleton** — Python hiếm khi cần pattern này theo kiểu Java/C++ (dùng module-level object thay thế đơn giản hơn nhiều):

```python
# config.py — module chỉ được import 1 lần, tự nhiên đã là "singleton"
class Config:
    def __init__(self):
        self.debug = False
        self.db_url = "postgresql://..."

config = Config()   # import config; config.config — luôn cùng 1 instance
```

**Nguyên tắc quan trọng nhất về design pattern:** đừng học pattern rồi cố nhét vào mọi bài toán ("khi cầm búa, cái gì cũng thấy giống đinh"). Pattern tồn tại để giải quyết vấn đề *lặp lại* cụ thể. Nếu bài toán của bạn không có vấn đề đó, đừng dùng pattern — code đơn giản luôn thắng code "đúng pattern" nhưng thừa thãi.

### 4.3. Nguyên tắc DRY, nhưng đừng DRY quá đà

**DRY (Don't Repeat Yourself)** — logic nghiệp vụ không nên lặp lại ở nhiều nơi (sửa 1 chỗ, quên chỗ khác gây bug). Nhưng:

```python
# Trùng lặp KHÔNG đáng lo — 2 hàm này TRÙNG HỢP giống nhau về cú pháp,
# nhưng khác nhau về Ý NGHĨA NGHIỆP VỤ, có thể thay đổi độc lập trong tương lai
def validate_username(name):
    return len(name) >= 3 and len(name) <= 20

def validate_product_code(code):
    return len(code) >= 3 and len(code) <= 20
```

Nếu bạn "DRY hóa" 2 hàm trên thành `validate_length(s, 3, 20)` dùng chung, ngày mai product code đổi rule thành "phải bắt đầu bằng chữ P" — bạn buộc phải viết `if`/`else` để phân biệt 2 trường hợp bên trong 1 hàm chung, code lại rối hơn. **Nguyên tắc thực dụng:** chỉ gộp code khi chúng thực sự đại diện cho **cùng 1 khái niệm nghiệp vụ**, không phải chỉ vì chúng "trông giống nhau" bây giờ.

### 4.4. Đặt tên biến/hàm — kỹ năng bị đánh giá thấp nhất

```python
# Junior
def calc(x, y, t):
    if t == 1:
        return x + y
    elif t == 2:
        return x - y

# Senior
def calculate(a: float, b: float, operation: Literal["add", "subtract"]) -> float:
    if operation == "add":
        return a + b
    elif operation == "subtract":
        return a - b
```

Quy tắc đặt tên senior luôn áp dụng:
- Tên hàm là **động từ** (`get_user`, `calculate_total`, `send_email`)
- Tên biến/class là **danh từ** (`user`, `order_total`, `EmailService`)
- Boolean nên bắt đầu bằng `is_`, `has_`, `can_` (`is_valid`, `has_permission`)
- Tránh viết tắt mơ hồ (`t`, `x`, `tmp`, `data2`) trừ khi trong ngữ cảnh cực ngắn (biến lặp `i`, `j` trong vòng for đơn giản là chấp nhận được)
- Độ dài tên tỉ lệ thuận với phạm vi sử dụng: biến dùng trong 2 dòng có thể tên ngắn (`i`), biến dùng xuyên suốt cả module cần tên rõ ràng (`active_user_count`)

### 4.5. Comment: giải thích "tại sao", không phải "cái gì"

```python
# TỆ — comment lặp lại điều code đã nói rõ
x = x + 1  # tăng x lên 1

# TỐT — comment giải thích lý do không hiển nhiên từ code
# Cộng thêm 1 vì API bên thứ 3 đánh index bắt đầu từ 1, không phải 0
x = x + 1
```

Code tốt tự giải thích "làm gì" qua tên biến/hàm rõ ràng. Comment chỉ nên tồn tại khi có **ngữ cảnh** mà code không thể diễn đạt — quyết định nghiệp vụ, workaround cho bug của thư viện ngoài, lý do lịch sử.

---

## PHẦN 5: TESTING & DEBUGGING CHUYÊN NGHIỆP

### 5.1. Tại sao senior luôn viết test — không phải vì "quy định"

Junior thường coi test là gánh nặng thêm việc. Senior coi test là công cụ để:
1. **Tự tin refactor** — sửa code mà biết chắc không phá hỏng cái gì khác (test đỏ = báo ngay)
2. **Tài liệu sống** — test case chính là ví dụ cụ thể "hàm này được dùng thế nào", "trường hợp biên nào cần xử lý"
3. **Bắt bug trước khi lên production** — rẻ hơn rất nhiều so với bug bị người dùng phát hiện

### 5.2. pytest — công cụ test tiêu chuẩn của cộng đồng Python

```python
# test_bank_account.py
import pytest
from bank import BankAccount, InsufficientFundsError

def test_deposit_increases_balance():
    account = BankAccount(owner="An", balance=100)
    account.deposit(50)
    assert account.balance == 150

def test_withdraw_raises_error_when_insufficient_funds():
    account = BankAccount(owner="An", balance=100)
    with pytest.raises(InsufficientFundsError):
        account.withdraw(200)

def test_deposit_negative_amount_raises_error():
    account = BankAccount(owner="An", balance=100)
    with pytest.raises(ValueError):
        account.deposit(-10)
```

```bash
pip install pytest
pytest                    # chạy tất cả test trong thư mục tests/
pytest -v                 # verbose, in tên từng test
pytest test_bank_account.py::test_deposit_increases_balance   # chạy 1 test cụ thể
pytest --cov=myapp        # đo % code được test bao phủ (cần pip install pytest-cov)
```

**Fixture** — chuẩn bị dữ liệu/tài nguyên dùng chung cho nhiều test, tránh lặp code setup:

```python
@pytest.fixture
def sample_account():
    """Tạo tài khoản mẫu, dùng lại cho nhiều test."""
    return BankAccount(owner="An", balance=1000)

def test_deposit(sample_account):
    sample_account.deposit(500)
    assert sample_account.balance == 1500

def test_withdraw(sample_account):
    sample_account.withdraw(300)
    assert sample_account.balance == 700
```

**Parametrize** — chạy cùng 1 test logic với nhiều bộ input khác nhau, tránh copy-paste test:

```python
@pytest.mark.parametrize("amount,expected_error", [
    (-10, ValueError),
    (0, ValueError),
])
def test_deposit_invalid_amounts(sample_account, amount, expected_error):
    with pytest.raises(expected_error):
        sample_account.deposit(amount)
```

### 5.3. Mock — giả lập phụ thuộc bên ngoài để test cô lập

Vấn đề: nếu `OrderService` (mục 4.1) gọi API thanh toán thật mỗi lần chạy test, test sẽ chậm, không ổn định (phụ thuộc mạng), và tốn phí giao dịch thật. Giải pháp: **mock** — thay phụ thuộc thật bằng đối tượng giả trong lúc test.

```python
from unittest.mock import Mock

def test_checkout_success():
    fake_repo = Mock()
    fake_repo.get_by_id.return_value = Order(id=1, total=100, status="pending")

    fake_payment = Mock()
    fake_payment.process.return_value = True     # giả lập thanh toán luôn thành công

    service = OrderService(order_repo=fake_repo, payment=fake_payment)
    result = service.checkout(order_id=1)

    assert result is True
    fake_payment.process.assert_called_once_with(100)   # kiểm tra hàm được gọi đúng cách
```

Đây chính là lý do Dependency Injection (mục 2.7) quan trọng — nếu `OrderService` tự tạo `MomoProcessor()` bên trong `__init__` thay vì nhận từ ngoài, bạn **không thể** thay nó bằng `Mock()` để test.

### 5.4. Cấu trúc 1 test tốt: Arrange – Act – Assert

```python
def test_something():
    # Arrange — chuẩn bị dữ liệu, điều kiện đầu vào
    account = BankAccount(owner="An", balance=100)

    # Act — thực hiện hành động cần test
    account.deposit(50)

    # Assert — kiểm tra kết quả đúng như mong đợi
    assert account.balance == 150
```

Mỗi test chỉ nên assert **một hành vi** — nếu test fail, tên test phải cho bạn biết ngay *cái gì* sai mà không cần đọc code bên trong.

### 5.5. Debugging — vượt qua thói quen chỉ dùng `print()`

`print()` không sai, nhưng senior có bộ công cụ rộng hơn:

```python
# logging thay vì print — có mức độ (level), có thể bật/tắt, ghi ra file, có timestamp
import logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

logger.debug("Chi tiết kỹ thuật, chỉ bật khi debug sâu")
logger.info("Sự kiện bình thường, ví dụ: user đăng nhập")
logger.warning("Có gì đó bất thường nhưng chưa phải lỗi")
logger.error("Lỗi xảy ra nhưng chương trình vẫn chạy tiếp được")
logger.critical("Lỗi nghiêm trọng, chương trình có thể sập")
```

Tại sao `logging` tốt hơn `print` trong code thật: bạn có thể tắt hết `debug`/`info` ở production chỉ bằng 1 dòng cấu hình, thay vì phải xóa từng `print()` rải rác khắp code.

**pdb** — debugger có sẵn trong Python, dùng khi cần dừng chương trình giữa chừng và "soi" trạng thái biến:

```python
def process_order(order):
    breakpoint()          # chương trình dừng ở đây, mở console tương tác
    total = calculate_total(order)
    return total
```

Khi chạy tới `breakpoint()`, bạn có console gõ lệnh: `n` (next line), `s` (step into hàm), `c` (continue), `p variable_name` (in giá trị biến), `l` (xem code xung quanh).

### 5.6. Đọc traceback — kỹ năng bị đánh giá thấp

```
Traceback (most recent call last):
  File "main.py", line 10, in <module>
    result = process(data)
  File "main.py", line 6, in process
    return data["key"] / count
KeyError: 'key'
```

Nguyên tắc đọc traceback: **đọc từ dưới lên** — dòng cuối cùng (`KeyError: 'key'`) là lỗi thực sự xảy ra. Các dòng phía trên là "đường đi" (call stack) dẫn tới lỗi đó, từ ngoài vào trong. Junior thường hoảng khi thấy traceback dài, nhưng 90% trường hợp bạn chỉ cần đọc dòng cuối + dòng ngay phía trên nó (nơi lỗi thực sự xảy ra trong code của bạn, không phải trong thư viện).

---

## PHẦN 6: PERFORMANCE & CONCURRENCY

### 6.1. Đo trước khi tối ưu — luật vàng

**Nguyên tắc quan trọng nhất trong tối ưu hiệu năng:** đừng đoán chỗ nào chậm — hãy đo. Donald Knuth có câu nói kinh điển: "tối ưu sớm là nguồn gốc của mọi tội lỗi" (premature optimization is the root of all evil). Junior thường tối ưu những chỗ không ảnh hưởng gì tới tốc độ thực tế, làm code phức tạp hơn mà không được gì.

```python
import timeit

# So sánh tốc độ 2 cách viết
time1 = timeit.timeit(lambda: [x**2 for x in range(1000)], number=10000)
time2 = timeit.timeit(lambda: list(map(lambda x: x**2, range(1000))), number=10000)
print(time1, time2)
```

```python
import cProfile

def slow_function():
    ...

cProfile.run("slow_function()")   # in ra hàm nào tốn thời gian nhất, gọi bao nhiêu lần
```

`cProfile` cho bạn thấy chính xác hàm nào đang là "nút thắt cổ chai" (bottleneck) thay vì đoán mò. Quy trình chuẩn: đo toàn bộ chương trình → tìm hàm chậm nhất → chỉ tối ưu hàm đó → đo lại để xác nhận có cải thiện.

### 6.2. `functools.lru_cache` — cache kết quả hàm miễn phí

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def fibonacci(n):
    if n < 2:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

fibonacci(35)   # nhanh — không tính lại những gì đã tính
```

Dùng khi: hàm **thuần túy** (pure function — cùng input luôn ra cùng output, không phụ thuộc trạng thái ngoài, không có side effect) và được gọi lặp lại nhiều lần với cùng tham số. Không dùng cho hàm có side effect (ghi file, gọi API thay đổi dữ liệu) vì cache sẽ khiến lần gọi thứ 2 trở đi "giả vờ" chạy nhưng thực ra không làm gì.

### 6.3. Độ phức tạp thuật toán (Big-O) — trực giác senior cần có

```python
# O(n²) — vòng lặp lồng nhau, chậm với n lớn
def has_duplicate_slow(lst):
    for i in range(len(lst)):
        for j in range(i + 1, len(lst)):
            if lst[i] == lst[j]:
                return True
    return False

# O(n) — dùng set để tra cứu O(1), nhanh hơn nhiều lần với n lớn
def has_duplicate_fast(lst):
    seen = set()
    for item in lst:
        if item in seen:
            return True
        seen.add(item)
    return False
```

Bạn không cần chứng minh Big-O bằng toán học mỗi ngày, nhưng senior luôn có phản xạ: "vòng lặp lồng vòng lặp trên dữ liệu lớn → cảnh giác", "tra cứu bằng list trong vòng lặp → cân nhắc set/dict", "dữ liệu có thể lên tới hàng triệu dòng → nghĩ tới generator/streaming thay vì load hết vào RAM".

### 6.4. GIL và khi nào threading/multiprocessing/asyncio phù hợp

Python có **GIL** (Global Interpreter Lock) — chỉ 1 thread Python được thực thi bytecode tại 1 thời điểm trong 1 process, bất kể máy có bao nhiêu core. Đây là điều khiến rất nhiều người từ ngôn ngữ khác bối rối khi mới học Python concurrency.

| Công cụ | Phù hợp với | Không phù hợp với |
|---|---|---|
| `threading` | I/O-bound (chờ mạng, chờ đọc file, chờ database) — thread khác chạy trong lúc chờ | CPU-bound (tính toán nặng) — GIL khiến không nhanh hơn |
| `multiprocessing` | CPU-bound (tính toán nặng, cần dùng nhiều core thật) | Task cần chia sẻ nhiều state — mỗi process có bộ nhớ riêng, tốn overhead |
| `asyncio` | I/O-bound, số lượng tác vụ chờ đợi RẤT LỚN (hàng nghìn kết nối mạng cùng lúc) | CPU-bound, hoặc code cần đơn giản mà không có nhiều I/O |

```python
# threading — phù hợp: gọi nhiều API cùng lúc (I/O-bound)
import threading

def fetch_url(url):
    response = requests.get(url)
    ...

threads = [threading.Thread(target=fetch_url, args=(url,)) for url in urls]
for t in threads: t.start()
for t in threads: t.join()

# multiprocessing — phù hợp: tính toán nặng, tận dụng nhiều core CPU
from multiprocessing import Pool

def heavy_computation(n):
    return sum(i * i for i in range(n))

with Pool(processes=4) as pool:
    results = pool.map(heavy_computation, [10_000_000] * 4)

# asyncio — phù hợp: hàng nghìn request I/O đồng thời, hiệu quả hơn threading nhiều lần
import asyncio
import aiohttp

async def fetch(session, url):
    async with session.get(url) as response:
        return await response.text()

async def main(urls):
    async with aiohttp.ClientSession() as session:
        return await asyncio.gather(*[fetch(session, url) for url in urls])

asyncio.run(main(urls))
```

**Trực giác senior cần có:** trước khi viết code concurrent, tự hỏi "bottleneck của tôi là chờ đợi (I/O) hay tính toán (CPU)?". Câu trả lời quyết định công cụ, và dùng sai công cụ (ví dụ threading cho CPU-bound) sẽ không nhanh hơn — thậm chí chậm hơn vì overhead quản lý thread.

---

## PHẦN 7: QUY TRÌNH LÀM VIỆC CHUYÊN NGHIỆP

### 7.1. Git — không chỉ `add`, `commit`, `push`

```bash
# Nhánh (branch) — không bao giờ code trực tiếp trên main/master
git checkout -b feature/them-tinh-nang-thanh-toan

# Commit nhỏ, thường xuyên, message rõ ràng
git commit -m "feat: thêm validate số dư trước khi rút tiền"
git commit -m "fix: sửa lỗi tính sai chiết khấu khi giỏ hàng rỗng"

# Trước khi tạo Pull Request — đồng bộ với main mới nhất
git fetch origin
git rebase origin/main       # giữ lịch sử commit gọn gàng, tuyến tính
```

Quy ước message commit senior hay dùng (Conventional Commits): `feat:` (tính năng mới), `fix:` (sửa lỗi), `refactor:` (tái cấu trúc không đổi hành vi), `test:` (thêm/sửa test), `docs:` (tài liệu), `chore:` (việc vặt như cập nhật dependency).

**Nguyên tắc commit:** mỗi commit nên là **1 thay đổi logic hoàn chỉnh** — không commit "fix typo" xen giữa 5 commit tính năng lớn (gộp lại), cũng không commit 1 lần cả chục file thay đổi không liên quan tới nhau (tách ra). Lý do: khi cần `git revert` hoặc `git bisect` tìm commit gây bug, lịch sử rõ ràng giúp việc này nhanh gấp nhiều lần.

### 7.2. Code review — kỹ năng 2 chiều senior đều giỏi

Khi review code người khác, senior tập trung vào (theo thứ tự ưu tiên):
1. **Đúng logic không?** — có case biên nào bị bỏ sót?
2. **Có test không?** — thay đổi này có được test bao phủ?
3. **Kiến trúc có hợp lý không?** — có vi phạm SOLID, có tách lớp đúng không?
4. **Đặt tên, style** — chỉ góp ý sau khi 3 điều trên ổn, và nên để linter tự động lo (mục 7.3) thay vì tranh cãi tay bo.

Khi nhận review, senior không phòng thủ — coi góp ý là cơ hội học, phản hồi ngắn gọn ("đã sửa", "mình giữ nguyên vì lý do X, bạn thấy sao?") thay vì tranh luận dài dòng qua lại nhiều vòng.

### 7.3. Linting & formatting tự động — đừng tranh cãi style bằng tay

```bash
pip install ruff black mypy

black .          # tự động format code theo 1 chuẩn thống nhất, không tranh cãi
ruff check .     # phát hiện lỗi, code smell, import thừa, biến không dùng...
mypy .           # kiểm tra type hint
```

Senior luôn cấu hình các công cụ này chạy tự động (qua `pre-commit` hook hoặc CI) để không ai phải tốn thời gian tranh luận "tab hay space", "dấu ngoặc kép hay đơn" trong code review — máy lo việc đó, con người tập trung vào logic.

```yaml
# .pre-commit-config.yaml — chạy tự động trước mỗi lần commit
repos:
  - repo: https://github.com/psf/black
    rev: 24.1.0
    hooks:
      - id: black
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.3.0
    hooks:
      - id: ruff
```

### 7.4. CI/CD cơ bản — tự động hóa kiểm tra chất lượng

```yaml
# .github/workflows/ci.yml — chạy tự động mỗi khi push code lên GitHub
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"
      - run: pip install -r requirements.txt
      - run: pytest --cov=myapp
      - run: ruff check .
      - run: mypy .
```

Ý nghĩa: mọi Pull Request đều tự động chạy test + kiểm tra style + kiểm tra type **trước khi** con người review — nếu có test fail hoặc lint lỗi, PR bị chặn merge. Đây là "lưới an toàn" giúp team lớn không ai vô tình đưa bug vào `main`.

### 7.5. Bảo mật cơ bản — những lỗi senior không bao giờ mắc

```python
# SAI NGHIÊM TRỌNG — SQL Injection
query = f"SELECT * FROM users WHERE username = '{username}'"   # username có thể chứa mã độc SQL
cursor.execute(query)

# ĐÚNG — dùng tham số hóa, thư viện tự escape an toàn
cursor.execute("SELECT * FROM users WHERE username = %s", (username,))
```

```python
# SAI — hardcode secret trong code, dễ bị lộ khi push lên Git public
API_KEY = "sk-abc123xyz..."

# ĐÚNG — đọc từ biến môi trường, không commit secret vào Git
import os
API_KEY = os.environ["API_KEY"]
```

```python
# SAI — tin tưởng input người dùng không kiểm tra
def get_file(filename):
    with open(f"/data/{filename}") as f:   # người dùng có thể truyền "../../etc/passwd"
        return f.read()

# ĐÚNG — validate, giới hạn phạm vi truy cập
import os

def get_file(filename):
    safe_path = os.path.join("/data", os.path.basename(filename))
    if not safe_path.startswith("/data/"):
        raise ValueError("Đường dẫn không hợp lệ")
    with open(safe_path) as f:
        return f.read()
```

Nguyên tắc cốt lõi: **không bao giờ tin tưởng input từ bên ngoài** (người dùng, API bên thứ 3, file upload) — luôn validate, luôn dùng cơ chế an toàn có sẵn của thư viện (parameterized query, escape HTML) thay vì tự ghép chuỗi tay.

---

## PHẦN 8: TƯ DUY GIẢI QUYẾT VẤN ĐỀ NHƯ SENIOR

Đây là phần **quan trọng nhất** của toàn bộ tài liệu — kỹ thuật (Phần 1-7) có thể tra cứu lại bất cứ lúc nào, nhưng tư duy là thứ khiến bạn tự ra quyết định đúng khi gặp tình huống chưa từng thấy trong sách.

### 8.1. Quy trình tiếp cận 1 bài toán mới

Junior thường mở editor và bắt đầu gõ code ngay khi nghe yêu cầu. Senior luôn đi qua các bước sau **trước khi gõ dòng code đầu tiên**:

1. **Làm rõ yêu cầu** — hỏi lại nếu mơ hồ. "Xóa user" nghĩa là xóa hẳn khỏi database, hay chỉ đánh dấu vô hiệu hóa (soft delete)? Câu hỏi sai lúc đầu tốn ít thời gian hơn nhiều so với code sai phải viết lại.
2. **Xác định input/output rõ ràng** — hàm nhận gì, trả về gì, trường hợp lỗi trả về gì (raise exception hay return None hay return giá trị mặc định)?
3. **Liệt kê case biên (edge case)** trước khi viết logic chính: input rỗng? input None? số âm? số cực lớn? dữ liệu trùng lặp? mạng bị ngắt giữa chừng?
4. **Vẽ/viết ra luồng xử lý bằng lời trước khi code** — nếu bạn không diễn đạt được bằng lời, code sẽ càng rối hơn.
5. **Viết code phiên bản đơn giản nhất chạy được trước** (tránh tối ưu sớm, tránh thiết kế "chống mọi trường hợp trong tương lai" khi chưa cần).
6. **Viết test cho case chính + case biên.**
7. **Refactor** sau khi đã chạy đúng — làm rõ tên biến, tách hàm nếu quá dài, xóa code thừa.

### 8.2. Trade-off thinking — không có giải pháp "hoàn hảo", chỉ có giải pháp phù hợp

Senior khi đứng trước 2 lựa chọn kỹ thuật không nói "cái nào đúng" mà nói "cái nào phù hợp với **ngữ cảnh này**". Vài trade-off kinh điển:

- **Tốc độ code vs tốc độ chạy:** dùng list đơn giản `O(n)` hay set phức tạp hơn chút nhưng `O(1)`? — phụ thuộc dữ liệu có lớn tới mức đáng lo hay không.
- **Chuẩn hóa (normalize) vs phi chuẩn hóa (denormalize) dữ liệu:** chuẩn hóa giảm trùng lặp nhưng tăng độ phức tạp truy vấn; phi chuẩn hóa ngược lại.
- **Generic/linh hoạt vs đơn giản/cụ thể:** thiết kế "chống mọi thay đổi trong tương lai" tốn thời gian ngay bây giờ để đổi lấy lợi ích *có thể* không bao giờ cần tới (YAGNI — "You Aren't Gonna Need It").
- **Nhất quán (consistency) vs khả dụng (availability)** trong hệ thống phân tán — đây là kiến thức nâng cao hơn nhưng senior luôn ý thức được: không có hệ thống nào tối ưu mọi tiêu chí cùng lúc.

**Câu hỏi senior luôn tự đặt ra:** "Nếu tôi chọn cách này, tôi đang đánh đổi cái gì để lấy cái gì? Đánh đổi đó có xứng đáng với bài toán cụ thể này không?"

### 8.3. YAGNI — đừng xây cho tương lai chưa tới

```python
# Junior: xây hệ thống "linh hoạt" cho tương lai chưa chắc xảy ra
class NotificationService:
    def __init__(self):
        self.strategies = {}   # "để sau này dễ thêm 10 loại notification khác"

    def register_strategy(self, name, strategy):
        self.strategies[name] = strategy

    def notify(self, name, message):
        self.strategies[name].send(message)

# Thực tế hiện tại chỉ cần gửi email — Senior viết đơn giản trước:
def send_notification(email, message):
    send_email(email, message)
# Khi THỰC SỰ cần thêm SMS, Slack... rồi mới refactor thành pattern phức tạp hơn
```

Senior không phải "lười" thiết kế linh hoạt — họ hiểu rằng thiết kế trừu tượng hóa quá sớm, dựa trên dự đoán sai về tương lai, thường phải viết lại từ đầu khi yêu cầu thật sự tới (mà yêu cầu thật luôn khác dự đoán). Refactor code đơn giản thành phức tạp khi cần dễ hơn nhiều so với gỡ bỏ 1 kiến trúc phức tạp sai hướng.

### 8.4. Đọc code người khác / codebase lớn — kỹ năng bị đánh giá thấp

Phần lớn thời gian của senior là **đọc code cũ**, không phải viết code mới. Chiến lược đọc hiệu quả:

1. **Đọc từ điểm vào (entry point)** — file `main.py`, route API, hoặc file được gọi trực tiếp khi chạy chương trình.
2. **Đọc theo luồng dữ liệu (data flow), không đọc từng file theo thứ tự alphabet** — theo dõi 1 request/1 input đi qua hệ thống như thế nào.
3. **Dùng "go to definition" và "find usages" của IDE** thay vì `Ctrl+F` tìm text — nhanh và chính xác hơn nhiều với codebase lớn.
4. **Đọc test trước khi đọc implementation** — test cho biết ngay "hàm này dùng để làm gì, input/output ra sao" nhanh hơn đọc logic bên trong.
5. **Không cần hiểu 100% mọi dòng** — chỉ cần hiểu đủ để tự tin sửa đúng chỗ cần sửa mà không phá vỡ chỗ khác.

### 8.5. Khi bị stuck — quy trình debug tâm lý, không chỉ kỹ thuật

- **Rubber duck debugging:** giải thích vấn đề thành lời (kể cả với... con vịt cao su) — quá trình diễn đạt bằng lời thường tự lộ ra chỗ sai trong tư duy.
- **Thu nhỏ vấn đề:** nếu code 200 dòng lỗi, viết lại 1 script 10 dòng tái hiện đúng lỗi đó — dễ debug hơn nhiều so với debug giữa 1 hệ thống lớn.
- **Đọc lại chính xác thông báo lỗi** — 80% trường hợp junior bị stuck vì đọc lướt traceback thay vì đọc kỹ dòng lỗi cuối cùng (mục 5.6).
- **Giới hạn thời gian tự mò:** nếu 30-45 phút không tiến triển, hỏi đồng nghiệp hoặc search — senior không cố "anh hùng" tự mò mãi, họ biết khi nào nên hỏi.

---

## PHẦN 9: LỘ TRÌNH LUYỆN TẬP THỰC CHIẾN

Đọc xong tài liệu này **không** khiến bạn thành senior — chỉ có thực hành lặp lại mới làm được điều đó. Dưới đây là lộ trình dự án gợi ý theo độ khó tăng dần, mỗi dự án cố tình thiết kế để buộc bạn áp dụng nhóm kỹ thuật cụ thể:

**Giai đoạn 1 — Củng cố nền tảng (áp dụng Phần 1-2):**
- Viết chương trình quản lý chi tiêu cá nhân (CLI) — dùng class, dataclass, xử lý file CSV, xử lý lỗi input người dùng đầy đủ (EAFP, custom exception).
- Viết lại chương trình trên nhưng tách rõ 3 lớp: `models` (dataclass), `services` (logic tính tổng/lọc), `cli` (giao diện dòng lệnh) — áp dụng mục 4.1.

**Giai đoạn 2 — Kỹ thuật nâng cao (áp dụng Phần 3):**
- Viết công cụ đọc log file lớn (dùng generator để không load hết vào RAM), tìm dòng chứa lỗi, thống kê theo giờ.
- Viết decorator `@retry` và `@timeit` tự dùng cho chính dự án của bạn (không copy từ tài liệu này, tự viết lại từ đầu).
- Viết context manager riêng để quản lý kết nối tới 1 API giả lập (mở kết nối → dùng → tự đóng dù có lỗi).

**Giai đoạn 3 — Kiến trúc thật (áp dụng Phần 4):**
- Xây REST API nhỏ (dùng FastAPI hoặc Flask) cho hệ thống quản lý đơn hàng — tách rõ `api/services/repositories`, áp dụng Dependency Injection cho payment processor giả lập.
- Refactor lại 1 dự án cũ của chính bạn (đã viết trước khi đọc tài liệu này) theo nguyên tắc SOLID — đây là bài tập giá trị nhất vì bạn thấy trực tiếp sự khác biệt trước/sau.

**Giai đoạn 4 — Testing & quy trình (áp dụng Phần 5, 7):**
- Viết test pytest đầy đủ cho dự án ở Giai đoạn 3 — bao gồm mock cho phần gọi API bên ngoài, đạt coverage > 80%.
- Setup GitHub Actions CI chạy test + ruff + mypy tự động cho repo của bạn.
- Tự tạo 1 Pull Request "giả" (branch riêng), tự review code chính mình sau 1 ngày để tách vai trò — bạn sẽ ngạc nhiên thấy nhiều điều muốn sửa hơn khi đọc lại với "con mắt reviewer".

**Giai đoạn 5 — Performance & Concurrency (áp dụng Phần 6):**
- Viết chương trình gọi 100 API cùng lúc bằng `asyncio` + `aiohttp`, so sánh thời gian với cách gọi tuần tự.
- Dùng `cProfile` tìm bottleneck trong 1 chương trình bạn viết trước đó, tối ưu, đo lại để xác nhận cải thiện thật (không đoán).

**Giai đoạn 6 — Tổng hợp:**
- Chọn 1 dự án open-source nhỏ trên GitHub (viết bằng Python, có sao nhưng không quá lớn), đọc code theo chiến lược ở mục 8.4, tìm 1 issue nhỏ (gắn nhãn "good first issue"), gửi Pull Request thật.

---

## PHẦN 10: CHECKLIST SENIOR & TÀI NGUYÊN HỌC TIẾP

### Checklist tự đánh giá — tick được hết là bạn đã có phản xạ senior

- [ ] Nhìn thấy `def f(x, lst=[])` là tự động nghi ngờ (mục 1.2)
- [ ] Biết chọn `list`/`tuple`/`dict`/`set` dựa vào ngữ nghĩa và độ phức tạp, không chọn theo thói quen (mục 1.3)
- [ ] Viết `except Exception: pass` khiến bạn thấy khó chịu, luôn bắt lỗi cụ thể (mục 1.8)
- [ ] Phân biệt được khi nào dùng kế thừa, khi nào dùng composition (mục 2.3)
- [ ] Biết dùng Dependency Injection để code dễ test (mục 2.7, 5.3)
- [ ] Phản xạ dùng generator khi xử lý dữ liệu lớn/luồng dữ liệu (mục 3.1)
- [ ] Hiểu decorator/context manager đủ để tự viết, không chỉ copy-paste (mục 3.2, 3.3)
- [ ] Tách được code thành layer rõ ràng thay vì viết hết vào 1 file (mục 4.1)
- [ ] Viết test trước khi coi task là "xong" (Phần 5)
- [ ] Đo hiệu năng bằng công cụ (`cProfile`, `timeit`) thay vì đoán mò (mục 6.1)
- [ ] Biết phân biệt bài toán I/O-bound và CPU-bound để chọn đúng công cụ concurrency (mục 6.4)
- [ ] Có quy trình rõ ràng trước khi code: làm rõ yêu cầu → case biên → code đơn giản → test → refactor (mục 8.1)
- [ ] Nói được "tôi chọn cách này vì đánh đổi X lấy Y, phù hợp với ngữ cảnh Z" thay vì "cách này đúng" (mục 8.2)

### Tài nguyên học tiếp (theo chủ đề)

- **Đọc tài liệu chính thức:** [docs.python.org](https://docs.python.org/3/) — senior đọc doc gốc thường xuyên hơn Stack Overflow, vì doc luôn chính xác và cập nhật.
- **Đào sâu Pythonic style:** sách *"Fluent Python"* của Luciano Ramalho — chi tiết nhất về dunder methods, iterator, decorator ở tầng sâu.
- **Clean Code & kiến trúc:** sách *"Clean Code"* (Robert C. Martin) — nguyên lý đặt tên, tách hàm, SOLID áp dụng được cho mọi ngôn ngữ.
- **Testing chuyên sâu:** tài liệu chính thức [pytest.org](https://docs.pytest.org/) — đọc phần fixture và parametrize kỹ.
- **Type hints nâng cao:** [mypy.readthedocs.io](https://mypy.readthedocs.io/)
- **Thực hành thuật toán/tư duy độ phức tạp:** LeetCode/HackerRank ở mức Easy-Medium, không cần Hard — mục tiêu là phản xạ Big-O, không phải thi đấu.
- **Đọc code thật:** chọn 1 thư viện Python nổi tiếng bạn hay dùng (`requests`, `httpx`, `click`) và đọc source code trên GitHub — đây là cách học kiến trúc thực chiến nhanh nhất.

---

### Lời kết

Tài liệu này cho bạn **bản đồ và các phản xạ ban đầu** — nhưng senior thực sự được hình thành qua **hàng trăm giờ code thật, hàng chục lần bị review "tơi tả" rồi sửa, hàng chục bug tự mình gỡ tới 2-3 giờ sáng rồi hiểu ra vấn đề**. Không có tài liệu nào thay thế được điều đó. Điều tài liệu này có thể làm là giúp bạn đi con đường đó **nhanh hơn và ít vòng vo hơn**, vì bạn đã biết trước những cái bẫy, những nguyên tắc mà bình thường phải tự vấp mới học được.

Hãy quay lại Phần 9, chọn 1 dự án ở Giai đoạn 1, và bắt đầu gõ code ngay hôm nay.








