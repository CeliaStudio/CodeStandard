# 代码缩进规则
大括号需要换行，如下
```
if (someExpression)
{
    DoSomething();
}
else
{
    DoSomethingElse();
}
```
switch case 的缩进形式如下
```
switch (someExpression) 
{
 
   case 0:
      DoSomething();
      break;
 
   case 1:
      DoSomethingElse();
      break;
 
   case 2: 
      {
         int n = 1;
         DoAnotherThing(n);
      }
      break;
}
```
大括号永远是不可省略的，哪怕逻辑只有一行，如下
```
for (int i=0; i<100; i++) 
{ 
    DoSomething(i); 
}
```
# 空格的使用
正确的空格可以提升代码的可读性，在函数的参数后的逗号要接空格，如下
```
// 正确
Console.In.Read(myChar, 0, 1);
// 错误
Console.In.Read(myChar,0,1);
```
逻辑判断符号的左右都要加空格，如下
```
// 正确
while (x == y)
// 错误
while(x==y)
// 正确
if (x == y)
// 错误
if (x==y)
```
# 代码命名规则
- 不要定义形如m_xxx这样的成员变量，直接命名为xxx，如果声明了形如Xxx的property，可以定义同名的_xxx变量
- 对于成员变量，使用驼峰命名法
```
public int camelCasing = 1;
public string myName = "Tianyu";
```
- 对于参数，使用驼峰命名法
```
void Test(string childName, string fatherName)
{
}
```
- 对于局部变量，使用驼峰命名法
```
{
    var helloKitty = "Hello Kitty";
}
``` 
- 对于函数名、属性名、事件名、类名，使用PascalCasing
```
public class Renderer
{
    string Name 
    { 
        get; 
        set; 
    }

    string GetName()
    {
        return Name;
    }

    public event EventHandler NameChanged;
}
```
- 对于接口命名，要以I开头
```
interface IDrawble
{
}
```

# var关键字的使用

只有在能从变量声明的右侧明确的判断类型时，才可以使用var关键字来声明临时变量。

```
var var1 = "This is a string";
var var2 = 27;
var var3 = Convert.ToInt32(Console.ReadLine());
```
以上三种情况均能明确的从声明式的右侧部分看出声明类型，故可以使用var关键字。

var关键字可以帮助我们减少代码量，如
```
var instance1 = new ExampleClass();
ExampleClass instance2 = new ExampleClass();
```
在能从声明式右侧确定类型的时候,var帮助我们减少了代码量。

```
int var4 = ExampleClass.ResultSoFar();
```
以上情况无法明确的判断右边返回的类型，故不要使用var关键字，会影响代码可读性。

# 关于代码注释
- 注释要独立占一行，不要放到代码的行尾。
- 不要使用英文注释
- 在//后接一个空格，再开始写注释内容

```
// 以下声明将会创建一个query,但并不会运行这个
// query
```

# 关于Delegates
使用更简洁的形式去创建delegate类型的实例
```
public delegate void Del(string message);
public static void DelMethod(string str)
{
    Console.WriteLine("DelMethod argument: {0}", str);
}

public static Main()
{
    // 这种方式来声明委托的实例更简洁。
    Del exampleDel2 = DelMethod;
    // 这是通过构造函数的完整声明方式。
    Del exampleDel1 = new Del(DelMethod);
}
```

# 关于对象初始化
可以通过以下方式简化
```
// 更简洁和推荐的方式
var instance3 = new ExampleClass 
{
    Name = "Desktop", 
    ID = 37414, 
    Location = "Redmond", 
    Age = 2.3
};

// 传统的初始化方式
var instance4 = new ExampleClass();
instance4.Name = "Desktop";
instance4.ID - 37414;
instance4.Location = "Redmond";
instance4.Age = 2.3;
```

# 事件捕获

- 如果你去定义一个事件捕获，并且不打算在接下来去移除它，请使用lambda表达式
```
public Form2()
{
    // lambda表达式
    this.Click += (s, e) =>
    {
        Console.WriteLine(e.ToString());
    }
}

public Form1()
{
    // 传统形式
    this.Click += new EventHandler(form1Click);
}

void form1Click(object sender, EventArgs e)
{
    Console.WriteLine(e.ToString());
}
```
# 静态成员
调用静态成员变量或者方法时请使用类名显式的调用，同时定义在基类的静态成员请用基类的类名显式调用
```
public class BaseClass
{
    public static int name = 0;
} 

public class Foo ：BaseClass
{
    void Test()
    {
        Console.WriteLine(BaseClass.name.ToString());
    }
}
```
# 单个代码文件的结构
- 一个代码文件只允许存在一个public类,但是允许存在多个内部类
- 代码文件名需要和public类的名一致
- public成员要放在前，同时提供注释