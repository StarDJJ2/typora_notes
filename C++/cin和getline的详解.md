# cin和getline的区别

```c++
#include <iostream>
#include <string>

int main() {
    using namespace std;
    string word;

    cout << "Enter a word or phrase: ";
    cin >> word; // 注意这里使用cin

    cout << "You entered: " << word << endl;

    return 0;
}
```

如果你运行这段代码，并输入 "Hello World"，那么你会发现它只打印出 "Hello"，因为 `cin` 在遇到空格、换行或者制表符的时候就会停止读取。

然后，我们看一下如何使用 `getline` 来读取输入：

```c++
#include <iostream>
#include <string>

int main() {
    using namespace std;
    string line;

    cout << "Enter a word or phrase: ";
    getline(cin, line); // 注意这里使用getline

    cout << "You entered: " << line << endl;

    return 0;
}
```

如果你运行这段代码，并输入 "Hello World"，那么你会发现它打印出 "Hello World"，因为 `getline` 会一直读取输入，直到遇到换行符（即按下 Enter 键）。

所以，如果你想读取包含空格的一行文本，你应该使用 `getline`。如果你只想读取连续的字符（不包含空格），那么你可以使用 `cin`。



# cin.getline( )和getline( )的区别

`cin.getline()` 和 `getline()` 都是用于从输入流中读取一行文本的函数，但它们有不同的用法和行为：

1. **cin.getline()**：
   - `cin.getline()` 是C++标准库中的函数，用于从标准输入流 `cin` 中读取一行文本（包括换行符 `\n`）并存储到指定的字符数组中。
   - 它的基本语法是：`cin.getline(char* buffer, int bufferSize)`，其中 `buffer` 是字符数组（或字符串指针），`bufferSize` 是字符数组的大小。
   - 例如：
     ```cpp
     char name[50];
     cin.getline(name, 50);
     ```
   - `cin.getline()` 会读取用户输入的一行文本，包括换行符，然后将该文本存储在 `name` 字符数组中。它会在输入行结束或达到指定的字符数上限时停止。

2. **getline()**：
   - `getline()` 是C++标准库中的另一个函数，用于从输入流中读取一行文本并存储到 `std::string` 类型的变量中。
   - 它的基本语法是：`getline(istream& is, string& str)`，其中 `is` 是输入流（如 `cin`），`str` 是存储文本的 `std::string` 变量。
   - 例如：
     ```cpp
     std::string name;
     getline(cin, name);
     ```
   - `getline()` 会读取用户输入的一行文本，但不包括换行符，然后将文本存储在 `name` 的 `std::string` 变量中。

总之，`cin.getline()` 用于将文本存储到字符数组中，而 `getline()` 用于将文本存储到 `std::string` 变量中。你可以根据需要选择其中一个函数来读取输入。使用 `std::string` 和 `getline()` 通常更方便和安全，因为它可以处理任意长度的输入行。

# getchar( )

`getchar()` 是C语言和C++中的函数，用于从标准输入流中获取一个字符



# C++中ch=cin.get()和cin.get(ch)等价吗

`ch = cin.get();` 和 `cin.get(ch);` 在功能上是等价的，都用于从输入流 `cin` 中获取一个字符，并将它存储在字符变量 `ch` 中。

`ch = cin.get();` 使用 `cin.get()` 方法来获取字符，然后将其分配给 `ch`。

`cin.get(ch);` 使用 `cin.get(char &ch)` 方法，其中 `ch` 是一个传递给函数的参数。该函数会从输入流 `cin` 中获取一个字符，并将其存储在参数 `ch` 中。

两者之间的差异主要在于函数调用和<font color='red'>返回值</font>。<font color='red'>`cin.get()` 返回获取的字符，而 `cin.get(ch)` 将字符存储在 `ch` 中，不返回字符本身。</font>

以下两个代码片段执行相同的操作，都从输入中读取一个字符，并将其存储在 `ch` 中：

```cpp
char ch;
ch = cin.get();
```

```cpp
char ch;
cin.get(ch);
```

你可以根据个人偏好选择使用哪一种形式。

# cin做判断语句

在C++中，输入运算符 `>>` 会尝试从输入流中读取数据并将其存储在目标变量中。如果输入流中的内容与目标变量的数据类型不匹配（例如，如果你尝试读取一个整数，但输入流中包含非数字字符），则输入操作会失败，并返回一个表示失败的状态。

这是因为C++的输入流（如 `cin`）在读取时会执行格式化操作，尝试将输入解释为与目标变量的数据类型匹配的值。如果无法解释输入为有效的目标数据类型，输入操作就会失败。

所以，当你尝试使用 `cin >> value` 读取一个 `double` 类型的值时，如果输入流中包含非数字字符，它无法正确解释为 `double` 类型，因此输入操作失败，并返回 `false`，表示读取失败。<font color='red'>（这里定义了value的类型为double）</font>

这种行为允许程序员在输入中发现非法或不符合预期的数据，并采取相应的措施，以确保程序的健壮性和正确性。

## 例子：

if (std::cin>>grades[i] == -1) 这样的条件语句为什么不成立

在 C++ 中，`std::cin` 返回一个引用到 `std::istream` 类型的对象。因此，`std::cin >> grades[i]` 的结果是一个 `std::istream` 对象，而不是 `grades[i]` 的值。

在你的条件语句中，你想检查输入的值是否为 `-1`，但由于优先级问题，`==` 操作符比 `>>` 操作符的优先级要高。因此，实际上这个条件会被解释为 `std::cin >> (grades[i] == -1)`，而不是你期望的 `std::cin >> grades[i]` 是否等于 `-1`。

为了解决这个问题，你可以使用括号明确指定优先级，确保先执行 `>>` 操作，然后再比较结果。修正后的条件语句如下：

```cpp
if ((std::cin >> grades[i]) == -1)
```

这样就会先执行 `std::cin >> grades[i]`，然后将结果与 `-1` 进行比较，以确保条件的正确性。
