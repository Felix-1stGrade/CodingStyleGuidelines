# <center> 图为C/C++编程规范</center>



# 前言

## 规范制定说明

编程规范是对软件开发人员编写代码提出一些要求，以约束代码的使用和编写风格。希望通过规范来帮助或指导软件开发人员写出易读、可维护、可靠、可测试、高效、可移植的代码。

编程规范中的各种条目并不是毫无理由的提出，编程规范修订组分析总结了各种典型的编码问题，并参考业界编程规范，制定本规范。

## 代码总体原则

软件开发人员工作中有相当多的时间不是写新的代码，而是维护修改现有的代码，看代码的过程常常很痛苦，想一遍遍的问编写者的具体意图，希望别人写的代码逻辑清晰，注释意义明确。逻辑清晰的代码，意义明确的注释，这就是高质量代码的第一要求。
代码第一原则：易读。

## 术语定义

原则：编程时必须坚持的指导思想。

规则：编程时强制必须遵守的约定。

建议：编程时必须加以考虑的约定。

说明：对此原则/规则/建议进行必要的解释。

# 排版
好的排版不会直接带来新的功能或者性能的提高，但是好的排版却能提高阅读代码的效率，反之，排版差的代码会降低阅读理解的效率，例如，在复杂逻辑多层嵌套出现时，括号没有对齐可能导致阅读者理解错逻辑关系，又例如，有多层括号的表达式，操作符和操作数密密麻麻挤在一起，任谁也难以轻易看出括号的匹配关系。

## 通用要求

**【建议】  在代码编辑器中，将字体设置为等宽字体。**  

在代码编辑器中，建议设置为等宽字体，例如Consolas、Courier New等，便于代码对齐。  

**【建议】代码行缩进4个空格，并且不使用tab** 。

在不同的编辑器中，一个tab的宽度是不同的，如果tab和空格混用，会导致在一个编辑器中排版好的代码在另一个编辑器中打开时对不齐。  

例如，下图为在VS中编写好的代码  

![VS代码的对齐](.\picture\Snipaste_2019-01-11_16-32-58.png)  

在记事本中打开，代码就乱了 ![notepad代码的对齐](.\picture\Snipaste_2019-01-11_16-37-48.png)  查看VS中代码，显示空格和tab后
![VS代码的对齐](.\picture\Snipaste_2019-01-11_16-40-48.png)  可以看出在编写代码时tab和空格混用，在VS中一个tab宽度为4个空格，而在记事本中一个tab宽度为8个空格，所以导致记事本中显示的代码格式混乱。

**【规则】程序的分界符`{`和`}`应独占一行并且位于同一列，同时与引用它们的语句左对齐。**

```C++
void DoNothing(void)
{
    {
        {
            ;
            ;
        }
    }
    
    ;
    ;
    {
        ;
    }
}

```

**【规则】一行代码只做一件事。**

```C++
// 推荐
int minValue;
int maxValue;

if (value > maxValue)
{
    maxValue = value;
}

// 不推荐
int minValue, maxValue;

if (value > maxValue) maxValue = value;
```

**【建议】代码行不宜过长，可在低优先级操作符处拆分为多行，低优先级操作符放在新行行首，并且适当缩进。**

```C++
    vdcBusFlt = 0.99373651262477824541718973705429f * vdcBusFlt
              + 0.0062634873752217745321302366789951f * vdcBusBak;

    if((rectifier.state.runState == REC_NORMALRUN)
    && (charger.state.selfTestFinish == 0))
    {
        ；
    }
```

## 空行

恰当的空行可以使程序结构清晰，段落感强，有助于提高代码的阅读效率，反之，如果没有空行，程序密密麻麻，不容易理解程序功能，也使人眼花，过多的空行，来回翻页也累人。

**【规则】函数、数据类型、类等声明/定义结束后应有一行空行。 **

普通函数

```c++
float CalcRectangleArea(float length, float width)
{
    float area;
    
    area = length * width;
    return area;
}

```

类成员函数/类方法

```C++
float Box::CalcRectangleArea(void)
{
    return length * width;
}

```

类声明

```C++
class Box
{
public:
    float GetLength(void);
    void  SetLength(float length);
    float GetWidth(void);
    void  SetWidth(float width);
    float GetHeight(void);
    void  SetHeight(float height);
    
private:
    float m_length;
    float m_width;
    float m_height;
};

```

**【规则】不同的程序功能块，或者不同的逻辑段落之间必须有一行空行。**

**【建议】空行不宜过多，需要空行的地方空一行就可以。**

## 变量

**【规则】每一行只声明一个变量。**

一行声明多个变量不但不方便注释每一个变量的含义，而且可能混淆变量的类型。

比如同一行包含指针和非指针的声明，易导致代码阅读者理解错误或代码犯错。

```C++
int * counter, quantity; // quantity是int类型指针吗？
```

**【规则】数据类型和变量之间加一个空格，也可根据实际代码对齐的需求，增加空格数量，但是不要太多。**

```C++
// 根据实际情况对齐代码
int    value1;
float  value2;
int    value3;
double value4;
char   value5;
```

```C++
// 如果对齐需要添加的空格太多，所以此处不强制对齐
int value1;
struct Rectifier value2;
```



## 关键字

**【规则】关键字后应有一个空格。**

const、virtual、inline、case 等关键字之后要留一个空格，否则无法辨析关键字。if、for、while 等关键字之后建议留一个空格再跟左括号‘（’，以突出关键字。

## 运算符

**【规则】一元运算符和操作数之间不加空格。**

作用于一个运算对象的运算符是一元运算符，如取地址符&和解引用符*。一元运算符如下

| 运算符 | 名称         |
| ------ | ------------ |
| **!**  | 逻辑“非”     |
| **&**  | 取地址       |
| ~      | 按位取反     |
| **\*** | 指针取消引用 |
| **+**  | 正           |
| ++     | 递增         |
| **–**  | 负           |
| **––** | 递减         |

代码示例

```C++
    i++;
    pBox = &box;  // pBox是指向box的指针
```

