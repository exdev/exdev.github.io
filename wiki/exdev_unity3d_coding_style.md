---
layout: page
title: Unity3D 编程规范
permalink: /wiki/exdev_unity3d_coding_style/
---

## 概括

以 FooBar 这个单词为例，我们简单概括:

+ 变量小写字母起头: `bool fooBar = false;`
+ 函数大写字母起头: `void FooBar ();`
+ 函数参数加以 `_` + 小写字母起头: `void MyFunction ( int _fooBar );`
+ public, private, protected, internal 写最前面
+ static, const, virtual, override 放中间, 多个混合顺序随意
+ Serialize 和 NonSerialize 的属性分段定义
+ 内嵌Class, Enum 的定义放最上方, 接着是 static 变量, 接着是 Serialized 变量, 接着是 Non-Serialized 变量, 接着是 static 函数, 最后是其他函数.

### 1) 变量定义

Unity3D 中变量的定义和 Inspector 显示以及 Serialize 挂钩。所以在定义中我们 **不采用** 匈牙利命名规则(m_, s_, g_)，而是直接以变量名的小写字母起头进行定义。

以 FooBar 为例，定义如下:

{% highlight csharp %}
public bool fooBar = false;
{% endhighlight %}

或者

{% highlight csharp %}
public bool foobar = false;
{% endhighlight %}

有时候我们会做出带 get, set 函数的属性定义，并带有 serialize 字段，这种情况下我们建议在变量末尾加 `_`

定义方法如下:

{% highlight csharp %}
[SerializeField] protected int fooBar_ = 10; 
public int fooBar { 
 get { return fooBar_; } 
 set { if ( fooBar_ != value ) { fooBar_ = value; Debug.Log("fooBar changed"); } } 
}
{% endhighlight %}

### 2) 函数定义

函数定义统一以大写字母起头，如一个名为FooBar的函数，定义为：

{% highlight csharp %}
public void FooBar () { ... }
{% endhighlight %}

函数中的参数，以 `_` + 小写字母起头参数定义。如参数名 “Do Update” 将定义为:

{% highlight csharp %}
public void FooBar ( bool _doUpdate ) { .... }
{% endhighlight %}

这样做可以避免掉参数和成员变量重名的问题，也方便代码阅读，明确哪些是外部参数

### 3) 修饰符定义

修饰符分两批

存取修饰符: public, protected, private, internal
其他修饰符: static, const, virtual, override, readonly ... 等
存取修饰符在定义是放在最前面，其他修饰符在存取修饰符之后。如:

{% highlight csharp %}
public static int fooBar = 0; protected void FooBar () { ... }
{% endhighlight %}

### 4) 大括号{}的书写位置

我们对 `{`, `}` 的书写定义没有强制要求，根据个人编程习惯来书写，有的人习惯写:

{% highlight csharp %}
public static int fooBar = 0; protected void FooBar () { ... }
if ( ... ) { 
    ... 
}
{% endhighlight %}

而也有喜欢书写:

{% highlight csharp %}
if ( ... ) 
{ 
    ... 
}
{% endhighlight %}

这都是可行的。但是我们推荐第一种紧凑型的写法，这是 Unix 的 C 书写标准，而且使得代码紧凑美观。

### 5) 空格符的书写

定义函数时，以下几种书写习惯都是可行的:

{% highlight csharp %}
void MyFunction ( int _a, int _b, int _c ) { ... } 

void MyFunction(int _a, int _b, int _c) { ... }
{% endhighlight %}

定义变量时，必须在 `=` 两边各空出一格以上

{% highlight csharp %}
int foobar = 0;
{% endhighlight %}

### 6) 定义顺序

定义顺序虽然没有强制要求，但是推荐按照以下顺序定义:

+ 内嵌结构如 struct, enum 和 class
+ 静态变量
+ public 或 serialized 变量
+ private 或 non-serialized 变量
+ 静态函数
+ Builtin 函数的重写 ( 所谓 Builtin 函数重写，是指继承自 Unity3D 的类中的可用函数，如 Start, Update, OnEnable 等)
+ 自定义的 public 函数
+ 自定义的 private, protected 函数

### 7) 间隔符

每份代码的开头处请放置(注: 86个`=`):

{% highlight csharp %}
// ======================================================================================
// File         : FileName.cs
// Author       : Your Name 
// Last Change  : 07/24/2012 | 14:10:05 PM | Tuesday,July (这里不做强制要求)
// Description  : 
// ======================================================================================
{% endhighlight %}

在所有的using namespace 声明前请放置 (注: 79个`/`):

{% highlight csharp %}
///////////////////////////////////////////////////////////////////////////////
// usings
///////////////////////////////////////////////////////////////////////////////
{% endhighlight %}

在一个 class 定义的上方请放置 (注: 79个`/`):

{% highlight csharp %}
///////////////////////////////////////////////////////////////////////////////
///
/// class 的定义说明
///
///////////////////////////////////////////////////////////////////////////////
{% endhighlight %}

在函数定义 或 property 定义的上方，请用分割说明 (注: 79个`/`)

{% highlight csharp %}
///////////////////////////////////////////////////////////////////////////////
// functions 或 properties
///////////////////////////////////////////////////////////////////////////////
{% endhighlight %}

每个函数的上方请放置 (注:66个`-`)

{% highlight csharp %}
// ------------------------------------------------------------------ 
// Desc: 
// ------------------------------------------------------------------ 
{% endhighlight %}

每个分隔注释的上方和下方都必须空出一行后方可书写代码
