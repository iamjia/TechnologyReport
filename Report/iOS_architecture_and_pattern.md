# iOS 项目架构及规范

## 一、基本语法规范

### 1、BOOL 值的使用，严格语意

1）条件判断的对象只能是 `BOOL` 值，`BOOL` 值可以是 `BOOL` 变量、常量、字面值或条件表达式。

- `BOOL` 变量，常量：`BOOL` 类型修饰的标志符，字面值就是 `YES`，`NO`。

- 条件表达式：被关系运算符（==，!=，>，>=，<，<=）修饰的表达式。

- 编译器隐式转换：常见语言对条件判断对象隐式转换，0 为 `NO`，非 0 为 `YES`。

反例 1.1 如下

```objective-c
NSObject *obj = nil;
if (obj) { // never do it like this!!!
	// xxx
}
```

虽然在传统强类型语言中，上例中的 `obj` 值被隐式转换为 `BOOL` 值，但是在 `swift` 或 `go` 这类新兴强类型语言中，`BOOL` 值的隐式转换是完全禁止的。


2）`BOOL` 值隐式转换与 `NULL/nil` 可能引发惊天大坑：由于除 `C` 语言外，`C++`，`OC` 等语言标准均没有规定 `NULL` 就是 0 值，理论上来说，实现语言标准的编译器可以把 `NULL` 置为任何值。

这时再考虑反例 1.1 中的条件判断，如果 `nil` 不是 0 值，那么条件判断的分支逻辑就不再遵从原本的逻辑。也就是说在实际编码时应该做到只依赖语言标准，而不是编译器特性。


### 2、系统注解的使用：#pragma 等

1）注释风格：

- 单行注释：注释单个变量，属性等

```objective-c 
NSInteger i = 0; // 双杠前后都有一个空格
```

- 多行注释：注释类声明，功能块等


2）XCode 内建注释符号：`MARK`，`TODO`，`FIXME`，`???`，`!!!`
以 `TODO` 为例

```objective-c 
NSInteger i = 0; // TODO: 双杠前后都有一个空格，后跟半角冒号，冒号后有一个空格
```
内建注释符号的好处：跟 XCode 的 `funtion menu` 深度集成，注释风格统一，方便维护。

3）`#pragma mark`：常用分段注解，后跟减号 `-` 则在 `funtion menu` 中会多一条分隔线

注释风格为顶部空两行，底部空一行，如

```objective-c 

} // 假装我是最近的一行末尾
1行
2行
#pragma mark - xxxooo
1行
// 该写啥写啥 
```

如果 `#pragma mark` 的是 `protocol`，`interface` 等，请使用 `protocol`，`interface` 的真实名称。


### 3、技术风格的选取

基于代码可读性和维护性的考虑，如无特殊要求和复用需求应该尽量遵守如下规则：

- `NSNotificationCenter`：使用 `addObserverForName:object:queue:usingBlock:`，该方法返回一个真实的 `observer` 对象，该对象被 `NSNotificationCenter` 本身 `retain`，因此在实际使用中，以 `__weak` 方式持有即可。但是必须被 `removeObserver:`。

- `KVO`：使用 [FBKVOController](https://github.com/facebook/KVOController)，`dealloc` 时无需显式 `unobserve`。

- `target-action`：`UIControl` 及其子类，`UIGestureRecognizer` 及其子类使用 [BlocksKit](https://github.com/zwaldowski/BlocksKit)。


## 二、MVCS 架构的层次关系

```flow
st=>start: Start|past:>http://www.google.com[blank]
e=>end: End:>http://www.google.com
op1=>operation: My Operation|past
op2=>operation: Stuff|current
sub1=>subroutine: My Subroutine|invalid
cond=>condition: Yes 
or No?|approved:>http://www.baidu.com
c2=>condition: Good idea|rejected
io=>inputoutput: catch something...|request

st->op1(right)->cond
cond(yes, right)->c2
cond(no)->sub1(left)->op1
c2(yes)->io->e
c2(no)->op2->e
```

## 三、模块化的真实含义


## 四、避免过早优化之重构的时机及意义


