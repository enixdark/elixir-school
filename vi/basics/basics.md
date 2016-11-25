---
layout: page
title: Basics
category: basics
order: 1
lang: vi
---

Getting started, basic data types and basic operations.

{% include toc.html %}

## Getting Started

Basic ( Cơ bản )

kiểu dữ liệu cơ bản và cơ chế hoạt động:

### Cài đặt

Bạn có thể dựa theo chỉ dẫn trên trang chủ elixir-lang.org tr [Installing Elixir](http://elixir-lang.org/install.html) 

Sau khi cài đặt Elixir , bạn có thể dễ  dàng kiểm tra phiên bản elixir đã cài thông qua lệnh:
% elixir -v
Erlang/OTP {{ site.erlang.OTP }} [erts-{{ site.erlang.erts }}] [source] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Elixir {{ site.elixir.version }}

### Chế độ Tương Tác (Interactive Mode)

Elixir cung cấp `iex`, một chế độ tương tác thông qua shell , cho phép đánh giá, phân tích các biểu thức của Elixir mà người dùng nhập vào.

để bắt đầu, gõ lệnh `iex` trên terminal:
Erlang/OTP {{ site.erlang.OTP }} [erts-{{ site.erlang.erts }}] [source] [64-bit] [smp:4:4] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Interactive Elixir ({{ site.elixir.version }}) - press Ctrl+C to exit (type h() ENTER for help)
iex>

tiếp đó, hãy bắt đầu thử bằng cách gõ một số biểu thức đơn giản:

iex> 2+3
5
iex> 2+3 == 5
true
iex> String.length("The quick brown fox jumps over the lazy dog")
43

Đừng lo lắng nếu bạn không hiểu những biểu thức trên.

## Các kiểu dữ liệu cơ bản 

### số nguyên ( Integers )

```
iex> 255
255
```

hỗ trợ số nhị phân, thập phân, thập lục phân:

```
iex> 0b0110
6
iex> 0o644
420
iex> 0x1F
31
```

### Floats ( Số thực )
In Elixir, float numbers require a decimal after at least one digit; they have 64 bit doublốe precision and support `e` for exponent numbers:

Trong elixir, số thực được biểu diễn bằng một số thập phân và sau nó có ít nhất là một số. chúng sẽ có độ chính xác kép 64bit và hỗ trợ e cho số luỹ thừa:

```elixir
iex> 3.14
3.14
iex> .14
** (SyntaxError) iex:2: syntax error before: '.'
iex> 1.0e-10
1.0e-10
```

### Booleans

```elixir
iex> true
true
iex> false
false
```

### Atoms 

atom là kiểu dữ liệu mà biến không đổi với tên sử dụng chính là giá trị của chúng. Nếu bạn quen thuộc với ngôn ngữ ruby bạn sẽ thấy nó giống với symbols.

```elixir
iex> :foo
:foo
iex> :foo == :bar
false
```

Chú ý: `true` và `false` trong boolean tương đượng với atom `:true` và `:false`

```elixir
iex> true |> is_atom
true
iex> :true |> is_boolean
true
iex> :true === true
true
```

Chú ý: tên của modules trong elixir cũng có thể là atoms. ngoài cách sử dụng tiền tố `:` trước một tên thì cách viêt `MyApp.MyModule` cũng hợp lệ với atoms. thậm chí kể cả với trường hợp không có bất kỳ module nào được định nghĩa, khai báo.

```elixir
iex> is_atom(MyApp.MyModule)
true
```

atoms còn được sử dụng để tham chiếu tới các modules trong các bộ thư viên của erlang.


```elixir
iex> :crypto.rand_bytes 3
<<23, 104, 108>>
```

### (chuỗi) Strings

chuỗi trong elixir được đinh dạng theo chuẩn UTF-8 và được bao bọc trong dấu ngoặc kép.
```elixir
iex> "Hello"
"Hello"
iex> "dziękuję"
"dziękuję"
```

chuỗi trong elixir cũng hỗ trợ  tách ra nhiều dòng và tự động thoát các chuỗi theo trình tự:

  
```elixir
iex> "foo
...> bar"
"foo\nbar"
iex> "foo\nbar"
"foo\nbar"
```

Ngoài các kiểu dữ liệu cơ bản ra, elixir cũng xây dựng, cung cấp nhiểu kiểu dữ liệu phức tạp tới từ 
Erlang như Collections, Functions. các kiểu dữ liệu này sẽ được tìm hiểu ở những chương kế tiếp của bài học.

## cơ chế hoạt động cơ bản ( Basic Operations )

### Toán học (Arithmetic)

Elixir cung cấp các toán tử  số học như `+`, `-`, `*`,  và `/`. lưu ý toán tử  `/` luôn trả về  kết quả một số thực.

```elixir
iex> 2 + 2
4
iex> 2 - 1
1
iex> 2 * 5
10
iex> 10 / 5
2.0
```

nếu bạn cần thực hiện một phép chia lấy phần nguyên hay chia lấy phần dư. bạn có thể sử dụng 2 hàm có sẵn trong elixir:

```elixir
iex> div(10, 5)
2
iex> rem(10, 3)
1
```

### Boolean

Elixir cung cấp các toán tử  boolean như `||` (or) , `&&` (and) , and `!` (not). These support any types:

```elixir
iex> -20 || true
-20
iex> false || 42
42

iex> 42 && true
true
iex> 42 && nil
nil

iex> !42
false
iex> !false
true
```

- Trong trường hợp sử dụng các toán tử boolean bằng chứ thì tham số đầu tiên trong phép toan' phai là boolean (`true` hoặc `false`)  

```elixir
iex> true and 42
42
iex> false or true
true
iex> not false
true
iex> 42 and true
** (ArgumentError) argument error: 42
iex> not 42
** (ArgumentError) argument error
```

### Comparison ( So sánh )

- Tương tự với các ngôn ngữ khác , Elixir cũng cung cấp các toán tử so sánh quen thuộc: `==`, `!=`, `===`, `!==`, `<=`, `>=`, `<` and `>`.

```elixir
iex> 1 > 2
false
iex> 1 != 2
true
iex> 2 == 2
true
iex> 2 <= 3
true
```

Khi muốn so sánh chính xác giữa kiểu số nguyên( integers ) và số thực( floats ), sử dụng toán tử `===`:

```elixir
iex> 2 == 2.0
true
iex> 2 === 2.0
false
```

Một trong những đặc tính quan trong của Elixir là bất kỳ 2 kiểu dữ liệu nào khác nhau cũng đều có thể so sánh được với nhau, điều này sẽ rất hữu dụng dùng trong sắp xếp. 
Chúng ta không cần phải ghi nhớ tứ tự sắp xếp của các kiểu dữ liệu nhưng cần lưu ý: 

```elixir
number < atom < reference < functions < port < pid < tuple < maps < list < bitstring
```

Điều này có thể dẫn đến một vài trường hợp so sánh hợp lệ nhưng khá xa lạ so với các ngôn ngữ khác:

```elixir
iex> :hello > 999
true
iex> {:hello, :world} > [1, 2, 3]
false
```

### String Interpolation ( Nội suy chuỗi )

If you've used Ruby, string interpolation in Elixir will look familiar:

```elixir
iex> name = "Sean"
iex> "Hello #{name}"
"Hello Sean"
```

### String Concatenation

String concatenation uses the `<>` operator:

```elixir
iex> name = "Sean"
iex> "Hello " <> name
"Hello Sean"
```



