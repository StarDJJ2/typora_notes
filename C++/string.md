1.[【C++深入浅出】STL之string用法详解-CSDN博客](https://blog.csdn.net/m0_69909682/article/details/133812952?spm=1001.2100.3001.7377&utm_medium=distribute.pc_feed_blog_category.none-task-blog-classify_tag-18-133812952-null-null.nonecase&depth_1-utm_source=distribute.pc_feed_blog_category.none-task-blog-classify_tag-18-133812952-null-null.nonecase)

# 2.问题：为什么一个sring对象可以直接用cout打印出来，但是vector却不可以呢？

在C++中，`std::string`类型的对象可以直接使用`std::cout`打印，因为`std::string`类重载了输出流操作符`operator<<`。这意味着当你尝试用`std::cout`打印一个`std::string`对象时，`std::cout`知道如何将其内容转换成可以在控制台上显示的文本。

然而，标准库中的`std::vector`并没有重载输出流操作符`operator<<`，所以尝试直接用`std::cout`打印`std::vector`对象将不会编译通过。为了打印`std::vector`的内容，你需要手动遍历它的元素，并逐个打印它们。

如果你希望能够直接打印`std::vector`对象，你可以自己重载`operator<<`，例如：

```cpp
#include <iostream>
#include <vector>

template <typename T>
std::ostream& operator<<(std::ostream& os, const std::vector<T>& v) {
    for (const T& item : v) {
        os << item << ' ';
    }
    return os;
}
```

这样重载之后，你就可以直接打印`std::vector`对象了[1][4]。这个重载函数模板会遍历`std::vector`中的所有元素，并将它们一个接一个地发送到输出流中。

另一种方法是使用索引或迭代器手动遍历`std::vector`并打印每个元素，例如：

```cpp
std::vector<char> vec = {'H', 'e', 'l', 'l', 'o'};
for (const char& c : vec) {
    std::cout << c;
}
std::cout << std::endl;
```

或者使用索引：

```cpp
for (size_t i = 0; i < vec.size(); ++i) {
    std::cout << vec[i];
}
std::cout << std::endl;
```

这两种方式都可以在不重载`operator<<`的情况下，打印出`std::vector`中的元素[2][4].