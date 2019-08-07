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

示例：对此原则/规则/建议从正、反两个方面给出例子。  







# 风格

## 排版

**【建议】  在代码编辑器中，将字体设置为等宽字体。**  

在代码编辑器中，建议设置为等宽字体，例如Consolas、Courier New等，便于代码对齐。  

**【建议】代码行缩进4个空格，并且不使用tab** 。

在不同的编辑器中，一个tab的宽度是不同的，如果tab和空格混用，会导致在一个编辑器中排版好的代码在另一个编辑器中打开时对不齐。  

例如，下图为在VS中编写好的代码  

![VS代码的对齐](.\picture\Snipaste_2019-01-11_16-32-58.png)  

在记事本中打开，代码就乱了 ![notepad代码的对齐](.\picture\Snipaste_2019-01-11_16-37-48.png)  查看VS中代码，显示空格和tab后
![VS代码的对齐](.\picture\Snipaste_2019-01-11_16-40-48.png)  可以看出在编写代码时tab和空格混用，在VS中一个tab宽度为4个空格，而在记事本中一个tab宽度为8个空格，所以导致记事本中显示的代码格式混乱。

**【建议】类的声明按照一定的顺序进行，关键字不缩进。**

对外使用的接口或变量放前面，只在类内部使用的成员变量或成员函数放后面。

```
class Box
{
public:
    float Length;
    float 

};
```



## 文件命名



## 数据类型命名



## 常量命名



## 变量命名



## 函数命名







# 注释 #

**【原则】好的代码本身就是文档，不需注释即可理解。**

代码必须具有可读性，最好的代码本身就是文档，类型和变量命名意义明确比通过注释解释模糊的命名好的多。

**【原则】注释要简洁明确，且在功能、意图层次上解释，着重说明“为什么”，而不是逐行描述代码。**

为了别人理解代码，或者自己理解代码，需要合理添加注释。如何写注释，什么样的注释是好的注释，这是一个非常重要的问题。注释并不是写的越多越好，关键是要说明程序的功能，目的，这就要求注释主要讲为什么，而不是是什么，或者怎么做。

例如，下面的注释完全是多余的，除了浪费码字的时间，占用字符位置，还影响别人读代码。

```c
if (Timer > 10)  // 如果Timer大于10
{
    i++;  // i加一
}
```

对于代码实现逻辑晦涩或巧妙的代码需着重说明。

例如，下面对定点DSP实现除法代码的注释。

```C
AvgCurrent = (TotalCurrent * 1365)>>13; // 定点运算，平均电流=总电流/设备数量6台
```

**【规则】注释必须与代码同步更新。**

和代码不能同步的注释，不仅没有解释代码，起到帮助别人理解代码的作用，更多情况反而会误导读者，所以修改代码的同时必须更新相应的注释。

**【建议】单行注释使用//，多行注释使用/\* \*/ **

**【规则】注释/\* \*/不可嵌套使用。 **

**【规则】注释应位于相应代码的上边相邻位置或右边。**

注释写在相应代码的右边或上面，紧邻代码，不要太远，例如行尾注释可在代码后空两格添加。注释位于代码上面时，需与相应代码缩进相同。

当连续多行代码都有注释时，可以适当调整注释位置使排版美观，可读性更好。

例如，注释位于代码右边。

```C
int VoltOverLow;  // 电压过低标志
```

例如，注释位于代码上面。

```C
// 由于通信可能受到干扰，为避免误判通信失败，在此处连续5次异常，才判定通信失败。
if (CommAbnormalCnt >= 5)
{
    CommFail = true;
}
```

例如，连续多行代码都有注释

```C
struct RecFaultBits
{
    UINT16 Fault				:1;  // BIT00 PFC故障汇总标志
    UINT16 HwSoftStartAbnormal  :1;  // BIT01 硬件软起异常
    UINT16 SwSoftStartAbnormal  :1;  // BIT02 软件软起异常
    UINT16 DcVoltLow            :1;  // BIT03 直流母线低压
    UINT16 Rsvd                 :12; // BIT04-15 保留
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
    float Uin;     // 市电电压
    ...
private:
    float FreqFlt;  // 市电频率滤波值，用于监控显示
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
typedef struct box {
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




# 宏和常量
## 宏常数和常量

## 宏表达式

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
#define UPDNLMT(Var,Max,Min) (Var)=((Var)>=(Max))?(Max):(Var); \
                             (Var)=((Var)<=(Min))?(Min):(Var);
```

当如下方式使用时

```
for (int i=0; i<1000; i++)
    UPDNLMT(Var,1024,-1024)
....
```

会导致循环中只有宏表达式的第一句执行。加上{}后可以解决这一问题。

```
#define UPDNLMT(Var,Max,Min) {(Var)=((Var)>=(Max))?(Max):(Var); \
                             (Var)=((Var)<=(Min))?(Min):(Var);}
```

上面示例中，宏表达式可正常作用。但是，如果在调用宏表达式时后面加上分号，仍会出现错误

```c++
if (Flag == 1)
    UPDNLMT(Var,1024,-1024);
else
    UPDNLMT(Var,10,-10);
```

编译器会提示编译错误。

所以使用do while(0)方式定义宏表达式更好一些。

**【规则】使用宏表达式时，参数不允许变化。**

```c++
#define SQUARE_AREA(R) ((R)*(R))
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

int MAX_FUNC(int a, int b) 
{
    return ((a) > (b) ? (a) : (b));
}

int testFunc()
{
    unsigned int a = 1;
    int b = -1;
    printf("MACRO: max of a and b is: %d\n", MAX_MACRO(++a, b));
    printf("FUNC : max of a and b is: %d\n", MAX_FUNC(a, b));
    return 0;
}
```

上面宏代码调用中，结果是(a < b)，所以a只加了一次，所以最终的输出结果是：

 MACRO: max of a and b is: -1

FUNC : max of a and b is: 2

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



# 函数

# 命名

# 

## 中断程序

1、不建议使用位域变量









>  1、 华为编程规范
>
> 2、Google_Cpp_Style_guide_CN
>
> 3、华为技术有限公司C++语言编程规范