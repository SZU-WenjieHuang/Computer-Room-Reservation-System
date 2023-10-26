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

另一种常见的做法是将函数的声明放在头文件（.h 文件）中，然后在源文件（.cpp 文件）中包含这个头文件。这样，所有的函数都可以在整个源文件中被调用










