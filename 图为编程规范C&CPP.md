# 前言

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

**【建议】**  在代码编辑器中，将字体设置为等宽字体。  
在代码编辑器中，建议设置为等宽字体，例如Consolas、Courier New等，便于代码对齐。  
**【建议】** 代码中排版使用空格，不使用tab键。  
在不同的编辑器中，一个tab的宽度是不同的，如果tab和空格混用，会导致在一个编辑器中排版好的代码在另一个编辑器中打开时对不齐。  
例如，下图为在VS中编写好的代码  
![VS代码的对齐](.\picture\Snipaste_2019-01-11_16-32-58.png)  
在记事本中打开，代码就乱了  
![notepad代码的对齐](.\picture\Snipaste_2019-01-11_16-37-48.png)  
查看VS中代码，显示空格和tab后  
![VS代码的对齐](.\picture\Snipaste_2019-01-11_16-40-48.png)  
可以看出在编写代码时tab和空格混用，在VS中一个tab宽度为4个空格，而在记事本中一个tab宽度为8个空格，所以导致记事本中显示的代码格式混乱。

# 注释 #

## 文件注释 ##

```c
/**
* @file       filename
* @brief      This is a brief description.
* @details    This is the detail description.
* @author     Felix Lu/000011
* @date       2019-02-14
* @version    V00A00D00
* @par        Copyright © 2018 西安图为电气技术有限公司 All rights reserved.
* @par History:
* version: author, date, desc
*/
```

## 函数注释 ##

```C
/** 下面是一个含有两个参数的函数的注释说明（简述）
 * @brief   该函数的简要说明
 * @details 该函数的详述信息
 * @param a 被测试的变量（param描述参数）
 * @param b 被测试的另一变量的描述
 * @return  测试结果（return描述返回值）
 * @see     Test()（本函数参考其它的相关的函数，这里作一个链接） 
 * @note    (note描述需要注意的问题)
 */
int DoAnyting(int a, float b);
```



## Doxygen指令说明 ##

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

## 宏函数




# 变量



# 函数

# 命名

# 