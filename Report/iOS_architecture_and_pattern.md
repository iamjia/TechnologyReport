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

1）`MVCS` 的含义

- `View`：只负责 `GUI` 及 `UI` 的组织布局。

- `Controller`：负责 `Model` 层与 `View` 层的对接，即使在 `iOS` 中也不一定是 `UIViewController`，切勿对号入座！

- `Model`：只负责数据业务模型的定义及业务相关处理。

- `Service`：数据的获取，处理，存储，查询等。

正如上面描述，各层次之间应该保持严格的独立性，互相不出现在其它层次中，以最大程度地降低耦合，提高复用性。
对于 `Controller` 的概念也应该是广义的，并且可以推广到局部的。

例如 2.1：
`View` 的数据源绑定操作应该放到 `Controller` 层（再次强调，绝不能与 `UIViewController` 划等号），这时利用 `OC` 的语法特性，推荐的做法是抽出一个 `View` 的数据绑定 `Category`，这里的 `Category` 就是办演的 `Controller` 角色。

例如 2.2：
`Service` 层中，数据获取会抽离为单独的网络请求层，而数据存储，查询则抽离为数据管理层，于是 `Service` 就是前面两层的 `Controller`，并且处理一些耦合性的操作，如数据后处理，业务排序等。


2）`iOS` 中的 `UIViewController` 

`UIViewController` 首先是 `View` 层的一部分，除 `View` 以外的支持则是 `Controller` 层。也就是说 `UIViewController` 可以把 `self.view` 放到其它纯 `UIView` 层次里，而 `UIViewController` 则只作为 `Controller` 层使用。


## 三、避免过早优化之重构的时机及意义

- **千万不要过度设计**：逻辑设计应该追求极致的“刚好”，以刚好满足当前产品需求，并在已知的范围内达到最优的设计为宜。
为以后可能不存在的事情多写一句代码和复杂设计都只会给日后的代码维护和扩展挖天坑而已。
*总之就是要避免当前卵用的设计。*

- **千万不要过早优化**：需求实现最初阶段，不过把精力放在局部的优化上面。根据需求的不稳定性来决定实现的最优程度。毕竟按计划完成需求更加重要。质朴的设计可以从根源上消除根本不必要的优化。
*总之就是要找准优化的点，做到有效优化。*

- **各位爷一定要重构**：

	- 重构的目的：提高代码的扩展性和可维护性。

	- 重构的原则：保证当前需求满足的前提下，改善项目结构，抽取重复逻辑等。

	- 重构的时机：迭代结束 -> 下轮迭代初始。

	- 重构的技巧：以各种 extract 方式为主。rename 为辅。单元测试可以帮上忙。

