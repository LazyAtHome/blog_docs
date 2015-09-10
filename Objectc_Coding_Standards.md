

#1.留白和格式
###1.1空格 vs. 制表符

只使用空格，且一次缩进两个空格。
我们使用空格缩进。不要在代码中使用制表符。你应该将编辑器设置成自动将制表符替换成空格。

###1.2行宽

尽量让你的代码保持在 80 列之内。

我们深知 Objective-C 是一门繁冗的语言，在某些情况下略超 80 列可能有助于提高可读性，但这也只能是特例而已，不能成为开脱。

如果阅读代码的人认为把把某行行宽保持在 80 列仍然有不失可读性，你应该按他们说的去做。

我们意识到这条规则是有争议的，但很多已经存在的代码坚持了本规则，我们觉得保证一致性更重要。

通过设置 Xcode > Preferences > Text Editing > Show page guide，来使越界更容易被发现。

###1.3方法声明和定义


\- + 和返回类型之间须使用一个空格，参数列表中只有参数之间可以有空格。
方法应该像这样：

```
- (void)doSomethingWithString:(NSString *)theString {
  ...
}```

星号前的空格是可选的。当写新的代码时，要与先前代码保持一致。

如果一行有非常多的参数，更好的方式是将每个参数单独拆成一行。如果使用多行，将每个参数前的冒号对齐。

```
- (void)doSomethingWith:(GTMFoo *)theFoo
                   rect:(NSRect)theRect
               interval:(float)theInterval {
  ...
}```

当第一个关键字比其它的短时，保证下一行至少有 4 个空格的缩进。这样可以使关键字垂直对齐，而不是使用冒号对齐：

```
- (void)short:(GTMFoo *)theFoo
    longKeyword:(NSRect)theRect
    evenLongerKeyword:(float)theInterval {
  ...
}```

###1.4方法调用


方法调用应尽量保持与方法声明的格式一致。当格式的风格有多种选择时，新的代码要与已有代码保持一致。
调用时所有参数应该在同一行：
```

[myObject doFooWith:arg1 name:arg2 error:arg3];```

或者每行一个参数，以冒号对齐：
```

[myObject doFooWith:arg1
               name:arg2
              error:arg3];```

不要使用下面的缩进风格：
```

[myObject doFooWith:arg1 name:arg2  // some lines with >1 arg
              error:arg3];

[myObject doFooWith:arg1
               name:arg2 error:arg3];

[myObject doFooWith:arg1
          name:arg2  // aligning keywords instead of colons
          error:arg3];```

方法定义与方法声明一样，当关键字的长度不足以以冒号对齐时，下一行都要以四个空格进行缩进。

```
[myObj short:arg1
    longKeyword:arg2
    evenLongerKeyword:arg3];```

###1.5@public 和 @private


@public 和 @private 访问修饰符应该以一个空格缩进。
与 C++ 中的 public, private 以及 protected 非常相似。
```

@interface MyClass : NSObject {
 @public
  ...
 @private
  ...
}
@end```

###1.6异常

每个 @ 标签应该有独立的一行，在 @ 与 {} 之间需要有一个空格， @catch 与被捕捉到的异常对象的声明之间也要有一个空格。
如果你决定使用 Objective-C 的异常，那么就按下面的格式。不过你最好先看看 避免抛出异常 了解下为什么不要使用异常。
```

@try {
  foo();
}
@catch (NSException *ex) {
  bar(ex);
}
@finally {
  baz();
}```

###1.7协议名


类型标识符和尖括号内的协议名之间，不能有任何空格。
这条规则适用于类声明、实例变量以及方法声明。例如：
```

@interface MyProtocoledClass : NSObject<NSWindowDelegate> {
 @private
  id<MyFancyDelegate> delegate_;
}
- (void)setDelegate:(id<MyFancyDelegate>)aDelegate;
@end```

###1.8块（闭包）


块（block）适合用在 target/selector
模式下创建回调方法时，因为它使代码更易读。块中的代码应该缩进 4 个空格。

取决于块的长度，下列都是合理的风格准则：

如果一行可以写完块，则没必要换行。

如果不得不换行，关括号应与块声明的第一个字符对齐。