**【规则】成员运算符`.`和` ->`前后不加空格。**

```c++
    box.length = 1.23;
    pBox = &box;  // pBox是指向box的指针
    pBox->width = 4.56;
```

**【建议】二元运算符和操作数之间加一个空格。**

作用于两个运算对象的运算符是二元运算符，如相等运算符==和乘法运算符*。

```C++
    rectangleArea = length * width;
```

**【规则】左括号`(`和右括号`)`与操作数之间不加空格。**

```c++
    average = (a + b + c) / 3;
```

**【规则】`[`之后和`]`之前不加空格。**

**【规则】`,`和`;`前面不加空格。**

**【建议】对于较长的表达式或语句，为了紧凑起见可以适当地去掉一些空格。**

```C++
    for (i=0; i<10; i++)
    {
        ;
    }

    if ((volt>LOW_VOLT) && (volt<HIGH_VOLT))
    {
        ;
    }

    root = (-b + sqrt(b*b-4*a*c)) / (2*a)；
```

## 结构体和类

**【建议】类的声明按照一定的顺序进行，`public`、`private`、`protected`等关键字不缩进。**

对外使用的接口或变量放前面，只在类内部使用的成员变量或成员函数放后面。

```C++
class Box
{
public:
    float length;
    float width;
    float height;

private:
    float xx;

public:
    float CalcVolume(void);

private:
    float DoNothing(void);
};
```

**【建议】结构体声明与类声明类似。**

```C++
struct Box
{
    float length;
    float width;
    float height;
};
```

## if-else

**【规则】*if*和*else*独占一行。**

**【规则】*if*和*else*后面的语句，无论有多少行，必须放在{}中。**

代码示例如下

```C++
    if (volt > 264.0f)
    {
        highVolt = 1;    
    }
    else if (volt < 186.0f)
    {
        lowVolt = 1;
    }
    else
    {
        highVolt = 0; 
        lowVolt  = 0;
    }
```



## switch-case

**【建议】*switch*必须有*default*分支。**

```C++
    switch()
    {
    case :
        ;
        ;
        break;
    case :
        ;
        ;
        break
    default:
        ;
        break;
    }
```

## 循环语句

循环语句包括for、while和do-while。

**【规则】*for*，*while*，*do*语句独占一行。**

**【规则】*for*，*while*，*do*后面的语句，无论有多少行，必须放在{}中。**

代码示例如下：

```C++
    for (int i=0; i<MAX_CNT; i++)
    {
        ;
        ;
    }
```

```C++
    while (i < MAX_CNT)
    {
        ;
    }
```

```
    do
    {
        ;
    } while(i < MAX_CNT)
```

## 函数

**【规则】函数名之后不留空格，紧跟左括号`(`。**

**【规则】函数定义结束后应有一行空行。 **

普通函数

```c++
float CalcRectangleArea(float length, float width)
{
    float area;
    
    area = length * width;
    return area;
}

```

类成员函数/类方法

```C++
float Box::CalcRectangleArea(void)
{
    return length * width;
}

```


# 命名

## 常见的命名法

目前常见的命名法有三种：驼峰命名法、unix like命名法和匈牙利命名法。

**驼峰命名法 **

驼峰命名法又分为大驼峰法和小驼峰法。

大驼峰命名首字母大写，并且后面的每个单词首字母大写，例如MaxValue，CurrentTime。大驼峰命名法又称为帕斯卡命名法。

小驼峰命名法和大驼峰类似，只是首字母小写，例如maxValue，currentTime。

**下划线命名法 **

此命名法所有单词字母均小写，并且用下划线分隔开，例如max_value，current_time。在UNIX/LINUX这样的环境，以及GNU代码中使用非常普遍。

**匈牙利命名法**

匈牙利命名法由1972年至1981年在施乐帕洛阿尔托研究中心工作的程序员查尔斯·西蒙尼发明。匈牙利命名法分为系统型匈牙利命名法和应用型匈牙利命名法。系统命名法与应用命名法的区别在于前缀的目的。

在系统匈牙利命名法中，前缀代表了变量的实际数据类型。例如：

- `lAccountNum`：变量是一个**长整数**（"l"）;
- `arru8NumberList`：变量是一个**无符号8位整型数组**（"arru8"）;
- `szName`：变量是一个**零结束字符串**（"sz"），这是西蒙尼最开始建议的前缀之一。

匈牙利应用命名法不表示实际数据类型，而是给出了变量**目的**的提示，或者说它代表了什么。

- `rwPosition`：变量代表一个**行**（"rw"）。
- `usName`：变量代表一个**非安全字符串**（"us"），需要在使用前处理。
- `strName`：变量代表一个包含名字的字符串（"str"）但是没有指明这个字符串是如何实现的。

西蒙尼建议的大多数前缀都是自然语义的，但不是所有。下面几个是来自原始论文的：

- `pX`是指向另一个**X**类型的指针，这包含非常少的语义信息。
- `d`是一个前缀表示两个值的差，例如，**dY**可能代表一个图形沿Y轴的距离，而一个仅仅叫做**y**的变量可能是一个绝对坐标。这完全是自然语义的。
- `sz`是一个无结束或零结束的字符串。在C中，这包含一些语义信息，因为C语言的**char\***类型的变量不确定是一个指向单个字符的指针，还是一个字符数组，或是一个零结束字符串。
- `w`标记一个变量是一个字。这基本上没有包含什么语义信息，因此可以被看作一种系统匈牙利命名法。
- `b`标记了一个字节，和w对比可能有一些语义信息，因为C语言中，只有**char**型（以及signed/unsigned char)是一个字节长的，这些类型有时候被用来保存数值或字符。这个前缀可以明确某个变量保存的是字符还是数值。

由于这种命名法通常使用小写字母开头用来助记，但是并没有对助记符本身作规定。有几种被广泛使用的习惯（见下面的示例），但是任意字母组合都可以被使用，只要它们在代码主体中保持一致就可以了。

在使用匈牙利应用命名法的代码中有时候也可能包含系统匈牙利命名法，即在描述被单独以类型方式定义的变量时使用。

