# 1.cout.setf()

`cout.setf()` 是C++标准库中的一个函数，用于设置输出流（通常是标准输出流 `cout`）的格式标志。这些标志控制输出的各种格式选项，如浮点数的小数位数、对齐方式、基数等。`setf()` 允许你在输出之前配置这些选项。

基本的语法如下：

```cpp
cout.setf(format_flag);
```

其中，`format_flag` 是一个用于控制输出格式的标志，它可以是一个或多个位掩码（bitmask）的组合，用于设置不同的格式选项。

以下是一些常见的 `setf()` 格式标志示例：

- `ios::fixed`：设置输出为固定小数点表示法。
- `ios::scientific`：设置输出为科学计数法表示法。
- `ios::left`：设置文本输出左对齐。
- `ios::right`：设置文本输出右对齐。
- `ios::hex`：设置整数输出为十六进制格式。
- `ios::dec`：设置整数输出为十进制格式。
- `ios::oct`：设置整数输出为八进制格式。
- `ios::showpoint`：显示浮点数小数点和末尾的零。
- `ios::showpos`：显示正数的正号。

你可以使用 `setf()` 来灵活地控制输出流的格式，以满足你的需求。注意，`setf()` 可以与 `unsetf()` 一起使用，以取消设置某些格式标志。

例如，以下是使用 `setf()` 设置输出流的格式的示例：

```cpp
#include <iostream>
using namespace std;

int main() {
    double value = 123.456789;
    
    // 设置输出为固定小数点表示法，小数点后保留2位
    cout.setf(ios::fixed);
    cout.precision(2);
    
    cout << "Formatted value: " << value << endl;
    
    // 取消固定小数点表示法
    cout.unsetf(ios::fixed);
    
    // 恢复默认精度
    cout.precision(6);
    
    cout << "Default format: " << value << endl;
    
    return 0;
}
```

在上述示例中，`setf()` 用于设置输出为固定小数点表示法，并使用 `precision()` 设置小数点后的位数。后面使用 `unsetf()` 取消了固定小数点表示法的设置，并恢复了默认精度。

# 2.输出char str[20]类型的字符串

在C++中，你可以使用`std::cout`来输出字符数组（也就是C风格的字符串）。你只需要像输出其他变量一样，将数组名传递给`std::cout`。这是因为当字符数组作为`std::cout`的参数时，它会被当作一个C风格的字符串处理。 以下是一个例子： 

```cpp
#include <iostream> 
int main() 
{    
	char maker[40] = "Hello, World!";   
	std::cout << maker << std::endl;    
	return 0; 
}
```

 在这个例子中，`std::cout << maker`会输出`maker`数组中的字符串，直到遇到第一个空字符（'\0'）。这是因为C风格的字符串是以空字符作为结束标志的。 注意，如果你的字符数组不是一个正确的C风格的字符串（也就是说，它不以空字符结束），那么`std::cout`可能会输出超出数组范围的内存，这可能会导致未定义的行为。因此，当你处理字符数组时，你应该确保它是一个正确的C风格的字符串。