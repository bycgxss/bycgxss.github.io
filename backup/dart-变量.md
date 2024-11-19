## 变量声明
### 明确类型声明
```dart
void main() {
  String name = 'John';
  String n;
  n = "xxx";
  print(name);
}
```
### var(自动推导)
```dart
void main() {
  var a = 'xxx'; // 变量a被推导为String类型
  a = 1; // error，一旦确认类型，不可更改
}
```
```dart
void main() {
  var a; // 变量a声明时未初始化，将等同于dynamic
  a = 1;
  a = 'xxx;
}
```

### Object类型声明
```dart
void main() {
  Object a = 'xxx';
  a = 1; // 变量a可以为任意类型，以为Object是所有类型的基类
  a.xxx(); // error，只能访问Object类型自身的属性或方法
  (a as int).abs(); // 当你确定该变量类型时，可以用类型断言，注意，有可能引发运行时异常
}
```

### dynamic
```dart
void main() {
  dynamic a = true;  // dynamic声明的变量可以为任意值，包括null
  a = 1;
  a = '1';
  print(a.xxx); // 且调用属性和方法会绕过静态类型检查
  print(a.xxx());
}
```

---

## 空安全
> 在dart2.12中引入了空安全特性，意味着所有类型都是非空的（即不可为null），除非显示的指定为可空类型
> 对一个非空类型的变量，在其初始化之前进行访问，会在编译阶段抛出异常
> 对一个可空类型的变量进行属性或方法调用前，请添加空检查判断
```dart
class Person {
  void say() {
    print("say");
  }
}

void main() {
  String s;
  print(s); // 编译报错，non-nullable，非空变量使用前必须初始化

  Person? p;
  p.say(); // 编译报错，变量有可能为null
  p!.say(); // 空断言，告诉编译器，变量p这里肯定不是空。有可能发生运行时异常
}
```