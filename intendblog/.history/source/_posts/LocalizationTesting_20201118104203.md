---
title: 本地化测试
date: 2020-11-18 09:40:50
comments: false
auto_excerpt: true
toc: true
tags: 功能测试
categories: 
description:
---
此文仅是本人学习笔记。

## 一、概述
Localization testing（本地化测试），本地化测试的对象是软件的本地化版本。本地化测试的目的是测试特定目标区域设置的软件本地化质量。本地化测试的环境是在本地化的操作系统上安装本地化的软件。从测试方法上可以分为基本功能测试，安装/卸载测试，当地区域的软硬件兼容性测试。测试的内容主要包括软件本地化后的界面布局和软件翻译的语言质量，包含软件、文档和联机帮助等部分。
本地化就是翻译产品的 UI，有时也更改某些初始设置以使产品适合于另一个地区。本地化测试检查针对特定目标区域性或区域设置的产品本地化质量。此测试基于全球化测试的结果，后者验证对特定区域性或区域设置的功能性支持。本地化测试只能在产品的本地化版本上进行。可本地化性测试不对本地化质量进行测试。
本地化测试过程中的测试工作集中在：
• 受本地化影响的方面，如 UI 和内容
• 区域性或区域设置特定的、语言特定的和地区特定的方面
另外，本地化测试还应包括：
• 基本功能测试
• 在本地化环境中运行的安装和升级测试
• 根据产品的目标地区计划应用程序和硬件兼容性测试。
可以选择 Windows 2000 的任何语言版本作为测试平台。然而，必须安装目标语言支持。
用户界面和语言的本地化测试应包括的项有：
• 验证所有应用程序资源
• 验证语言的准确性和资源属性
• 版式错误
• 书面文档、联机帮助、消息、界面资源、命令键顺序等的一致性检查。
• 确认是否遵守系统、输入和显示环境标准
• 用户界面可用性
• 评估文化适合性
• 检查政治上敏感的内容
当交付本地化产品时，确保包含本地化文档（手册、联机帮助、上下文帮助等）。要检查的项包括：
• 翻译的质量
• 翻译的完整性
• 所有文档和应用程序 UI 中使用的术语一致
## 二、软件本地化测试的内容构成
1、软件本地化测试的目的
保证本地化的软件与源语言软件具有相同的功能和性能。
保证本地化的软件在语言、文化、传统观念等方面符合当地用户的习惯。
2、软件本地化测试的测试策略
本地化软件要在各种本地化操作系统上安装并测试。
源语言软件安装在另一台相同源语言操作系统上，作为对比测试。
重点测试因本地化引起的软件功能和软件界面的错误。
测试本地化软件的翻译质量。
手工测试和自动测试相结合。
3、软件本地化测试的主要内容
测试内容由不同的测试阶段决定，例如第一个Build，以软件界面测试为主，中间Build以功能和界面为主，最后Build终点测试安装/卸载，软件帮助和主要功能。
4、安装/卸载性能测试
测试本地化的软件是否可以正确地安装/卸载在本地语言的操作系统上（包括是否支持本地语言的安装目录名）。安装/卸载前后安装文件、快捷方式、程序图标和注册表等的变化是否与源语言程序一致。
5、软件功能测试
本地化软件功能是否与源语言软件功能相同。
是否支持当地语言的输入和输出，如对双字节支持和正确显示。
对当地日期，时间，货币符号等的支持性能。
是否支持当地语言的文件名和目录名。
6、软件界面测试
软件安装窗口中的按钮，菜单等的布局是否合理，美观。
软件运行后的界面元素，包括菜单、快捷键、对话框、屏幕提示、按钮、列表框的布局和本地化字体和字号是否正确。界面文字的翻译是否与术语表一致，是否存在没有翻译的元素。
7、帮助文件功能和翻译质量
本地化帮助文件的功能是否与源语言软件一致。
本地化帮助文件的布局是否合理，美观。
本地化帮助文件的文字翻译是否准确、专业，是否存在没有翻译的段落。
## 四、软件本地化测试类型解析与测试要领
软件本地化测试是在本地化的操作系统上对本地化的软件版本进行的测试。根据软件本地化项目的规模、测试阶段以及测试方法，本地化测试分为多种类型，每种类型都对软件本地化的质量进行检测和保证。为了提高测试的质量，保证测试的效率，不同类型的本地化测试需要使用不同的方法，掌握必要的测试技巧。本文主要选取本地化测试中具有代表性的测试类型进行分析，结合软件本地化项目的测试经验对其测试要领进行剖析。
1、  导航测试
导航测试（Pilot Testing）是为了降低软件本地化的风险而进行的一种本地化测试。大型的全球化软件在完成国际化设计后，通常选择少量的典型语言进行软件的本地化，以此测试软件的可本地化能力，降低多种语言同时本地化的风险。
导航测试尤其是用于数十种语言本地化的新开发的软件，导航测试版本的语言主要由语言市场的重要性和规模确定，也要考虑语言编码等的代表性。例如，德语市场是欧洲的重要市场，通常作为导航测试的首要单字节字符集语言。日语是亚洲重要的市场，可以作为双字节字符集语言代表。随着中国国内软件市场规模的增加，国际软件开发商逐渐对简体中文本地化提高重视程度，简体中文有望更多成为导航测试的首选语言。
导航测试是软件本地化项目早期进行的探索性测试，需要在本地化操作系统上进行，测试的重点是软件的国际化能力和可本地化能力，包括与区域相关的特性的处理能力，也包括测试是否可以容易地进行本地化，减少硬编码等缺陷。由于导航测试在整个软件本地化过程中意义重大，而且导航测试的持续时间通常较短，另外由于是新开发的软件的本地化测试，测试人员对软件的功能和使用操作了解不多，因此，本地化公司通常需要在正是测试之前进行搜集和学习软件的相关资料，做好测试环境和人员的配备，配置具有丰富测试经验的工程师执行测试。
2、可接受性测试
本地化软件的可接受性测试（Build Acceptable Testing）也称作冒烟测试（Smoke Testing），是指对编译的软件本地化版本的主要特征进行基本测试，从而确定版本是否满足详细测试的条件。理论上，每个编译的本地化新版本在进行详细测试之前，都需要进行可接受性测试，以便早期发现软件版本的可测试性，避免不必要的时间浪费。
注意，软件本地化版本的可接受性测试与软件公司为特定客户定制开发的原始语言软件在交付客户前的验收测试完全不同，验收测试主要确定软件的功能和性能是否达到了客户的需求，如果一切顺利，只进行一次验收测试就可以结束。
本地化软件在编译后，编译工程师通常需要执行版本健全性检查（Build Sanity Check），确定本地化版本的内容和主要功能可以用于测试。而编译的本地化版本是否真的满足测试条件则还要通过独立的测试人员进行可接受性测试，它要求测试人员在较短的时间内完成，确定本地化的软件版本是否满足全面测试的要求，是否正确包含了应该本地化的部分。如果版本通过了可接受性测试，则可以进入软件全面详细测试阶段，反之，则需要重新编译本地化软件版本，直到通过可接受性测试。
在进行本地化软件版本的可接受性测试时，需要配置正确的测试环境（软件和硬件），在本地化的操作系统上安装软件，确定是否可以正确安装。软件运行软件，确定软件包含了应该本地化的全部内容，并且主要功能正确。然后，卸载软件，保证软件可以彻底卸载。软件的完整性是需要注意的一个方面，通过使用文件和文件夹的比较工具软件，对比安装后的本地化软件和英文软件内容的异同，确定本地化的完整性。
3、语言质量测试
语言质量测试是软件本地化测试的重要组成部分，贯穿于本地化项目的各个阶段。语言质量测试的主要内容是软件界面和联机帮助等文档的翻译质量，包括正确性、完整性、专业性和一致性。
为了保证语言测试的质量，应该安排本地化语言作为母语的软件测试工程师进行测试，同时请本地化翻译工程师提供必要的帮助。在测试之前，必须阅读和熟悉软件开发商提供的软件术语表（Glossary），了解软件翻译风格（Translation Style）的语言表达要求。
由于软件的用户界面总是首先进行本地化，因此，本地化测试的初期的软件版本的语言质量测试主要以用户界面的语言质量为主，重点测试是否存在未翻译的内容，翻译的内容是否正确，是否符合软件术语表和翻译风格要求，是否符合母语表达方式，是否符合专业和行业的习惯用法。
本地化项目后期要对联机帮助和相关文档（各种用户使用手册等）进行本地化，这个阶段的语言质量测试，除了对翻译的表达正确性和专业性进行测试之外，还有注意联机帮助文件和软件用户界面的一致性。如果对于某些软件专业术语的翻译存在疑问，需要报告一个翻译问题，请软件开发商审阅，如果确认是翻译错误，需要修改术语表和软件的翻译。
关于本地化软件的语言质量测试，一个值得注意的问题是“过翻译”，就是软件中不应该翻译的内容（例如软件的名称等）如果进行了翻译，应该报告软件“过翻译”错误。
4、用户界面测试
本地化软件的用户界面测试（UI Testing），也称作外观测试（Cosmetic Testing）主要对软件的界面文字和控件布局（大小和位置）进行测试。用户界面至少包括软件的安装和卸载界面、软件的运行界面和软件的联机帮助界面。软件界面的主要组成元素包括窗口、对话框、菜单、工具栏、状态栏、屏幕提示文字等内容。
用户界面的布局测试是本地化界面测试的重要内容，由于本地化的文字通常比原始开发语言长度增长，所以一类常见的本地化错误是软件界面上的文字显示不完整，例如，按钮文字只显示一部分。另一类常见的界面错误是对话框中的控件位置排列不整齐，大小不一致。
相对于其他类型的本地化测试，用户界面测试可能是最简单的测试类型，软件测试工程师不需要过多的语言翻译知识和测试工具，但是由于软件的界面众多，而且某些对话框可能隐藏的比较深入，因此，软件测试工程师必须尽可能地熟悉被测试软件的使用方法，这样才能找出那些较为隐蔽的界面错误。另外，某个界面错误可能是一类错误，需要报告一个综合的错误，例如，软件安装界面的“上一步”或“下一步”按钮显示不完整，则可能所有安装对话框的同类按钮都存在相同的错误。
5、功能测试
原始语言开发的软件的功能测试主要测试软件的各项功能是否实现以及是否正确，而本地化软件的功能测试主要测试软件经过本地化后，软件的功能是否与源软件一致，是否存在因软件本地化而产生的功能错误，例如，某些功能失效或功能错误。
本地化软件的功能测试相对于其他测试类型具有较大难度，由于大型软件的功能众多，而且有些功能不经常使用，可能需要多步组合操作才能完成，因此本地化软件的功能测试需要测试工程师熟悉软件的使用操作，对于容易产生本地化错误之处能够预测，以便减少软件测试的工作量，这就要求测试工程师具有丰富的本地化测试经验。
除了某些菜单和按钮的本地化功能失效错误外，本地化软件的功能错误还包括软件的热键和快捷键错误，例如，菜单和按钮的热键与源软件不一致或者丢失热键。另外一类是排序错误，例如，排序的结果不符合本地化语言的习惯。
发现本地化功能错误后，需要在源软件上进行相同的测试，如果源软件也存在相同的错误，则不属于本地化功能错误，而属于源软件的设计错误，需要报告源软件的功能错误。另外，如果同时进行多种本地化语言（例如，简体中文、繁体中文、日文和韩文）的测试，在一种语言上的功能错误也需要在其他语言版本上进行相同的测试，以确定该错误是单一语言特有的，还是许多本地化版本共有的错误。
软件的测试类型数量众多，可谓五花八门，而软件本地化测试又具有其自身的特点，除以上常见的本地化测试类型外，还包括联机帮助测试、本地化能力测试等测试。不论何种类型的本地化测试，其最终测试目标都是尽早找出软件本地化错误，保证本地化软件与原始开发语言软件具有相同的功能。通过正确配置本地化测试环境，合理组织本地化测试人员，采用正确的本地化流程和测试工具，完善软件缺陷的报告和跟踪处理，有助于保证软件本地化测试的有效实现。
## 五、本地化测试软件缺陷分类详解
本地化测试发现的软件缺陷特征明显，便于分类。本文按照本地化测试软件缺陷的特征进行分类，周详地分析各种缺陷的表现特征，简要描述各类缺陷的产生原因，最后给出各类缺陷的修正方法。
1.缺陷类型
概括地讲，软件本地化的缺陷主要分为两大类：核心缺陷和本地化缺陷。 
2.缺陷表现特征
由于本地化缺陷是本地化测试中出现的数量最多的缺陷，所以首先分析本地化缺陷的表现特征。而本地化测试中发现的核心缺陷虽然数量不多，不过他们的危害程度更大，所以需要认真对待，接下来分析他们的表现特征。
2.1用户界面缺陷
控件的文字被截断(Truncation)
对话框中的文本框、按钮、列表框、状态栏中的本地化文字只显示一部分
控件或文字没有对齐(Misaligned)
对话框中的同类控件或本地化文字没有对齐
控件位置重叠(Overlapped)
对话框中的控件彼此重叠
多余的文字(Extra strings)
软件程式的窗口或对话框中的出现多余的文字
丢失的文字(Missed strings)
软件程式的窗口或对话框中的文字部分或全部丢失
不一致的控件布局(Inconsistent layout)
本地化软件的控件布局和源语言软件不一致
丢失的文字(Missed strings)
软件程式的窗口或对话框中的文字部分或全部丢失
文字的字体、字号错误(Incorrect font name and font size)
控件的文字显示不美观，不符合本地化语言的正确字体和字号
多余的空格(Extra space)
本地化文字字符之间存在多余的空格
2.2语言质量缺陷
字符没有本地化(Unlocalized strings)
对话框或软件程式窗口中的应该本地化的文字没有本地化
字符不完整地本地化(Incomplete localized strings)
对话框或软件程式窗口中的应该本地化的文字只有一部分本地化
错误的本地化字符(Error localization)
源语言文字被错误地本地化，或对政治敏感的文字错误地进行了本地化
不一致的本地化字符(Inconsistent localized string)
相同的文字前后翻译不一致
相同的文字各语言之间不一致
相同的文字软件用户界面和联机帮助文件不一致
过度本地化(Over localization)
不应该本地化的字符进行了本地化
标点符号、版权、商标符号错误(Incorrect punctuation, Copyright)
标点符号、版权和商标的本地化不符合本地化语言的使用习惯
2.3本地化功能缺陷
本地化功能缺陷是本地化软件中的某些功能不起作用，或功能错误，和源语言功能不一致。
功能不起作用(Not working)
菜单、对话框的按钮、超链接不起作用
功能错误(Error function)
菜单、对话框的按钮、超链接引起程式崩溃
菜单、对话框的按钮、超链接带来和源语言软件不一致的错误结果
超链接没有链接到本地化的网站或页面
软件的功能不符合本地化用户的使用需求
热键和快捷键错误(Error hot keys and short-cut keys)
菜单或对话框中存在重复的热键
本地化软件中缺少热键或快捷键
不一致的热键或快捷键
快捷键或快捷键无效
2.4源语言功能缺陷
源语言功能缺陷是在源语言软件和全部本地化软件上都能复现的错误。
功能不起作用(Not working)
菜单不起作用
对话框的按钮不起作用
超链接不起作用
控件焦点跳转顺序(Tab键)不正确
文字内容错误(Incorrect strings)
软件的名称或版本编号错误
英文拼写错误、语法错误
英文用词不恰当等
2.5源语言国际化缺陷
源语言国际化缺陷是在源语言软件设计过程中对软件的本地化能力的处理不足引起的，他只出目前本地化的软件中。
区域设置错误(Error regional setting)
本地化日期格式错误
本地化时间格式错误
本地化数字格式(小数点、千位分隔符)错误
本地化货币单位或格式错误
本地化度量单位错误
本地化纸张大小错误
本地化电话号码和邮政编码错误
双字节字符错误(Error DBCS)
不支持双字节字符的输入
双字节字符显示乱码
不能保存含有双字节字符内容的文件
不能打印双字节字符
3.缺陷产生原因
核心缺陷是由于源程式软件编码错误引起的，例如研发人员对于某个功能模块的编码错误，或没有考虑软件的国际化和本地化能力，而将代码设定为某一种语言;
本地化缺陷是由于软件本地化过程引起的，例如语言翻译质量较差、界面控件布局不当、翻译了程式中的变量等。
4.缺陷修正方法
本地化缺陷是测试中发现的数量最多的Bug，他只出目前本地化的版本上，而不出目前源语言版本上，能由本地化工程师修改本地化软件相关资源文件解决，例如修改错误的翻译文字、调整控件的大小和位置等。
核心缺陷中的源语言功能缺陷既出目前本地化软件，也能在源语言软件上复现，而核心缺陷中的源语言国际化缺陷，虽然只出目前本地化版本中，不过只能通过修改程式代码实现，属于源语言软件的设计错误，这类缺陷只能由软件研发人员修正。 
 
转载：http://wenku.baidu.com/view/7c31c80b763231126fdb1107.html
