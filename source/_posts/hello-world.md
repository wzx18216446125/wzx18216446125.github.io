### 不使用TypeScript的7个很好的理由

#### 大家都喜欢TypeScript。它“解决”了JS的很多问题，它是JS的“超集”，它会让你的代码不容易出错，而且阅读起来很愉快。使用TypeScript有很多好的理由，但我要给你7个真正好的理由不要使用。

### 1有风险
哗，怎么会有风险呢？如果TypeScript添加类型定义并在编译时检查它们，这怎么可能有风险？以及IDE集成会警告你任何类型不匹配？正是因为如此。TypeScript仅在编译时检查类型，并且仅检查可用的类型。任何网络调用，系统库，特定于平台的API和无类型的第三方库都无法与TypeScript通信。 当你习惯了对类型进行检查，不用完全理解代码和平台，错误和bug就会体现出来。

使用JS，你对类型不做任何假设，你检查变量的具体值，以确保它是你所期望的。或者，如果你不关心它的类型，在这种特殊情况下，你不关心。在TS中，你依靠编译器为你做，但它只能检查这么多。你可以把这两种方式结合起来，但那有什么意义呢？如果你会花时间写定义，然后花时间写代码来确保这些定义在运行时得到维护，那为什么一开始就要有这些定义呢？

理解了调用堆栈，你就会清楚解像是JS 这们的编程语言是如何执行的。

### 2. 太乱了
另一个悖论是：语言本应该为代码库带来清晰和可读性，但它却使代码库变得模糊了。为了说明我的意思，请查看一些我在流行的开源库中找到的示例：

// TODO: do this more elegantly
;((currentReducer as unknown) as Reducer<
  NewState,
  NewActions
>) = nextReducer
这是来自Redux库的，所有这4行代码都将 nextReducer 分配给 currentReducer。

下一个例子如果来自RxJS库。

// HACK: Since TypeScript inherits static properties too, we have to
// fight against TypeScript here so Subject can have a different static create signature
/**
 * Creates a new cold Observable by calling the Observable constructor
 * @static true
 * @owner Observable
 * @method create
 * @param {Function} subscribe? the subscriber function to be passed to the Observable constructor
 * @return {Observable} a new cold observable
 * @nocollapse
 * @deprecated use new Observable() instead
 */
static create: Function = <T>(subscribe?: (subscriber: Subscriber<T>) => TeardownLogic) => {
  return new Observable<T>(subscribe);
}
我不知道你是怎么想的，但如果我不得不打一个本应帮助我的工具，我不认为这是一个好工具。
  
### 它不能解决问题
据说TypeScript可以解决JavaScript的问题，但事实并非如此。动态类型化在JavaScript中从来都不是问题，但是其他很多毛病，比如 NaN === NaN 是false的，分号是可选的还是不可选的，一个换行符把一个对象定义改成了作用域，语法糖代替OOP，这些确实是问题。TypeScript并没有解决这些问题，而是引入了另一个标准，进一步分化了JS社区。

即使假设JS中缺少类型是一个问题，TS也无法解决。你知道是什么吗？Java、C、C#和其他编译语言。它们可以在编译时和运行时安全地保证强类型，解释语言就是不能做到这一点。

### 它不是超集，而是子集
TypeScript是编译成JavaScript的东西，从定义上看，它不可能是一个超集。它限制了你使用JavaScript所能做的事情，掩盖了它强大的一面，同时提供了一种虚假的安心感。如果你真的想成为一名优秀的开发者，就不要满足于安逸的谎言，要试着去了解JavaScript的真正威力和它的灵活性。

### 它是开源的，仅此而已
使用TypeScript的许多原因都表明它是开源的。的确，TS编译器是在MIT许可下分发的。但它仍然被微软这个垄断巨头所控制，它在开源方面的进步只不过是一种营销手段。不要把开源和民主混为一谈，微软仍然可以自由地对TS做任何事情，而JS则是由一个国际委员会管理，没有经过社会的认可，是不会改变任何东西的。

### 但是它具有更多功能……
现在不一样了。的确，2012年TS刚推出的时候，它有类等功能，在JS中还是没有的。但是JS从那时起已经有了长足的进步，现在TS也在努力的追赶。如果JS有什么缺失，有一个babel插件可以做到。
