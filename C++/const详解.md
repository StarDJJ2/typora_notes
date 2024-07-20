[【C++学习手札】-引用与内联函数以及C++中对const拓展详解（超详细！）_慕斯( ˘▽˘)っ的博客-CSDN博客](https://blog.csdn.net/weixin_64038246/article/details/132068536?spm=1001.2014.3001.5502)

[C++ const的用法详解_c++ const用法-CSDN博客](https://blog.csdn.net/weixin_56935264/article/details/125760242?ops_request_misc=&request_id=&biz_id=102&utm_term=const 指针&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-5-125760242.142^v99^pc_search_result_base4&spm=1018.2226.3001.4187)

1.疑问：

```cpp
#include <iostream>
#include <vector>

using namespace std;

bool find_int(vector<int>::const_iterator begin_, vector<int>::const_iterator end_, int n)
{
	// for(vector::const_iterator begin = begin_;begin != end_;++begin)
	while(begin_ != end_)
	{
		if( *begin_ == n) return true;
		++begin_;
	}

	return false;
}

int main()
{
	vector<int> vi{1,2,3,4,5,6};

	cout << boolalpha << find_int(vi.begin(), vi.end(), 0) << endl;

	return 0;
}

```

这段代码中的begin_为什么可以进行++的递增操作？他不是const iterator的数据类型吗？

回答：

在这段代码中，`begin_`是一个`const_iterator`类型的变量。这个`const_iterator`类型表示所指向的元素是常量，不能被修改。但这并不意味着迭代器变量`begin_`本身不能修改。你可以将其想象为一个指向常量的指针。 

例如，如果你有一个指向常量的指针，你不能通过该指针来修改其指向的值，但你可以改变指针本身的值，让它指向别的地方。同样，虽然通过`const_iterator`类型的迭代器不能改变元素的值，但你可以改变迭代器本身，也就是进行`++`或`--`等操作，让它指向其他元素。 

所以，`begin_++`实际上是在修改`begin_`的值，使其指向下一个元素，这是允许的。而如果你尝试去修改`begin_`所指向的元素的值，比如`*begin_ = 10`，就会导致编译错误，因为`const_iterator`类型的迭代器所指向的元素是不可修改的。