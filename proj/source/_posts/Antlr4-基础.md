---
title: Antlr4 基础
date: 2021-06-02 23:35:24
tags:
- Antlr4
- Java
categories:
- OTHER
---

## Install  ANTLR v4 on unix
+ Install Java (version 1.7 or higher)
Download
    $ cd /usr/local/lib
    $ curl -O https://www.antlr.org/download/antlr-4.9-complete.jar
Or just download in browser from website: https://www.antlr.org/download.html and put it somewhere rational like /usr/local/lib.

+ Add antlr-4.9-complete.jar to your CLASSPATH:
    $ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH"
It's also a good idea to put this in your .bash_profile or whatever your startup script is.

+ Create aliases for the ANTLR Tool, and TestRig.
    $ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
    $ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.gui.TestRig'

## Book source code
The book has lots and lots of examples that should be useful too. You can download them here for free:

http://pragprog.com/titles/tpantlr2/source_code

Also, there is a large collection of grammars for v4 at github:

https://github.com/antlr/grammars-v4/


# 百科
https://baike.baidu.com/item/antlr/9368750

antlr是指可以根据输入自动生成语法树并可视化的显示出来的开源语法分析器。

提供了一个通过语法描述来自动构造自定义语言的识别器（recognizer），编译器（parser）和解释器（translator）的框架

词法分析器又称为Scanner，Lexical analyser和Tokenizer。程序设计语言通常由关键字和严格定义的语法结构组成。编译的最终目的是将程序设计语言的高层指令翻译成物理机器或虚拟机可以执行的指令。词法分析器的工作是分析量化那些本来毫无意义的字符流，将他们翻译成离散的字符组（也就是一个一个的Token），包括关键字，标识符，符号（symbols）和操作符供语法分析器使用。


编译器又称为Syntactical analyser。在分析字符流的时候，Lexer不关心所生成的单个Token的语法意义及其与上下文之间的关系，而这就是Parser的工作。语法分析器将收到的Tokens组织起来，并转换成为目标语言语法定义所允许的序列。
无论是Lexer还是Parser都是一种识别器，Lexer是字符序列识别器而Parser是Token序列识别器。他们在本质上是类似的东西，而只是在分工上有所不同而已。如图1所示：




![1](1.png)
图1 字符输入流、tokens和AST之间的关系

树分析器可以用于对语法分析生成的抽象语法树进行遍历，并能执行一些相关的操作。

ANTLR将上述结合起来，它允许我们定义识别字符流的词法规则和用于解释Token流的语法分析规则。然后，ANTLR将根据用户提供的语法文件自动生成相应的词法/语法分析器。用户可以利用他们将输入的文本进行编译，并转换成其他形式（如AST—Abstract Syntax Tree，抽象的语法树）。

# ANTRL 语法
## `grammar`
声明语法头，类似于java类的定义

    grammar  SPL;

## `options`
选项，如语言选项，输出选项，回溯选项，记忆选项等等

    options { output=AST;  language=Java; }
    options { tokenVocab=MySqlLexer; }