**示例**

- `bBusy`：[布尔型]
- `cApples`：项目计数
- `dwLightYears`：双[字]（系统）
- `fBusy`：[布尔型]或[浮点型]
- `nSize`：[整型]（系统）或计数（应用）
- `iSize`：[整型]（系统）或索引（应用）
- `fpPrice`：[浮点数]
- `dbPi`：[双精度浮点数]（系统）
- `pFoo`：[指针]
- `rgStudents`：数组或范围
- `szLastName`：零结束字符串
- `u32Identifier`：无符号32位[整型]（系统）
- `stTime`：时钟结构
- `fnFunction`：函数名

对于指针和[数组]来说，它们实际上并不是数据类型，因此通常在助记符后面跟着实际元素的类型。

- `pszOwner`：指向零结束字符串的指针
- `rgfpBalances`：[浮点]值的数组

尽管匈牙利命名法可以被应用在任何程序设计语言和环境中，由于[微软]在C语言项目中，特别是在[Microsoft Windows]里的大量应用，使得匈牙利命名法的应用大量存在于和Windows相关的领域：

- `hwndFoo`：窗口句柄
- `lpszBar`：指向零结束字符串的长指针

这种命名法又是在[C++]中被扩展而包含变量的[作用域]，由一个下划线隔开：

- `g_nWheels`：全局名字空间的成员，整型
- `m_nWheels`：结构体／类成员，整型

**匈牙利命名法的优点 **

（其中一些只适用于系统匈牙利命名法）

- 不需要[集成开发环境]的支持，从名字中就可以看出变量的类型
- 拥有类似语义的多个变量可以在一个代码块中使用：dwWidth，iWidth，fWidth，dWidth
- 变量名在仅仅知道他们的类型时可以被轻易记住
- 可以使变量名更加一致
- 决定一个变量名的时候可以更机械化，更快
- 不合适的类型转换和操作可以在阅读代码的时候被检测出来，而不需要编译器的检测
- 在那些数字被当作字符串处理的基于字符串的语言中非常有用
- 在匈牙利应用命名法中，变量名确保不会犯以下错误：

​        heightWindow = window.getWidth()

- 在使用[动态类型语言]或完全无类型的语言编程时，关于类型的修饰可以更简化。这种语言一般不包含类型修饰（或者可选），因此唯一可以看出哪些类型是被允许的只有名字本身、文档以及通过阅读代码来明白它们在做什么。在这些语言中，包含对于变量类型的指示可能会有助于程序员。就像上面提到的，匈牙利命名法扩展了这样的语言（BCPL）。
- 在包含许多全局对象的复杂程序中（VB/Delphi Forms），拥有一个基本的前缀命名法可以简化在编辑器中查找组件的工作。按`btn<Ctrl-Space>`可以使编辑器弹出一个Button对象的列表。

**匈牙利系统命名法的缺点 **

- 匈牙利命名法在编译器做类型检查时是多余的。一个提供类型检查的语言在确定一个变量与其类型一致时，比人眼仅仅检查变量的用法与变量名一致要强大的多。
- 一些现代的[集成开发环境]，如[Visual Studio]在需要时可以显示变量类型，并且自动标记不匹配的类型。使用这种命名法完全没有必要。
- 向标识符添加类型标识导致标识符冗长；同时纵容相同主体名而不同类型的变量导致的歧义，开发人员无法从`sWidth`、`nWidth`、`fWidth`中了解这几个Width的用法区别，更好的写法可能是`string input`、`int width`、`float zoomedWidth`。
- 匈牙利命名法在被用作代表多个属性的时候会造成困惑，如 `a_crszkvc30LastNameCol`：一个常量[参数]，保存了一个[varchar]（30）类型的[数据库]列`LastName`的内容，而这列又是这个表的[主键]的一部分。
- 在代码更改后可能造成不一致。如果一个变量的类型改变了，不是变量名的修饰与新的类型不一致，就是变量名必须被改变。
- 由于变量名和类型捆绑在一起，因此不利于代码的移植。一个典型的众所周之的例子就是WPARAM类型，以及在许多Windows系统函数声明中使用的wParam参数。它原本是一个16位的类型，但是在后来的操作系统中被改成了32位或64位，但仍保留原来的名字（它实际的基础类型是UINT_PTR，即一个大小足够保存一个指针的无符号整型）。
- 大多数时候，看到一个变量就意味着知道了它的类型。但是，如果你不知道一个变量是干什么的，知道了它的类型也没什么帮助。

.NET Framework，微软新的软件开发平台，除了接口类型一般不适用匈牙利命名法。在.NET中，习惯在接口类型前放一个`I`（例如Windows Forms中的`IButtonControl`接口。）.NET Framework指导方针建议程序员不要用匈牙利命名法，但是没有指明不要用系统匈牙利命名法还是匈牙利应用命名法，或者是两者都不要用。与此对比，Java的标准库中连接口类型也不加前缀。

## 共性要求

**【规则】标识符命名应当简洁明确，可望文知意。**

标识符名称最好采用英文单词的组合，不要用汉语拼音，用词应当简单准确。

**【规则】标识符名称需满足*最小长度-最大信息量*原则。**

标识符名称需明确表达标识符的含义，一般来说，长的名称能更好的表达含义，但并不是越长越好。

**【规则】程序中不能出现仅仅依赖大小写区分的名称。**

仅仅依赖大小写区分的名称难以区分，容易混淆，例如，

```C++
int x;
int X;
```

## 文件命名

**【建议】文件命名采用全小写字母，不同单词可用下划线分隔。**

因为不同系统对文件名大小写处理会不同（如MS的DOS、Windows系统不区分大小写，但是Linux系统则区分），所以代码文件命名建议统一采用全小写字母命名。 

## 数据类型命名

**【规则】类以及自定义的数据类型名称采用大驼峰法。**

```c++
struct RectifierFaultGroup
{
    int softstartAbnormal;
    int busHighVolt;
    ......
};

class Rectifier
{
    ......    
};
```

