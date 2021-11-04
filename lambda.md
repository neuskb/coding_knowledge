* 匿名函数

lambda表达式定义了一个匿名函数，可以捕获一定范围的变量在函数内部使用，一般是如下形式语法：
```
auto func = [capture] (params) opt -> ret { func_body; };
```
其中func是lambda表达式的名字，作为一个函数使用，capture是捕获列表，params是参数表，opt是函数选项（mutable之类），ret是返回值类型，func_body是函数体。
一个完整的lambda表达式：
```
auto func1 = [](int a) -> int { return a+1; };
auto func2 = [](int a) { return a+2; };
cout << func1(1) << " " << func(2) << endl;
```

如上代码， 很多时候lambda表达式返回值都很明显，c++11允许省略表达式的返回值定义。
lambda表达式允许捕获一定范围内的变量：
1. []不捕获任何变量
2. [&]引用捕获，捕获外部作用域所有变量，在函数体内当做引用使用
3. [=]值捕获，捕获外部作用域所有变量，在函数体内当做副本使用
4. [=, &a]值捕获外部作用域所有变量，按引用捕获a变量
5. [a]只值捕获a变量，不捕获其他变量
6. [this]捕获当前类中的this指针

lambda表达式示例代码：
```
int a = 0;
auto f1 = [=](){ return a; }; // 值捕获a
cout << f1() << endl;

auto f2 = [=]() { return a++; }; // 修改按值捕获的外部变量，error
auto f3 = [=]() mutable { reutrn a++; };
```

代码中的f2是编译不过的，因为我们修改了按值捕获的外部变量，其实lambda表达式就相当于一个仿函数，仿函数是一个有operator()成员函数的类对象，这个operator()默认是const的，所以不能修改成员变量，而加了mutable，就是去掉const属性。