块内的代码须按 4 空格缩进。

如果块太长，比如超过 20 行，建议把它定义成一个局部变量，然后再使用该变量。

如果块不带参数，^{ 之间无须空格。如果带有参数，^( 之间无须空格，但 ) { 之间须有一个空格。
块内允许按两个空格缩进，但前提是和项目的其它代码保持一致的缩进风格。
```
// The entire block fits on one line.
[operation setCompletionBlock:^{ [self onOperationDone]; }];

// The block can be put on a new line, indented four spaces, with the
// closing brace aligned with the first character of the line on which
// block was declared.
[operation setCompletionBlock:^{
    [self.delegate newDataAvailable];
}];

// Using a block with a C API follows the same alignment and spacing
// rules as with Objective-C.
dispatch_async(fileIOQueue_, ^{
    NSString* path = [self sessionFilePath];
    if (path) {
      // ...
    }
});


// An example where the parameter wraps and the block declaration fits
// on the same line. Note the spacing of |^(SessionWindow *window) {|
// compared to |^{| above.
[[SessionService sharedService]
    loadWindowWithCompletionBlock:^(SessionWindow *window) {
        if (window) {
          [self windowDidLoad:window];
        } else {
          [self errorLoadingWindow];
        }
    }];

// An example where the parameter wraps and the block declaration does
// not fit on the same line as the name.
[[SessionService sharedService]
    loadWindowWithCompletionBlock:
        ^(SessionWindow *window) {
            if (window) {
              [self windowDidLoad:window];
            } else {
              [self errorLoadingWindow];
            }
        }];

// Large blocks can be declared out-of-line.
void (^largeBlock)(void) = ^{
    // ...
};
[operationQueue_ addOperationWithBlock:largeBlock];```


#2命名
对于易维护的代码而言，命名规则非常重要。Objective-C 的方法名往往十分长，但代码块读起来就像散文一样，不需要太多的代码注释。

当编写纯粹的 Objective-C 代码时，我们基本遵守标准的 Objective-C naming rules [http://developer.apple.com/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html]，这些命名规则可能与 C++ 风格指南中的大相径庭。例如，Google 的 C++ 风格指南中推荐使用下划线分隔的单词作为变量名，而(苹果的)风格指南则使用驼峰命名法，这在 Objective-C 社区中非常普遍。

任何的类、类别、方法以及变量的名字中都使用全大写的 首字母缩写 [http://en.wikipedia.org/wiki/Initialism]。这遵守了苹果的标准命名方式，如 URL、TIFF 以及 EXIF。

当编写 Objective-C++ 代码时，事情就不这么简单了。许多项目需要实现跨平台的 C++ API，并混合一些 Objective-C、Cocoa 代码，或者直接以 C++ 为后端，前端用本地 Cocoa 代码。这就导致了两种命名方式直接不统一。

我们的解决方案是：编码风格取决于方法/函数以哪种语言实现。如果在一个 @implementation 语句中，就使用 Objective-C 的风格。如果实现一个 C++ 的类，就使用 C++ 的风格。这样避免了一个函数里面实例变量和局部变量命名规则混乱，严重影响可读性。

###2.1文件名


文件名须反映出其实现了什么类 – 包括大小写。遵循你所参与项目的约定。

文件的扩展名应该如下：

.h	C/C++/Objective-C 的头文件

.m	Ojbective-C 实现文件

.mm	Ojbective-C++ 的实现文件

.cc	纯 C++ 的实现文件

.c	纯 C 的实现文件

类别的文件名应该包含被扩展的类名，如：GTMNSString+Utils.h 或GTMNSTextView+Autocomplete.h。

###2.2Objective-C++


源代码文件内，Ojbective-C++ 代码遵循你正在实现的函数/方法的风格。
为了最小化 Cocoa/Objective-C 与 C++ 之间命名风格的冲突，根据待实现的函数/方法选择编码风格。实现 @implementation 语句块时，使用 Objective-C 的命名规则；如果实现一个 C++ 的类，就使用 C++ 命名规则。
```
// file: cross_platform_header.h

class CrossPlatformAPI {
 public:
  ...
  int DoSomethingPlatformSpecific();  // impl on each platform
 private:
  int an_instance_var_;
};

// file: mac_implementation.mm
#include "cross_platform_header.h"

// A typical Objective-C class, using Objective-C naming.
@interface MyDelegate : NSObject {
 @private
  int instanceVar_;
  CrossPlatformAPI* backEndObject_;
}
- (void)respondToSomething:(id)something;
@end
@implementation MyDelegate
- (void)respondToSomething:(id)something {
  // bridge from Cocoa through our C++ backend
  instanceVar_ = backEndObject->DoSomethingPlatformSpecific();
  NSString* tempString = [NSString stringWithInt:instanceVar_];
  NSLog(@"%@", tempString);
}
@end

// The platform-specific implementation of the C++ class, using
// C++ naming.
int CrossPlatformAPI::DoSomethingPlatformSpecific() {
  NSString* temp_string = [NSString stringWithInt:an_instance_var_];
  NSLog(@"%@", temp_string);
  return [temp_string intValue];
}```

###2.3类名


类名（以及类别、协议名）应首字母大写，并以驼峰格式分割单词。

应用层 的代码，应该尽量避免不必要的前缀。为每个类都添加相同的前缀无助于可读性。当编写的代码期望在不同应用程序间复用时，应使用前缀（如：GTMSendMessage）。

###2.4类别名


类别名应该有两三个字母的前缀以表示类别是项目的一部分或者该类别是通用的。类别名应该包含它所扩展的类的名字。

比如我们要基于 NSString 创建一个用于解析的类别，我们将把类别放在一个名为 GTMNSString+Parsing.h 的文件中。类别本身命名为 GTMStringParsingAdditions （是的，我们知道类别名和文件名不一样，但是这个文件中可能存在多个不同的与解析有关类别）。类别中的方法应该以 gtm_myCategoryMethodOnAString: 为前缀以避免命名冲突，因为 Objective-C 只有一个名字空间。如果代码不会分享出去，也不会运行在不同的地址空间中，方法名字就不那么重要了。

类名与包含类别名的括号之间，应该以一个空格分隔。

###2.5Objective-C 方法名


方法名应该以小写字母开头，并混合驼峰格式。每个具名参数也应该以小写字母开头。

方法名应尽量读起来就像句子，这表示你应该选择与方法名连在一起读起来通顺的参数名。（例如，convertPoint:fromRect: 或 replaceCharactersInRange:withString:）。详情参见 Apple’s Guide to Naming Methods 。

访问器方法应该与他们 要获取的 成员变量的名字一样，但不应该以get作为前缀。例如：

```
- (id)getDelegate;  // AVOID
- (id)delegate;     // GOOD```

这仅限于 Objective-C 的方法名。C++ 的方法与函数的命名规则应该遵从 C++ 风格指南中的规则。

###2.6变量名


变量名应该以小写字母开头，并使用驼峰格式。类的成员变量应该以下划线作为后缀。例如：myLocalVariable、myInstanceVariable_。如果不能使用 Objective-C 2.0 的 @property，使用 KVO/KVC 绑定的成员变量可以以一个下划线作为前缀。
普通变量名

对于静态的属性（int 或指针），不要使用匈牙利命名法。尽量为变量起一个描述性的名字。不要担心浪费列宽，因为让新的代码阅读者立即理解你的代码更重要。例如：


错误的命名：
```

int w;
int nerr;
int nCompConns;
tix = [[NSMutableArray alloc] init];
obj = [someObject object];
p = [network port];```


正确的命名：
```
int numErrors;
int numCompletedConnections;
tickets = [[NSMutableArray alloc] init];
userInfo = [someObject object];
port = [network port];```

###2.7实例变量

实例变量应该混合大小写，并以下划线作为后缀，如 usernameTextField_。然而，如果不能使用 Objective-C 2.0（操作系统版本的限制），并且使用了 KVO/KVC 绑定成员变量时，我们允许例外（译者注： KVO=Key Value Observing，KVC=Key Value Coding）。这种情况下，可以以一个下划线作为成员变量名字的前缀，这是苹果所接受的键/值命名惯例。如果可以使用 Objective-C 2.0，@property 以及 @synthesize 提供了遵从这一命名规则的解决方案。

##2.8常量

常量名（如宏定义、枚举、静态局部变量等）应该以小写字母 k 开头，使用驼峰格式分隔单词，如：kInvalidHandle，kWritePerm。

#3注释
虽然写起来很痛苦，但注释是保证代码可读性的关键。下面的规则给出了你应该什么时候、在哪进行注释。记住：尽管注释很重要，但最好的代码应该自成文档。与其给类型及变量起一个晦涩难懂的名字，再为它写注释，不如直接起一个有意义的名字。

当你写注释的时候，记得你是在给你的听众写，即下一个需要阅读你所写代码的贡献者。大方一点，下一个读代码的人可能就是你！

记住所有 C++ 风格指南里的规则在这里也同样适用，不同的之处后续会逐步指出。

###3.1文件注释


每个文件的开头以文件内容的简要描述起始，紧接着是作者，最后是版权声明和/或许可证样板。
版权信息及作者

每个文件应该按顺序包括如下项：

文件内容的简要描述

代码作者

版权信息声明（如：Copyright 2008 Google Inc.）

必要的话，加上许可证样板。为项目选择一个合适的授权样板（例如，Apache 2.0, BSD, LGPL, GPL）。

如果你对其他人的原始代码作出重大的修改，请把你自己的名字添加到作者里面。当另外一个代码贡献者对文件有问题时，他需要知道怎么联系你，这十分有用。

###3.2声明部分的注释


每个接口、类别以及协议应辅以注释，以描述它的目的及与整个项目的关系。
```

// A delegate for NSApplication to handle notifications about app
// launch and shutdown. Owned by the main app controller.
@interface MyAppDelegate : NSObject {
  ...
}
@end```

如果你已经在文件头部详细描述了接口，可以直接说明 “完整的描述请参见文件头部”，但是一定要有这部分注释。

另外，公共接口的每个方法，都应该有注释来解释它的作用、参数、返回值以及其它影响。

为类的线程安全性作注释，如果有的话。如果类的实例可以被多个线程访问，记得注释多线程条件下的使用规则。

###3.3实现部分的注释


使用 | 来引用注释中的变量名及符号名而不是使用引号。
这会避免二义性，尤其是当符号是一个常用词汇，这使用语句读起来很糟糕。例如，对于符号 count ：

// Sometimes we need |count| to be less than zero.
或者当引用已经包含引号的符号：

// Remember to call |StringWithoutSpaces("foo bar baz")|

###3.4对象所有权


当与 Objective-C 最常规的作法不同时，尽量使指针的所有权模型尽量明确。

继承自 NSObject 的对象的实例变量指针，通常被假定是强引用关系（retained），某些情况下也可以注释为弱引用（weak）或使用 __weak 生命周期限定符。同样，声明的属性如果没有被类 retained，必须指定是弱引用或赋予 @property 属性。然而，Mac 软件中标记上 IBOutlets 的实例变量，被认为是不会被类 retained 的。

当实例变量指向 CoreFoundation、C++ 或者其它非 Objective-C 对象时，不论指针是否会被 retained，都需要使用 __strong 和 __weak 类型修饰符明确指明。CoreFoundation 和其它非 Objective-C 对象指针需要显式的内存管理，即便使用了自动引用计数或垃圾回收机制。当不允许使用 __weak 类型修饰符（比如，使用 clang 编译时的 C++ 成员变量），应使用注释替代说明。

注意：Objective-C 对象中的 C++ 对象的自动封装，缺省是不允许的，参见 这里 [http://chanson.livejournal.com/154253.html] 的说明。

强引用及弱引用声明的例子：
```
@interface MyDelegate : NSObject {
 @private
  IBOutlet NSButton *okButton_;  // normal NSControl; implicitly weak on Mac only

  AnObjcObject* doohickey_;  // my doohickey
  __weak MyObjcParent *parent_;  // so we can send msgs back (owns me)

  // non-NSObject pointers...
  __strong CWackyCPPClass *wacky_;  // some cross-platform object
  __strong CFDictionaryRef *dict_;

}

@property(strong, nonatomic) NSString *doohickey;
@property(weak, nonatomic) NSString *parent;
@end```