## 常量命名

**【规则】常量名所有字母均大写，不管是宏常量还是*const*常量，不同单词间用下划线分隔。**

```C++
#define PI 3.14159265f
const int DAYS_IN_A_WEEK = 7;
```

## 变量命名

变量名最重要的要求是准确简洁地说明变量的用途含义。

**【规则】变量名采用小驼峰法，第一个字母小写，后面每个单词首字母大写，其余均小写。**

```C++
int points;
int maxValue;
float busVoltAvg; // 母线电压平均值
```

**【规则】变量的名称应该是“名词”或“形容词+名词”。**

```
int currentTime;
int time;
```

**【规则】用正确的反义词组命名具有互斥意义的变量。**

```c++
int minValue;
int maxValue;
```

**【规则】禁止单字母作为变量名，除*i，j，k*作为局部循环变量外。**

```C++
int a;   // 不好的命名
```

**【规则】禁止无意义的字母加数字命名。**

为了防止程序员偷懒，不肯为命名动脑筋而产生无意义的名字，因此禁止字母加数字的无意义命名。

```c++
int a1;   // 不好的命名
int a2;   // 不好的命名
int aaa;  // 不好的命名
int a123; // 不好的命名
```

**【规则】静态变量加前缀s_（static）。**

```C++
void GetObjectNumber(void)
{
    static int s_objectNumber = 0;
    ......    
}
```

**【规则】尽量不使用全局变量，如果必须有，那么全局变量加前缀g_（global）。**

**【规则】类的成员变量加前缀m_（member）。**

## 函数命名

**【规则】函数名采用大驼峰法。**

```C++
int GetCurrentTime(void)
{
    ......
}
```

**【规则】函数表示行为或动作，函数名应以动词开头，动词或动词+名词。**

例如函数名GetCurrentTime，获取当前时间Get（动词）+CurrentTime（名词，宾语）。

**【规则】用正确的反义词组命名具有互斥意义的函数。**

```C++
float GetTemperature(void)
{
    return m_temperature;
}

void SetTemperature(float temperature)
{
    m_temperature = temperature;
}
```




# 注释 #

**【原则】好的代码本身就是文档，不需注释即可理解。**

代码必须具有可读性，最好的代码本身就是文档，类型和变量命名意义明确比通过注释解释模糊的命名好的多。

**【原则】注释要简洁明确，且在功能、意图层次上解释，着重说明“为什么”，而不是逐行描述代码。**

为了别人理解代码，或者自己理解代码，需要合理添加注释。如何写注释，什么样的注释是好的注释，这是一个非常重要的问题。注释并不是写的越多越好，关键是要说明程序的功能，目的，这就要求注释主要讲为什么，而不是是什么，或者怎么做。

例如，下面的注释完全是多余的，除了浪费码字的时间，占用字符位置，还影响别人读代码。

```c
if (timer > 10)  // 如果timer大于10
{
    i++;  // i加一
}
```

对于代码实现逻辑晦涩或巧妙的代码需着重说明。

例如，下面对定点DSP实现除法代码的注释。

```C
avgCurrent = (totalCurrent * 1365)>>13; // 定点运算，平均电流=总电流/设备数量6台
```

**【规则】注释必须与代码同步更新。**

和代码不能同步的注释，不仅没有解释代码，起到帮助别人理解代码的作用，更多情况反而会误导读者，所以修改代码的同时必须更新相应的注释。

**【建议】单行注释使用//，多行注释使用/\* \*/ **

**【规则】注释/\* \*/不可嵌套使用。 **

**【规则】注释符号//、/\*、\*/与注释之间有一个空格。**

**【规则】注释应位于相应代码的上边相邻位置或右边。**

注释写在相应代码的右边或上面，紧邻代码，不要太远，例如行尾注释可在代码后空两格添加。注释位于代码上面时，需与相应代码缩进相同。

当连续多行代码都有注释时，可以适当调整注释位置使排版美观，可读性更好。

例如，注释位于代码右边。

```C
int voltOverLow;  // 电压过低标志
```

例如，注释位于代码上面。

```C
// 由于通信可能受到干扰，为避免误判通信失败，在此处连续5次异常，才判定通信失败。
if (commAbnormalCnt >= 5)
{
    commFail = true;
}
```

例如，连续多行代码都有注释

```C
struct RecFaultBits
{
    UINT16 fault                :1;  // BIT00 PFC故障汇总标志
    UINT16 hwSoftStartAbnormal  :1;  // BIT01 硬件软起异常
    UINT16 swSoftStartAbnormal  :1;  // BIT02 软件软起异常
    UINT16 dcVoltLow            :1;  // BIT03 直流母线低压
    UINT16 rsvd                 :12; // BIT04-15 保留
};
```

**【建议】文件头部注释应列出文件内容说明、作者姓名/工号、创建日期、版本号、版权信息、修改日志等。**

文件注释列出作者姓名工号便于后来的代码阅读者在有疑问时找到原作者沟通问题。

文件头部注释示例如下：

```C
/**
* @file       filename
* @brief      This is a brief description.
* @details    This is the detail description.
* @author     Felix Lu/000011
* @date       2019-02-14
* @version    V00A00D00
* @par Copyright (c) 西安图为电气技术有限公司. All rights reserved.
* @par History:
*             version: author, date, desc
*/
```

**【建议】函数声明处注释描述函数的功能、用法、输入输出参数返回值，以及对参数的限制和注意事项；函数定义处着重说明函数解决的问题和实现思路。**

示例如下

```C
/**
 * @brief   该函数的简要说明
 * @details 该函数的详述信息
 * @param a param描述参数
 * @return  return描述返回值
 * @note    note描述需要注意的问题
 */
```

**【建议】类数据成员、全局变量和常量应注释说明含义及用途。**

首先，变量名本身应该能够明确说明变量的用途。特定情况下，需要额外注释。

类数据成员（成员变量）应注释说明用途，或注意事项。

例如：

```C
class CUtility
{
public:
    float uin;     // 市电电压
    ...
private:
    float freqFlt;  // 市电频率滤波值，用于监控显示
    ...
};
```

