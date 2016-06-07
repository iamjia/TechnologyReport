# iOS 面试指导大纲


## 基础考查

**1、解释以下指针的行为：**

```c
char *p1; // 描述 sizeof(p1) 的值

int *p2; // 描述 sizeof(p2) 的值

void *p3; // 描述 sizeof(p3) 的值
```

```c
char *p = 0;

++p; // 描述 p 的值
```

```c
void *p = 0;

printf("%p", p); // 描述输出结果
```

```c
char *p = 0;

printf("%c", *p); // 描述输出结果
```


**2、计算无符号数 0x70 的十进制值**

**3、不用中间量，交换两个变量的值**

```c
int a = 3;
int b = 4;

// 交换 a, b 的值
```

```c
float a = 3;
float b = 4;

// 交换 a, b 的值
```

```c
int a = INT_MAX;
int b = 9;

// 交换 a, b 的值
```

**4、描述运算符的优先级**

- 条件运算符：
- 算术运算符：
- 逻辑运算符：
- 关系运算符：
- 逗号运算符：


## 学习能力考查

**1、最近有看哪些书，技术方面的有哪些，说说收获**

**2、遇到技术问题，一般如何解决，步骤流程**

**3、平时上哪些技术网站**

**4、会翻墙否？如何组织搜索的关键词**

**5、apple developer 官网知道吗？看过原版英文文档否？举例说明**


## OC 相关

**1、描述 true, false 同 YES，NO 的区别**

**2、描述 nil, Nil, null, NSNull 的区别**

**3、带`+`号方法和带`-`号方法的区别**

**4、_cmd 代表什么**

**5、如何取得 oc 方法的函数指针，并调用之**

**6、内存管理**

- ARC 是如何运作的？同 GC 的区别

- autoreleasepool 的作用方式

-  retain 和 strong 的区别， weak 和 assign 的区别

- property 中 @synthesize , @dynamic 分别表示什么

- 实现以下 property 的 getter, setter

```objective-c

@property (nonatomic, strong) id obj;

```

```objective-c

@property (atomic, strong) id obj;

```

**7、什么是 retain cycle? 在 block 中如何避免？**

**8、category 的使用，头文件暴露与否同作用范围的关系（加分儿项：load 方法的描述）**

**9、iOS app 的生命周期中会经历哪些状态，以及状态之间如何转化**


## IDE 的使用及项目结构

**1、描述 source code -> ipa 过程中 Xcode 所经历的过程**

**2、多语言的配置，及查找逻辑 （app  bundle 的结构）**

**3、如何配置 ARC 与 MRC 源码混合的环境**

**4、是否配置及使用过 Xcode 的 UT**

**5、项目上传 repo，一般需要滤除哪些文件**

**6、描述 Xcode Products 分组对应的目录结构 （build目录）**


## 项目经验及高阶技术栈

**1、UIViewController 在 iOS6 -> iOS9 中，self.view 在 window 中的初始位置变化**

**2、constraints 的使用及原理**

**3、auto layout 之前如何布局**

**4、iOS 中可用的多线程技术有哪些？使用经验**

**5、core data 的使用经验， NSPredicate**

**6、如何提高 UITableViewCell 的滚动帧率**

**7、设计一个类似 sina weibo 的草稿箱功能**

**8、hybride （js bridge，js patch，react native 等）**

