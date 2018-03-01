前置条件:Alcatraz-Xcode包管理器(插件、模版以及颜色配置)
BBUDebuggerTuckAway-自动隐藏控制台
ClangFormat-格式化代码
deriveddata-exterminator清除Xcode缓存目录
FuzzyAutocompletePlugin-代码自动补全插件
HOStringSense-大段文本利器
KSImageNamed-图片插件
OMColorSense-颜色显示插件
Peckham-自动补全功能补充
SCXcodeSwitchExpander-补全枚举类型的每种可能取值
VVDocumenter-规范注释生成器
XAlign-一个用来对齐常规代码的Xcode插件
XcodeBoost-辅助小功能插件
XToDo-Xcode注释辅助插件
前置条件:Alcatraz-Xcode包管理器(插件、模版以及颜色配置)
Github

Alcatraz是一个帮你管理Xcode插件、模版以及颜色配置的工具。它可以直接集成到Xcode的图形界面中，让你感觉就像在使用Xcode自带的功能一样。

安装: 打开Mac上的终端, 输入curl -fsSL https://raw.github.com/supermarin/Alcatraz/master/Scripts/install.sh | sh; 重启Xcode,可以在Xcode的顶部菜单中找到Alcatraz并使用(网络环境不理想时, 需要多次输入该命令, 直至安装成功)
图示
删除: 打开Mac上的终端, 输入rm -rf ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins/Alcatraz.xcplugin

插件路径: Xcode的插件都安装在目录~/Library/Application Support/Developer/Shared/Xcode/Plug-ins/下

BBUDebuggerTuckAway-自动隐藏控制台
Github

BBUDebuggerTuckAway是一款支持自动隐藏Debugger的Xcode插件，其开发者为来自德国柏林Contentful GmbH公司的Boris Bügling。使用BBUDebuggerTuckAway，开发者能够实现在编辑代码时，自动隐藏底部的调试栏。
Demo
ClangFormat-格式化代码
Github

ClangFormat-Xcode是一款格式化代码工具，能够让开发者使用Clang将代码格式化为LLVM、Google、Chromium、Mozilla或WebKit等格式，其开发者为来自37signals的Travis Jeffery。通过ClangFormat，开发者不仅可以实现对代码的自动或批量格式化，还可以进行自定义配置。


Demo
deriveddata-exterminator清除Xcode缓存目录
Github

有些时候Xcode会出各种奇怪的问题，最常见的是在某些复杂操作下（例如同一个项目，来回切换到各种分支版本），会造成Xcode显示一些编译的错误或警告，但是最终却又可以编译通过。新手遇到这种问题常常束手无策，而熟悉Xcode的人就知道，通常清除Xcode缓存就可以解决这类问题。该插件在Xcode菜单上增加了一个清除缓存按钮，可以一键方便地清楚缓存内容。
Menu
FuzzyAutocompletePlugin-代码自动补全插件
Github

FuzzyAutocompletePlugin通过添加模糊匹配来提高Xcode代码自动补全功能，开发者无需遵循从头匹配的原则，只要记得方法里某个关键字即可进行匹配，很好地提高了工作效率。

HOStringSense-大段文本利器
Github

经常输入大段文本的时候，如果文本里面有各种换行和特殊字符，经常会让人很头疼，有了HOStringSense，再也不不用为这个问题犯愁了，顺便附送字数统计功能。
StringDemoAnimation
KSImageNamed-图片插件
Github

为项目中使用的UIImage的imageNamed提供文件名自动补全功能。使用[UIImage imageNamed:@"xxx"]时，该插件会扫描整个workspace中的图片文件。


Demo
OMColorSense-颜色显示插件
Github

代码里的那些冷冰冰的颜色数值，到底是什么颜色？如果你经常遇到这个问题，每每不得不运行下模拟器去看看，那么这个插件绝对不容错过。更彪悍的是你甚至可以点击显示的颜色面板，直接通过系统的ColorPicker来自动生成对应颜色代码，再也不用做各种颜色代码转换了！
Watch Demo Video (YouTube)

Peckham-自动补全功能补充
Github

添加导入语句有时候确实让人烦躁。举例来说，如果大家需要导入一条pod标题，那么Xcode的自动补全机制根本帮不上忙。在这种情况下，Peckham插件来救驾了。
按下Command+Control+P键，输入所需标题中的几个字母，并从该插件提供的备选内容列表中选取正确项目。对于Xcode的自动补全功能来说，这确实是一项极好的补充。
Peckham
SCXcodeSwitchExpander-补全枚举类型的每种可能取值
Github

插入所有可能的switch cases；保留已经使用的条件，仅插入缺失的条件；当使用内置的Xcode片段时仅保留默认条件；适用于变量、属性以及方法参数等；适用于嵌套switch语句；快速稳定，且不会明显影响Xcode的性能。
Demo
VVDocumenter-规范注释生成器
Github

很多时候，为了快速开发，很多的技术文档都是能省则省，这个时候注释就变得异常重要，再配合Doxygen这种注释自动生成文档的，就完美了。但是每次都要手动输入规范化的注释，着实也麻烦，但有了VVDocumenter，规范化的注释，主需要输入三个斜线“///”，就OK啦！


Demo
XAlign-一个用来对齐常规代码的Xcode插件
Github

一个用来对齐常规代码的Xcode插件，十分强大的自定义对齐模式。这里是一个对齐模式示例，模式文件在main/main/patterns.plist.


Demo
XcodeBoost-辅助小功能插件
Github

XcodeBoost是一款可以让开发者轻而易举地检查和修改Objective-C代码的插件。XcodeBoost能够自动进行一些繁琐的操作，比如方法的定义与声明、添加基于命令行的代码处理（剪切/复制/粘贴/重复/删除行）、持续高亮等。

XToDo-Xcode注释辅助插件
Blog

这是一个注释辅助插件, 可以把项目中的 TODO FIXME等注释列出来. 是不是也有点收集强迫症的嫌疑~~~


Demo

作者：Vinc
链接：https://www.jianshu.com/p/00410d75b83f
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