全局变量和常量，应注释说明含义及用途。

例如：

```C
const float GRID_FREQ = 50.0f;  // 电网频率
```

**【规则】避免在注释中使用缩写，除非是业界通用或子系统内标准化的缩写。**

**【规则】同一产品统一注释风格。**

**【建议】不要在一行代码或表达式中间插入注释。**

**【建议】多行注释在合理的位置分行。**

**【建议】TODO注释后添加自己的姓名工号。**

对于临时的或者需要继续完善的实现代码，可添加TODO注释，并在后面括号()中写上你的名字工号，还可以加上冒号：说明待完成的工作。

例如

```
// TODO(Felix Lu/000011): 此处故障检测方法太灵敏，需优化。
```

**【建议】注释用自己熟悉的语言书写。**

如果英语水平不行，写注释与其用语句不通的英语，不如用信手拈来的汉语。

**【规则】注释采用Doxygen格式书写。**

Doxygen是一种开源跨平台的，以类似JavaDoc风格描述的文档系统，完全支持C、C++、Java、Objective-C和IDL语言，部分支持PHP、C#。注释的语法与Qt-Doc、KDoc和JavaDoc兼容。Doxygen可以从一套归档源文件开始，生成HTML格式的在线类浏览器，或离线的LATEX、RTF参考手册。

因此，在写注释时按照Doxygen的格式书写，便于生成代码参考手册。

## Doxygen注释种类

Doxygen注释的种类有多种

1.

```c++
/**
 * ....描述...
*/
```

2.

```c++
/*!
 * ....描述...
*/
或者
/*!
  ....描述...
*/
```

3.

```c++
///
///....描述...
///
或者
//!
//!....描述...
//!
```

### 文件注释 ###

```c
/**
* @file       filename
* @brief      This is a brief description.
* @details    This is the detail description.
* @author     Felix Lu/000011
* @date       2019-02-14
* @version    V00A00D00
* @par Copyright (c) 西安图为电气技术有限公司. All rights reserved.
* @par History:
*             version: author, date, desc
*/
```

### 函数注释 ###

```C
/**
 * @brief   该函数的简要说明
 * @details 该函数的详述信息
 * @param a 被测试的变量（param描述参数）
 * @param b 被测试的另一变量的描述
 * @return  测试结果（return描述返回值）
 * @see     Test()（本函数参考其它的相关的函数，这里作一个链接） 
 * @note    (note描述需要注意的问题)
 */
int DoNothing(int a, float b);
```

### 宏定义注释

```c++
/** Description of the macro */
#define XXXX_XXX_XX      ox7fffffff
```

或者

```c++
#define XXXX_XXX_XX      0  ///< Description of the macro.
```

### 结构体注释

```c++
/**
 * The brief description.
 * The detail description.
 */
typedef struct
{
    int var1;     ///< Description of the member variable
}XXXX;
```

或者

```c++
typedef struct Box
{
    double length; ///< The length of the box
    double width;  ///< The width of the box
    double height; ///< The height of the box
};
```

enum的各个值也如上注释。

### 变量注释

```c++
//! 简述
//! 详细描述
//! 从这里开始
int var; ///< 变量var说明
```

### 全局和静态变量注释

```c++
/**  Description of global variable  */
int g_xxx = 0;
static int s_xxx = 0; ///<  Description of static variable
```

### Doxygen指令说明 ###

| 指令       | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| @file      | 档案的批注说明。                                             |
| @author    | 作者的信息                                                   |
| @brief     | 用于class 或function的简易说明。eg：@brief 本函数负责打印错误信息串 |
| @param     | 主要用于函数说明中，后面接参数的名字，然后再接关于该参数的说明。eg：@param arg_name 参数说明 |
| @return    | 描述该函数的返回值情况。eg：@return 本函数返回执行结果，若成功则返回TRUE，否则返回FLASE |
| @retval    | 主要用于函数说明中，描述返回值类型和意义，所以后面要先接一个返回值，然后再放该返回值的说明。eg：@retval NULL 空字符串。 @retval !NULL 非空字符串。 |
| @note      | 注解                                                         |
| @attention | 注意                                                         |
| @warning   | 警告信息                                                     |
| @enum      | 引用了某个枚举，Doxygen会在该枚举处产生一个链接。eg：@enum CTest::MyEnum |
| @var       | 引用了某个变量，Doxygen会在该变量处产生一个链接。eg：@var CTest::m_FileKey |
| @class     | 引用某个类，格式：@class <name> [<header-file>] [<header-name>]。eg：@class CTest "inc/class.h" |
| @exception | 可能产生的异常描述。eg：@exception 本函数执行可能会产生超出范围的异常 |
|            |                                                              |



# 预处理



# 头文件




# 宏
**【规则】用宏定义表达式必须要有完备的括号。**

因为宏只是在预处理过程中进行简单的替换。

如下的定义都是有风险的

```c++
#define POWER(VOLT, CURRENT) VOLT*CURRENT
#define POWER(VOLT, CURRENT) (VOLT*CURRENT)
#define POWER(VOLT, CURRENT) (VOLT)*(CURRENT)
```

如果使用上面第一种宏表达式写法，在使用 POWER(a+b, c+d) 将会展开为 a+b * c+d，导致错误发生。

正确的写法应当是

```c++
#define POWER(VOLT, CURRENT) ((VOLT)*(CURRENT))
```

表达式整体以及参数都必须加上括号。

**【规则】宏定义的多条表达式应放在{}中。**

更好的方法是多条语句写成 do while(0) 的形式。

例如：有下面的宏定义表达式

```c++
#define UPDNLMT(var,max,min) (var)=((var)>=(max))?(max):(var); \
                             (var)=((var)<=(min))?(min):(var);
```

当如下方式使用时

```c++
for (int i=0; i<1000; i++)
    UPDNLMT(var,1024,-1024)
....
```

会导致循环中只有宏表达式的第一句执行。加上{}后可以解决这一问题。

