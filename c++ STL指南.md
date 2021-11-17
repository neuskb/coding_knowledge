# c++ STL指南

## hash_map和map的使用场景
hash_map查找速度会比map快，属于常数级别，而map的查找速度是log(n)级别。
但是不一定常数就比log(n)小，hash函数还会耗时，所以当数据量达到一定程度就考虑用hash_map。但是对内存要求很严格，建议用map。

## vector底层原理

1. 底层是个动态数组，当空间不够装下数据时，会自动申请一片更大的空间（1.5倍或者2倍），然后把原来的数据拷贝到新的内存，接着释放原来的那片空间。当释放或者删除（vec.clear()）里面的数据时，其存储空间不释放，仅仅是清空了里面的数据。

2. reserve 和 resize 区别
reserve增加了vector的capacity，但是size没有改变，resize改变了vecotor的capacity，同时也增加了size。

3. size和capacity
size表示当前vector中有多少个元素（finish – start），而capacity函数则表示它已经分配的内存中可以容纳多少元素（end_of_storage – start）。

4. 元素类型可以是引用吗？
不行，vector底层实现 要求连续的对象排列，引用并非对象，没有实际地址，但是可以放指针。

5. 迭代器失效的情况
当插入一个元素到vector中，如果引起内存重新分配，那么指向原内存的迭代器全部失效。当删除容器中一个元素后，也会造成迭代器失效，erase方法会返回下一个有效迭代器，所以我们要删除某个元素时，需要it=vec.erase(it);

6. 正确释放vector的内存
* vec.clear() 清空内容，但是不释放内存
* vec1.swap(vec) 清空内容，且释放内存，得到一个全新的vec1
* vec.shrink_to_fit() 请求容器降低其capacity和size匹配，收缩到合适
* vec.clear();vec.shrink_to_fit(); 清空内容，且释放内存

7. vector 常用函数
```
vector<int> vec(10,100);        创建10个元素,每个元素值为100
vec.resize(r,vector<int>(c,0)); 二维数组初始化
reverse(vec.begin(),vec.end())  将元素翻转
sort(vec.begin(),vec.end());    排序，默认升序排列
vec.push_back(val);             尾部插入数字
vec.size();                     向量大小
find(vec.begin(),vec.end(),1);  查找元素
iterator = vec.erase(iterator)  删除元素
```

## list底层原理
1. list的底层是个双向链表，以节点为单位存放数据，节点的地址在内存中不一定连续，每次插入或删除一个元素，就配置或释放一个元素空间。
2. 适合大量插入和删除
3. 常用函数
```
list.push_back(elem)    在尾部加入一个数据
list.pop_back()         删除尾部数据
list.push_front(elem)   在头部插入一个数据
list.pop_front()        删除头部数据
list.size()             返回容器中实际数据的个数
list.sort()             排序，默认由小到大 
list.unique()           移除数值相同的连续元素
list.back()             取尾部迭代器
list.erase(iterator)    删除一个元素，参数是迭代器，返回的是删除迭代器的下一个位置
```

## deque底层原理
1. deque是个双向开口的连续线性空间，双端队列。
2. 常用函数
```
deque.push_back(elem)   在尾部加入一个数据。
deque.pop_back()        删除尾部数据。
deque.push_front(elem)  在头部插入一个数据。
deque.pop_front()       删除头部数据。
deque.size()            返回容器中实际数据的个数。
deque.at(idx)           传回索引idx所指的数据，如果idx越界，抛出out_of_range。
```

## 容器选择使用场景
1. vector可以随机获取元素，不用挨个查找，但是非尾部插入删除数据时，效率很低。
2. list不支持随机访问，适合插入和删除频繁的

## map的几种插入方式
1. insert函数插入pair数据
```
mapStudent.insert(pair<int, string>(1, "student_one")); 
```
2. insert函数插入value_type数据
```
mapStudent.insert(map<int, string>::value_type(1, "student_one"));
```
3. insert函数使用make_pair函数
```
mapStudent.insert(make_pair(1, "student_one"));
```
4. 数组方式插入
```
mapStudent[1] = "student_one";
```

