## 变量声明
### 明确类型声明
```dart
void main() {
  String s = 'John'; // 声明并给定初始值
  String s1; // 声明后赋值
  s1 = "xxx";
}
```
### Object类型声明
```dart
void main() {
  Object a = 'xxx'; // 可以是除null以外的任意类型的值
  a = 1;
  a.xxx(); // error，只能访问Object类型定义的属性和方法
}
```
### var关键字
```dart
void main() {
  var s = 'xxx'; // 根据初始化自动推导类型
  s = 1; // error，一旦确认类型，不可更改其类型

  var a; // 声明时未初始化，将等同于使用dynamic声明
  a = 1;
  a = 'xxx;
}
```
### dynamic关键字
```dart
void main() {
  // 可以为任意类型的值，包括null，默认值为null
  // 访问任意属性和方法都可以通过编译，可能会造成运行时异常
  dynamic a;
  a = 1;
  a = '1';
  a.xxx()
  print(a.xxx);
}
```

---

## 空安全
- 是什么
  - 空安全是 Dart 2.12 版本引入的一个重要特性，它帮助开发者在编译时就能够发现潜在的空引用错误，而不是在运行时才发现。

- 有什么用
  - 防止空引用异常：避免最常见的 NullPointerException 错误
  - 提高代码质量：使代码更加健壮和可维护
  - 提升开发效率：在编译时就能发现问题

- 代码体现
```dart
void main() {
  // dart默认启用空安全，意味着一个不可空变量必须赋值后才可访问
  String s = 'xxx';

  // 你可以显式的指定一个变量为可空变量
  String? s1;
  // 不能无条件的访问一个可空变量的属性或方法，可以添加空检查判断
  s1?.toLowerCase(); // 条件访问，不为null时调用，否则返回null
  s1!.toLowerCase(); // 非空断言，认定该变量这时一定不为null。如果为null，则会造成运行时错误
}
```

---

## late（延迟变量）
对于不可空变量而言，Dart可以检测到在使用之前何时将其赋过值，但有两个例外情况，dart无法检测
- 顶层变量
```dart
String name = 'xxx'; // 顶层变量，声明时必须给定初始值
late int age; // 无法在声明时确定值，可以添加late关键字
void main() {
  print(name);
  print(age); // error，使用时未赋值，则会造成运行时异常
}
```
- 实例属性
```dart
class Person {
  String name = 'xxx'; // 实例变量，声明时必须给定初始值
  late int age; // 无法在声明时确定值，可以添加late关键字
}
void main() {
  Person p = Person();
  print(p.name);
  print(p.age); // error，使用时未赋值，则会造成运行时异常
}
```
late变量、顶层变量、实例属性只会在使用时才会初始化
```dart
String getName() {
  print("getName");
  return 'xxx';
}
int getAge() {
  print("getAge");
  return 1;
}

String getHobby() {
  print("getHobby");
  return '唱跳rap';
}

String name = getName();
late int age = getAge();

void main() {
  late String hobby = getHobby();
  print('start');
  print(hobby);
  print(name);
  print(age); 
  print('end');
}
```

---

## 常量
const、final关键字都用于声明常量
- 常量只能被赋值一次，不可更改引用
```dart
void main() {
  final String hobby;
  hobby = '唱跳rap';
  hobby = '篮球'; // error

  const name = 'xxx'; // 可省略类型，自动推导
  name = 'yyy'; // error
}
```
- const只能声明编译器常量
```dart
void main() {
  final String time = DateTime.now().toString();
  const name = DateTime.now().toString(); // error
}
```
- const作用在类上时，需要加上static关键字
```dart
class Person {
  static const String name = 'xxx'; // const是编译期常量，如果不加static关键字，实例还未创建，属性如何确认值
}
```
- const还可用于创建常量值，常量值不可被修改，只在内存里存在一份
```dart
void main() {
  var a = const [1, 2, 3];
  var b = const [1, 2, 3];
  var c = [1, 2, 3];
  print(a == b); // true
  print(a == c); // false
  a[0] = 4; // runtime error，
}
```