```C++
#define UPDNLMT(var,max,min) {(var)=((var)>=(max))?(max):(var); \
                             (var)=((var)<=(min))?(min):(var);}
```

上面示例中，宏表达式可正常作用。但是，如果在调用宏表达式时后面加上分号，仍会出现错误

```c++
if (flag == 1)
    UPDNLMT(var,1024,-1024);
else
    UPDNLMT(var,10,-10);
```

编译器会提示编译错误。

所以使用do while(0)方式定义宏表达式更好一些。

**【规则】使用宏表达式时，参数不允许变化。**

```c++
#define SQUARE_AREA(r) ((r)*(r))
...
a = 1;
SQUARE_AREA(a++)
```

在宏使用时，看上去a自增一次，实际结果是a增加了两次变成3，因为宏展开后为  ((a++)*(a++))。

同时建议即使函数调用，也不要在参数中做变量变化操作，因为可能引用的接口函数，在某个版本升级后，变成了一个兼容老版本所做的一个宏，结果可能不可预知。

**【规则】不允许直接使用魔鬼数字**

使用魔鬼数字会导致代码难以理解。如果一个有含义的数字多处使用，一旦需要修改这个数值，需要逐个查找更改，代价惨重。使用明确意义的名称能增加信息，并能提供单一的维护点。

解决途径：对于局部使用的唯一含义的魔鬼数字，可以在代码周围增加说明注释，也可以定义局部const变量，变量命名自注释。

对于广泛使用的数字，必须定义const全局变量/宏；同样变量/宏命名应是自注释的。

0作为一个特殊的数字，作为一般默认值使用没有歧义时，不用特别定义。

**【建议】除非必要，应尽可能使用函数代替宏。**

 宏对比函数，有一些明显的缺点：

1.宏缺乏类型检查，不如函数调用检查严格。

2.宏展开可能会产生意想不到的副作用，如#define SQUARE(a) ((a) * (a)) 这样的定义，如果是SQUARE(i++)，就会导致i被加两次，如果是函数调用int square(int a) {return a * a;}则不会有此副作用。

3.以宏形式写的代码难以调试难以打断点，不利于定位问题。

4.宏如果调用的很多，会造成代码空间的浪费，不如函数空间效率高。 

示例：下面的代码无法得到想要的结果：

```C++
#define MAX_MACRO(a, b) ((a) > (b) ? (a) : (b))

int MaxFunc(int a, int b) 
{
    return ((a) > (b) ? (a) : (b));
}

int TestFunc()
{
    unsigned int a = 1;
    int b = -1;
    printf("MACRO: max of a and b is: %d\n", MAX_MACRO(++a, b));
    printf("FUNC : max of a and b is: %d\n", MaxFunc(a, b));
    return 0;
}
```

上面宏代码调用中，结果是(a < b)，所以a只加了一次，所以最终的输出结果是：

```
MACRO: max of a and b is: -1
FUNC : max of a and b is: 2
```

**【建议】常量建议使用*const*定义代替宏。**

  “尽量用编译器而不用预处理”，因为#define经常被认为好象不是语言本身的一部分。看下面的语句：

```C++
 #define ASPECT_RATIO 1.653 
```

编译器会永远也看不到ASPECT_RATIO这个符号名，因为在源码进入编译器之前，它会被预处理程序去掉，于是ASPECT_RATIO不会加入到符号列表中。如果涉及到这个常量的代码在编译时报错，就会很令人费解，因为报错信息指的是1.653，而不是ASPECT_RATIO。如果ASPECT_RATIO不是在你自己写的头文件中定义的，你就会奇怪1.653是从哪里来的，甚至会花时间跟踪下去。这个问题也会出现在符号调试器中，因为同样地，你所写的符号名不会出现在符号列表中。解决这个问题的方案很简单：不用预处理宏，定义一个常量：

```c
const double ASPECT_RATIO = 1.653;
```

 这种方法很有效，但有两个特殊情况要注意。首先，定义指针常量时会有点不同。因为常量定义一般是放在头文件中（许多源文件会包含它），除了指针所指的类型要定义成const外，重要的是指针也经常要定义成const。例如，要在头文件中定义一个基于char*的字符串常量，你要写两次const：

```
const char * const authorName = "Scott Meyers";
```

**【建议】宏定义中尽量不使用*return*、*goto*、*continue*、*break*等改变程序流程的语句**

 如果在宏定义中使用这些改变流程的语句，很容易引起资源泄漏问题，使用者很难自己察觉。 

示例：在某头文件中定义宏CHECK_AND_RETURN：

```
#define CHECK_AND_RETURN(cond, ret) {if (cond == NULL_PTR) {return ret;}}
```

 然后在某函数中使用(只说明问题，代码并不完整)：

```c
pMem1 = VOS_MemAlloc(...); 
CHECK_AND_RETURN(pMem1 , ERR_CODE_XXX) 
pMem2 = VOS_MemAlloc(...); 
CHECK_AND_RETURN(pMem2 , ERR_CODE_XXX) /*此时如果pMem2==NULL_PTR，则pMem1未释放函数就返回了，造成内存泄漏。*/
```

所以说，类似于CHECK_AND_RETURN这些宏，虽然能使代码简洁，但是隐患很大，使用须谨慎。

# 变量

**【规则】定义变量的同时初始化变量，避免忘记初始化。**

```C++
int month = 1;
int day = 1;
```

**【规则】程序中不要出现名称完全相同的全局变量和局部变量。**

**【建议】变量的名称要与实际用途相符。不要一个变量，多种用途。**

# 常量

常量的值在程序运行期间恒定不变，可以用#define定义宏常量，也可以用const定义常量。

如果不使用常量，直接在程序中填写数字或字符串，将会有什么麻烦？  

1. 程序的可读性（可理解性）变差。程序员自己会忘记那些数字或字符串是什么意思，用户则更加不知它们从何处来、表示什么。  

2. 在程序的很多地方输入同样的数字或字符串，难保不发生书写错误。  

3. 如果要修改数字或字符串，则会在很多地方改动，既麻烦又容易出错。  

 **【规则】用含义直观的常量来表示在程序中多次出现的数字或字符串。**

