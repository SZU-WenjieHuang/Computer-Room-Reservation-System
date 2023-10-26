# Computer Room Reservation System

### 01 接口
在 C++ 中，接口是一种特殊的抽象类，它只包含纯虚函数。纯虚函数是一种没有实现的虚函数，它在基类中被声明，并且被子类重写。接口定义了一种契约，它规定了实现接口的类必须提供哪些功能。

在 C++ 中，接口通过抽象类实现。一个没有任何实现并且全部由纯虚函数组成的类，就是一个接口。如下面的例子所示

```cpp
class IAnimal {
public:
    virtual ~IAnimal() {} // 虚析构函数，保证正确的析构过程
    virtual void eat() = 0; // 纯虚函数
    virtual void sleep() = 0; // 纯虚函数
    virtual void makeSound() = 0; // 纯虚函数
};
```

在这个例子中，IAnimal是一个接口，它定义了三个需要由其子类实现的纯虚函数：eat(), sleep(), 和 makeSound()。任何实现该接口的类都必须提供这三个函数的实现。

比如这样一个类：

```cpp
class Dog : public IAnimal {
public:
    void eat() override {
        cout << "Dog is eating." << endl;
    }

    void sleep() override {
        cout << "Dog is sleeping." << endl;
    }

    void makeSound() override {
        cout << "Dog says: Woof!" << endl;
    }
};
```

这个 Dog 类实现了 IAnimal 接口，提供了接口中所定义的所有纯虚函数的实现。

接口在设计模式和面向对象编程中扮演了重要的角色，它们可以用来定义行为的规范，提供了一种方式来保证某个类遵守特定的契约。

在 C++ 中，一个接口定义了一组函数，这些函数是那些实现（或称之为“继承”）该接口的类必须提供的。你可以把接口看作是一个契约或规范。任何类只要声明它实现了某个接口，那么它就必须提供该接口中所有函数的实现。

### 02 C++函数声明的顺序

在 C++ 中，函数的声明顺序是很重要的。如果你在一个函数中调用了另一个函数，那么被调用的函数必须在调用它的函数之前已经被声明。否则，编译器在编译时会报错，因为它无法找到你正在尝试调用的函数。

这是因为 C++ 采用了自上而下的编译方式，编译器在解析源代码时，是从上到下的顺序一行一行的解析，如果遇到了一个还未声明的函数，编译器就会报错。

例如，以下代码将无法编译：
```cpp
void functionA() {
    functionB();  // 编译错误：functionB 在此处尚未声明。
}

void functionB() {
    // 函数定义
}
```
为了解决这个问题，你可以在调用函数的函数之前先声明被调用的函数。通常，我们在源文件的开始部分声明所有的函数，这样就可以在文件的任何地方调用它们了。例如：
```cpp
void functionB();  // 函数声明

void functionA() {
    functionB();  // 正确：functionB 在此已经被声明了。
}

void functionB() {
    // 函数定义
}

```
在这个例子中，functionB 在 functionA 之前被声明，所以 functionA 可以成功地调用 functionB。

另一种常见的做法是将函数的声明放在头文件（.h 文件）中，然后在源文件（.cpp 文件）中包含这个头文件。这样，所有的函数都可以在整个源文件中被调用。

### 03 C风格的字符串和std::string

而关于std::string和C风格字符串的区别：

1-内存管理：std::string是C++的一个类，它自动管理内存。你不需要关心分配和释放字符串的内存。但是，对于C风格字符串，你需要手动分配和释放内存，否则可能导致内存泄漏或者越界访问。

2-安全性：std::string提供了很多方法（例如substr，replace，find等）来操作字符串，这些方法是安全的。但是，C风格字符串的操作（例如strcpy，strcat等）可能导致缓冲区溢出，如果使用不当，可能会引发安全问题。

3-性能：在某些情况下，C风格字符串的操作可能比std::string更快，因为它直接操作内存，没有额外的函数调用开销。但是，这通常需要更精细的内存管理和更多的代码。

4-兼容性：C风格字符串可以在C和C++中使用，而std::string只能在C++中使用。

以下的一些函数需要C语言标准库的传入:

strlen：返回字符串的长度。</br>
strcpy：复制一个字符串到另一个字符串。</br>
strcat：连接两个字符串。</br>
strcmp：比较两个字符串。</br>

相互转换:

从std::string到C风格字符串：你可以使用std::string的.c_str()成员函数。这个函数返回一个指向实际字符串内容的常量字符指针（const char*），并以空字符('\0')结束。这个返回的指针可以被用作创建C风格字符串。
```cpp
std::string str = "Hello, World!";
const char *cstr = str.c_str();
```
从C风格字符串到std::string：你可以直接使用C风格字符串来构造std::string。
```cpp
const char *cstr = "Hello, World!";
std::string str = cstr;
```
在这个例子中，std::string的构造函数接受一个C风格字符串作为参数，创建一个新的std::string对象，并复制C风格字符串的内容。






