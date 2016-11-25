---
layout: page
title: Collections ( Tập hợp )
category: basics
order: 2
lang: vi
---

List, tuples, keywords, maps and functional combinators.

{% include toc.html %}

## Lists ( Danh sách )

Trong Elixir danh sách là một tập hợp của các giá trị, bao gồm nhiều kiểu dữ liệu khác nhau và có thẻ lặp lại.

```elixir
iex> [3.14, :pie, "Apple"]
[3.14, :pie, "Apple"]
```

lists trong Elixir được thực hiện như một link lists( danh sách liên kết ), điều này tức là việc truy câp độ dài của lists có độ phức tạp `O(n)`.
Do đó, việc thêm phàn tử vào đầu danh sách sẽ nhanh hơn là thêm vào cuối danh sách.

```elixir
iex> list = [3.14, :pie, "Apple"]
[3.14, :pie, "Apple"]
iex> ["π"] ++ list
["π", 3.14, :pie, "Apple"]
iex> list ++ ["Cherry"]
[3.14, :pie, "Apple", "Cherry"]
```


### List Concatenation ( Nối danh sách )

toán tử `++/2` được sử dụng để nối lists:

```elixir
iex> [1, 2] ++ [3, 4, 1]
[1, 2, 3, 4, 1]
```

trong định dạng của kỳ hiệu (++/2) sử dụng phía trên: trong elixir( erlang ) , tên của một hàm hay toán tử gồm có 2 thành phần: 
- tên hàm/toán tử 
- tham số ( arity )
trong đó tên hàm là tên hám/toán tử do người dùng cung cấp trong trg hợp trên là `++`. tham số ( arity ) là số lượng các tham số của hàm đó và đựơc phân cách nhau bởi kỳ tự `/`
trong vd trên `++/2` tức là toán từ có tên là `++` nhận 2 tham số.

### List Subtraction ( Trừ danh sách )

toán tử `--/2` được sử dụng để trừ danh sách. Bao gồm cả những giá trị không có trong danh sách trừ.

```elixir
iex> ["foo", :bar, 42] -- [42, "bar"]
["foo", :bar]
```

**Note:** It uses [strict comparison](../basics/#comparison) to match the values.

### Head / Tail (Đầu / Đuôi)

Khi sử dụng danh sách , ta thường sử dụng danh sách với đầu ( head )  và đuôi( tail ) của danh sách, trong đó đầu(head) là  đầu là phần tử đầu tiên của danh sách và đuôi( tail) là những phần tử còn lại của danh sách. Elixir cung cấp 2 phương thức để sử dụng cùng đầu ( head ) cuối ( tail ) của danh sách là `hd` và `tl`:
  x
```elixir
iex> hd [3.14, :pie, "Apple"]
3.14
iex> tl [3.14, :pie, "Apple"]
[:pie, "Apple"]
```

Ngoài 2 phương thức trên, bạn cũng có thể sử dụng khớp mẫu [pattern matching](../pattern-matching/) cùng vỡi toán từ '|' để tách danh sách ra thành đầu ( head ) và đuôi ( tail ); trong các bài học sau chúng ta sẽ tìm hiểu về khớp mẫu:

```elixir
iex> [h|t] = [3.14, :pie, "Apple"]
[3.14, :pie, "Apple"]
iex> h
3.14
iex> t
[:pie, "Apple"]
```

## Tuples (Bộ)

Bộ (Tuples ) là kiểu dữ liệu tương tự như danh sách ( list ) nhưng thay lưu trữ theo dạng liên kết thì nó đựoc lưu trữ lên tục trên bộ nhớ. Nhờ vào vậy việc truyên cập vào độ dài của Bộ (Tuples ) sẽ nhanh hơn nhưng sẽ khó đề chỉnh sửa. Nếu muốn chỉnh sửa thay vì truy cập vào phần từ như dạng danh sách thì ta phải sao chép lại toàn bộ vào trong bộ nhớ.  Ta sử dụng 2 cặp ngoặc {} để định nghia/quy ước: 

```elixir
iex> {3.14, :pie, "Apple"}
{3.14, :pie, "Apple"}
```

Chúng ta thuờng sử dụng Bộ ( Tuples ) như một cơ chế để trả về các thông tin của hàm ( functions ). Việc làm này sẽ hữu dụng khi dùng cùng với khớp mẫu( pattern matching ):

```elixir
iex> File.read("path/to/existing/file")
{:ok, "... contents ..."}
iex> File.read("path/to/unknown/file")
{:error, :enoent}
```

## Keyword lists ( Danh sach khóa )

danh sách khóa( keyword list) và map là những kiểu dữ liệu tập hợp ( từ điển ) trong Elixir.  Trong Elixir, danh sách từ khóa là một danh sách dặc biệt của bộ mà phần từ đầu tiên thì là một kiểu dữ liệu:

```elixir
iex> [foo: "bar", hello: "world"]
[foo: "bar", hello: "world"]
iex> [{:foo, "bar"}, {:hello, "world"}]
[foo: "bar", hello: "world"]
```

Thcó 3 dặc thủ nổi bật quan trọng của kiểu dữ liệu danh sách khóa mà ta cần biết::

+ Khóa là một atom
+ Khóa có trình tự
+ Khóa không phải duy nhất ( được phép lắp )

vì những lí do trên mà chứng ta thuờng sử dụng danh sách khóa như một tham số không bắt buộc để truyền vào hàm.

## Maps

Trong elixir kiểu dữ liệu maps là dữ liệu dưới dạng key-value hay còn đựoc gọi là kiểu dữ liệu từ điển. không giống với danh sách từ khóa , maps cho phép các khóa đựoc định nghĩa ở bất kỳ kiểu dữ liệu nào và không theo trình tự. maps được quy ứơc trong "%{}":

```elixir
iex> map = %{:foo => "bar", "hello" => :world}
%{:foo => "bar", "hello" => :world}
iex> map[:foo]
"bar"
iex> map["hello"]
:world
```

từ Elixir 1.2 trở lên , biến cũng có thể sử dụng như một từ khóa trong maps:

```elixir
iex> key = "hello"
"hello"
iex> %{key => "world"}
%{"hello" => "world"}
```

Nếu thêm một khóa lặp cùng giá trị vào trong maps. nó sẽ thay thế giá trị cũ bằng giá trị mới:

```elixir
iex> %{:foo => "bar", :foo => "hello world"}
%{foo: "hello world"}
```

Như chúng ta thấy từ kết quả output phía trên , có một cú pháp dặc biệt đối với maps nếu khóa của nó chỉ là atom:

```elixir
iex> %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}

iex> %{foo: "bar", hello: "world"} == %{:foo => "bar", :hello => "world"}
true
```

trong maps có hỗ trợ cú pháp update và truy cập vào các khóa riêng, đây là mọt trong những đặc tính thú vị của maps:

```elixir
iex> map = %{foo: "bar", hello: "world"}
%{foo: "bar", hello: "world"}
iex> %{map | foo: "baz"}
%{foo: "baz", hello: "world"}
iex> map.hello
"world"
```