```C++
#define PI 3.1415926f
const float HIGH_VOLT 400.0f
```

**【规则】如果某一常量与其它常量密切相关，应在定义中包含这种关系，而不应给出一些孤立的值。**

```C++
const float RADIUS = 100; 
const float DIAMETER = RADIUS * 2;
```

**【规则】需要对外公开的常量放在头文件中，不需对外公开的常量放在实现文件的头部。为便于管理，可以把不同模块的常量集中存放在一个公共的头文件中。**

**【建议】使用`const`常量代替宏常量。**

const常量有数据类型，而宏常量没有，编译器可以对const常量进行类型安全检查。集成化的调试工具可以对const常量进行调试，但不能对宏常量调试。

**【建议】类中的常量用枚举实现。**

枚举常量不会占用对象的存储空间，它们在编译时被全部求值。枚举常量的缺点是：它的隐含数据类型是整数，其最大值有限，且不能表示浮点数（如 PI=3.14159）。 

```c++
class A 
{
    enum { SIZE1 = 100, SIZE2 = 200}; // 枚举常量 
    int array1[SIZE1];
    int array2[SIZE2]; 
};
```



# 表达式

C/C++中有数十个运算符，优先级与结合律如下表。注意一元运算符 + - * 的优先级高于对应的二元运算符。

![运算符的优先级与结合律](.\picture\运算符的优先级与结合律.png)

**【规则】如果代码中的运算符比较多，用`()`来确保计算顺序，避免使用默认的优先级。**

```C++
    root = (-b + sqrt(b*b-4*a*c)) / (2*a)；  // 求根公式
        
    value = 2;
    result = value >> 2 + 1;  // ?
```

**【建议】不要编写过于复杂的复合表达式。**

# 语句

## if

**【规则】不可将布尔型变量与TRUE、FALSE或者1、0进行比较。**

根据布尔类型的语义，规定0为FALSE，非零为TRUE ，TRUE 的值究竟是什么并没有统一的标准。例如 Visual C++ 将 TRUE 定义为 1，而 Visual Basic 则将 TRUE 定义为-1。

```C++
bool flag;

if (flag) // 正确
{}
if (！flag) // 正确
{}
// 以下都是不良风格
if (flag == 0)
{}
if (flag == 1)
{}
if (flag == TRUE)
{}
if (flag == FALSE)
{}
```

**【规则】不可将浮点变量用`==`或`!=`与任何数字做比较。**

float和double变量都有精度限制，所以必须避免相等或不等的比较，都需要转化为`>=`或`<=`的比较。

例如，需要比较变量value是否为0，应该转化为下面代码

```C++
    #define EPS 0.00001f // 允许误差

    if ((value >= -EPS) && (value <= EPS))
    {}
```

**【规则】判断指针变量是否为空，应将指针变量与NULL进行相等或不等的比较，而不是与0比较。**

```C++
    if (ptr == NULL) // 正确写法
    {}
    
    if (ptr == 0) // 错误写法
    {}
```

**【规则】必须考虑条件是否完整覆盖。**

**【建议】为了避免将`==`误写为`=`，可将常量放到`==`的左边。**

```C++
    if (value == 1) // 正确代码
    {}
    
    if (value = 1)  // 误将“==”写为“=”，编译器不能发现错误
    {}
    
    if (1 = value)  // 误将“==”写为“=”，编译器可以发现错误
    {}
```

## switch

**【规则】每一个case分支的结尾必须有break语句，否则匹配一个case后会继续执行下一个case分支，直到遇到break语句或者switch结束（除非编码的目的本就是多case连续执行）。**

```C++
    switch (value)
    {
    case 'A':
        DoA();
        break;
    case 'B':   // 如果value='B'，将会执行DoB()和DoC()。
        DoB();
    case 'C':
        DoC();
        break;
    default:
        break;        
    }
```

**【规则】switch必须有default分支。**

## 循环语句

**【规则】重复的代码如果可用循环实现，则必须用循环实现。**

```C++
    // 数组初始化	
    warn[0].word1.all = 0;
	warn[0].word2.all = 0;
	warn[1].word1.all = 0;
	warn[1].word2.all = 0;
	warn[2].word1.all = 0;
	warn[2].word2.all = 0;
	warn[3].word1.all = 0;
	warn[3].word2.all = 0;
	warn[4].word1.all = 0;
	warn[4].word2.all = 0;
	warn[5].word1.all = 0;
	warn[5].word2.all = 0;
	warn[6].word1.all = 0;
	warn[6].word2.all = 0;
	warn[7].word1.all = 0;
	warn[7].word2.all = 0;
	warn[8].word1.all = 0;
	warn[8].word2.all = 0;
	warn[9].word1.all = 0;
	warn[9].word2.all = 0;
	warn[10].word1.all = 0;
	warn[10].word2.all = 0;
	warn[11].word1.all = 0;
	warn[11].word2.all = 0;
	warn[12].word1.all = 0;
	warn[12].word2.all = 0;
	warn[13].word1.all = 0;
	warn[13].word2.all = 0;
	warn[14].word1.all = 0;
	warn[14].word2.all = 0;
	warn[15].word1.all = 0;
	warn[15].word2.all = 0;
    // 改为循环实现
    for (int i=0; i<16; i++)
    {
        warn[i].word1.all = 0;
	    warn[i].word2.all = 0;
    }
```

**【规则】禁止在for循环体内修改循环变量，防止for循环失控。**

**【建议】在多重循环中，如果有可能，应将最长的循环放在最内层，最短的循环放在最外层，以减少CPU跨切循环层的次数。**

```C++
// 低效率：长循环在最外层
for (row=0; row<100; row++) 
{ 
    for (col=0; col<5; col++) 
    { 
        sum = sum + a[row][col]; 
    } 
}
// 高效率：长循环在最内层
for (col=0; col<5; col++) 
{ 
    for (row=0; row<100; row++) 
    { 
        sum = sum + a[row][col]; 
    } 
}
```

