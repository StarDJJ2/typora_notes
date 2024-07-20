# 1.基本介绍

[C++ vector容器详解_c++容器vector-CSDN博客](https://blog.csdn.net/qq_52324409/article/details/121000029?ops_request_misc=%7B%22request%5Fid%22%3A%22170478430816800182734373%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=170478430816800182734373&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-121000029-null-null.142^v99^pc_search_result_base4&utm_term=vector容器&spm=1018.2226.3001.4187)

2.向一个vector插入元素会使所有指向容器的迭代器，引用和指针失效。如何理解这段话？请给出解释和相关程序

当你在 `std::vector` 中插入或删除元素时，`vector` 可能需要重新分配它的内存以适应更多（或更少）的元素。当这发生时，指向 `vector` 原有元素的迭代器、引用和指针将会变得无效，因为它们仍然指向已经被释放或重分配的内存。 为了说明这个问题，我们来看一个简单的例子：

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> v = {1, 2, 3, 4, 5};

    // 指向第一个元素的迭代器
    std::vector<int>::iterator it = v.begin();

    // 插入一个新元素
    v.insert(v.begin(), 0);

    // 这时，迭代器it可能已经失效了
    // 在访问it时可能会导致未定义的行为
    std::cout << *it << std::endl;

    return 0;
}
```

在这个例子中，我们在 `vector` 的开始插入了一个新元素。这可能会导致 `vector` 重分配它的内存。当这发生时，我们原来保存的迭代器 `it` 就失效了，因为它指向的内存已经被重新分配了。当我们试图通过 `it` 访问元素时，结果是未定义的，可能会导致错误的输出或程序崩溃。

 为了防止这种问题，你应该尽量避免保存 `vector` 的迭代器、引用和指针，特别是在你需要修改 `vector` 的情况下。相反，你应该在需要时获取这些值，这样可以确保你的迭代器、引用和指针总是有效的。

# 2.

## 1.插入字符串

问题：

```cpp
vector<string> str = {"jin", "tian", "tianqi", "hen", "hao", "wo", "hen", "kai", "xin"};
```

如何在这个vector容器的"hao",和"wo"之间一次性插入3个字符串？

解答：

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

int main() {
	std::vector<std::string> str = {"jin", "tian", "tianqi", "hen", "hao", "wo", "hen", "kai", "xin"};

	// 要在"hao"和"wo"之间插入的字符串
	std::vector<std::string> to_insert = {"string1", "string2", "string3"};

	// 找到"hao"的位置
	auto it = std::find(str.begin(), str.end(), "hao");

	// 检查是否找到"hao"
	if(it != str.end()) {
		// 插入新的字符串
		// 这里+1是为了在"hao"的后面插入字符串
		str.insert(it + 1, to_insert.begin(), to_insert.end());
	}

	// 打印插入后的字符串列表
	for(const auto& s : str) {
		std::cout << s << " ";
	}
	std::cout << std::endl;

    return 0;
}
```

find() 是一个 STL 函数，它位于 <algorithm> 头文件下，它返回一个迭代器，指向范围内搜索元素的第一次出现。

用法:

```cpp
InputIterator find(
    InputIterator first, 
    InputIterator last, 
    const T& val);
```

其中，

InputIterator first- 搜索范围开始的迭代器
InputIterator last- 到搜索范围结束的迭代器
const T& val- 要搜索的数据类型 T 的值

原文链接：https://blog.csdn.net/wuxiaopengnihao1/article/details/127637725

## 2.删除字符串

一次性删除两个字符串间的代码：

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <algorithm>

int main() {
	std::vector<std::string> str = {"jin", "tian", "tianqi", "hen", "hao", "wo", "hen", "kai", "xin"};

	auto it_tian = std::find(str.begin(), str.end(), "tian");
	auto it_wo = std::find(str.begin(), str.end(), "wo");

	// 检查是否找到 "tian" 和 "wo"
	if(it_tian != str.end() && it_wo != str.end()) {
		// 删除 "tian" 和 "wo" 之间的字符串
		// 这里 +1 是为了不删除 "tian" 本身，it_wo 是为了不删除 "wo" 本身
		str.erase(it_tian + 1, it_wo);
	}

	// 打印删除后的字符串列表
	for(const auto& s : str) {
		std::cout << s << " ";
	}
	std::cout << std::endl;

    return 0;
}
```

以上代码可以更改为使用下标来进行删除操作吗？（这种方式更加复杂，没必要使用）

是的，可以使用下标进行删除操作。但是，`std::vector`本身并没有提供一种直接使用下标来删除元素的方法，所以你仍然需要使用`erase`成员函数进行删除。但是，联合使用下标和迭代器，你可以更改代码来达到相同的目的。

# 3.data()成员函数：

返回指向第一个元素的指针

```cpp
#include <iostream>
#include <vector>

int main ()
{
  std::vector<int> myvector (5);

  int* p = myvector.data();

  *p = 10;
  ++p;
  *p = 20;
  p[2] = 100;

  std::cout << "myvector contains:";
  for (unsigned i=0; i<myvector.size(); ++i)
    std::cout << ' ' << myvector[i];
  std::cout << '\n';

  return 0;
}
```

output:

```
myvector contains: 10 20 0 100 0
```

问题：为什么100在第四个位置？

回答：

因为指针p向前移动了一个位置，从当前的位置数第三个位置赋值为100