**【建议】如果循环体内存在逻辑判断，并且循环次数很大，为了提高效率，可考虑将逻辑判断移到循环体的外面。**

下面代码示例1比示例2多执行了 N-1 次逻辑判断，并且由于前者每次循环进行逻辑判断，打断了循环“流水线”作业，使得编译器不能对循环进行优化处理，降低了效率。如果 N 非常大，最好采用示例2的写法，可以提高效率。如果 N 非常小，两者效率差别并不明显，采用示例1的写法比较好，因为程序更加简洁。 

```C++
// 示例1：效率低但程序简洁
for (i=0; i<N; i++) 
{ 
    if (condition)
    {
        DoSomething();
    }     
    else
    {
        DoOtherthing();
    }    
}
// 示例2：效率高但程序不简洁
if (condition) 
{ 
    for (i=0; i<N; i++)
    {
        DoSomething(); 
    }        
} 
else 
{ 
    for (i=0; i<N; i++)
    {
        DoOtherthing();
    }        
}
```



# 函数

**【原则】函数功能要单一，一个函数只做一件事。**

**【原则】函数应高内聚，低耦合。**

**【建议】函数规模尽可能小，尽量控制在50行代码之内。**

**【规则】重复代码尽量提炼成函数。**

**【规则】函数的参数要书写完整，不要只写参数类型不写参数名字，如无参数必须写void。**

```C++
void SetValue(int width, int height); // 良好的风格 
void SetValue(int, int); // 不良的风格 
float GetValue(void); // 良好的风格 
float GetValue(); // 不良的风格
```

**【规则】参数命名要恰当，顺序要合理。**

例如编写字符串拷贝函数 CopyString，它有两个参数。如果把参数名字起为 str1和 str2，例如   

```C++
void CopyString(char *str1, char *str2);
```

 那么我们很难搞清楚究竟是把 str1 拷贝到 str2 中，还是刚好倒过来。可以把参数名字起得更有意义，如叫 strSource 和 strDestination。这样从名字上就可 以看出应该把 strSource 拷贝到 strDestination。

还有一个问题，这两个参数哪个在前哪个在后？参数的顺序要遵循程序员的习惯。一般地，应将目的参数放在前面，源参数放在后面。

 如果将函数声明为： 

```C++
void CopyString(char *strSource, char *strDestination);
```

 别人在使用时可能会不假思索地写成如下形式导致错误： 

```C++
    char str[20];
    CopyString(str, "Hello World"); // 参数顺序颠倒
```

**【规则】如果参数是指针，且仅作输入用，则应在类型前加 const，以防止该指针在函数体内被意外修改。**

```C++
void CopyString(char * const strDestination, const char * const strSource);
```

**【规则】如果输入参数以值传递的方式传递对象，则宜改用“const &”方式来传递，这样可以省去临时对象的构造和析构过程，从而提高效率。**

**【建议】避免函数有太多的参数，参数个数尽量控制在 5 个以内。**

如果参数太多，在使用时容易将参数类型或顺序搞错。

**【规则】函数返回值类型不可省略。**

C语言中，凡不加类型说明的函数，一律自动按整型处理。这样做不会有什么好处，却容易被误解为void类型。

C++语言有很严格的类型安全检查，不允许上述情况发生。由于C++程序可以调用C函数，为了避免混乱，规定任何C/C++函数都必须有返回类型。如果函数没有返回值，那么应声明为void类型。

**【规则】不要将正常值和错误标志混在一起返回。正常值用输出参数获得，而错误标志用 return语句返回。**

```C++
/**
* @brief   GetHead()
* @details 读取列表中的第一个条目，不删除
* @param   *y 读取的条目
* @return  操作状态，故障码
*/
INT16 CWarningList::GetHead(TListElem *y)
{
    if (y == nullptr)
    {
        return WL_FAIL;
    }

    if (length <= 0)
    {
        return WL_EMPTY;
    }

    *y = data[(front + 1) % capacity];

    return WL_SUCCESS;
} 
```

**【规则】在函数入口处对参数有效性进行检查。**

**【建议】不仅要检查输入参数的有效性，还要检查函数内用到的其它变量的有效性，比如全局变量，文件等。**

**【建议】尽量避免函数带有“记忆”功能。相同的输入应当产生相同的输出。**

带有“记忆”功能的函数，其行为可能是不可预测的，因为它的行为可能取决于某种“记忆状态”。这样的函数既不易理解又不利于测试和维护。在 C/C++语言中，函数的static 局部变量是函数的“记忆”存储器。建议尽量少用 static 局部变量，除非必需。

**【规则】在函数体的出口处，对 return 语句的正确性和效率进行检查。**

注意事项如下

1. return语句不可返回指向栈内存的指针或引用。

   因为栈内存在函数结束时自动销毁。
```C++
char * Func(void) 
{ 
    char str[] = “hello world”; // str的内存位于栈上
    return str; // 函数返回时，str指向的内存将被销毁，导致错误 
}
```

2. 要搞清楚返回的究竟是“值”、“指针”还是“引用”。
3. 如果函数返回值是一个对象，要考虑return语句的效率。

```C++
    return String(s1 + s2);
```

这是临时对象的语法，表示“创建一个临时对象并返回它”。不要以为它与“先创建一个局部对象 temp 并返回它的结果”是等价的，如

```C++
    String temp(s1 + s2);
    return temp;  
```

 实质不然，上述代码将发生三件事。首先，temp对象被创建，同时完成初始化；然后拷贝构造函数把temp拷贝到保存返回值的外部存储单元中；最后，temp在函数结束时被销毁（调用析构函数）。然而“创建一个临时对象并返回它”的过程是不同的，编译器直接把临时对象创建并初始化在外部存储单元中，省去了拷贝和析构的化费，提高了效率。

# 内存管理

 



# 中断程序

1、不建议使用位域变量









>  1、 华为编程规范
>
>  2、Google_Cpp_Style_guide_CN
>
>  3、华为技术有限公司C++语言编程规范
>
>  4、高质量C++/C编程指南 林锐