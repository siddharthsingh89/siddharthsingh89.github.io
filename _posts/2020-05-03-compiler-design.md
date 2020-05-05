---
layout: post
title: Design a Compiler
description : compiler, design, system dev
---

#### What is a Compiler?
* A Compiler is a software program which translates a program written in a **source language** to equivalent program in the  **target language**.
* **Source language** is generally high level languages like C, C++, Java etc. It is designed and optimized for humans (the syntax is similar to our notion of languages such as english) and is readable and maintenable. It is easier to write, review and in general platform independent.
* **The target language**  is generally machine language or an intermediate language. It is generlly binary(0s and 1s) and the not 
for human to read or write. it is highly optimized to be understood  and executed by the processor.
![Compiler](/images/compiler.png "Compiler")


##### Goals of the Compiler
* **Corretness** - A compiler's most important goal is correctness . All valid programs must compile correctly. What the programmer wanted to achieve in the high level language should reflect in the generated machine code exactly with nothing lost in translation. 

* **Performance** - The code generated by the compiler should be performant.

* **Fast Compile Time** - The compiler should be fast enough to support modern face paced development cycles. Also, the compile time should be proportional to the high level code size.

* **Machine Code Size** - The compile should generate smaller sized binaries.

##### Abstract Design
The compile process comprises of many steps which can be abstracted under two main stages- the front end and the back end.
* The "front end" translates the source language or the high level program into an intermediate representation. 

* The second stage is the "back end", which works with the internal representation to produce code in the output language which is a low level code. 

![Two Stage Compiler Design](/images/two_stage.png "Two Stage Compiler Design")

##### Breaking a complex process in to small steps

* Compiler design is a complex task. We need to break it down to phases and need to go step by step, with each step doing a particular task and passing out its output for the next step in the form of another program representation. 

* The steps can be parse tree generation, high level intermediate code generation, low level intermediate code generation, and then the machine language conversion. As the translation proceeds the representation becomes more and more machine specific, increasingly dealing with registers, memory locations etc.

* Representations become more machine specific and less language specific as the translation proceeds.


##### Structure of a Compiler
A Compiler is composed of various components working on the source code in a sequence of phases. Below is a diagram showing the components and various phases of a compilation process-

![Stages of Compiler](/images/stages_compiler.png "Stages of Compiler")

###### Lexical Analyzer 
The first phase of a compiler is called lexical analysis or scanning. The lexical analyzer reads the stream of characters making up the source program and groups the characters into meaningful sequences called lexemes. For each lexeme, the lexical analyzer produces as output a token of the form **<token-name; attribute-value>** that it passes on to the subsequent phase, syntax analysis. 

In the token, the first component token-name is an abstract symbol that is used during syntax analysis, and the second component attribute-value points to an entry in the symbol table for this token. Information from the symbol-table entry is needed for semantic analysis and code generation.

 eg. *position = initial + rate * 60* becomes **<id; 1> <=> <id,2> <+> <id, 3> <*> <60>**
 
###### Syntax Analyzer
The second phase of the compiler is syntax analysis or parsing. The parser uses the first components of the tokens produced by the lexical analyzer to create a tree-like intermediate representation that depicts the grammatical structure of the token stream.

The subsequent phases of the compiler use the grammatical structure to help analyze the source program and generate the target program.
 
###### Semantic Analyzer
The semantic analyzer uses the syntax tree and the information in the symbol table to check the source program for semantic consistency with the language definition. It also gathers type information and saves it in either the syntax tree or the symbol table, for subsequent use during intermediate-code generation.

An important part of semantic analysis is type checking, where the compiler checks that each operator has matching operands. 
 
###### Intermediate Code Generator
After syntax and semantic analysis of the source program, many compilers generate an explicit low-level or machine-like intermediate representation, which we can think of as a program for an abstract machine. This intermediate representation should have two important properties: it should be easy to produce and it should be easy to translate into the target machine.
eg. three-address code is a popular intermediate representation.

###### Code Optimization
The machine-independent code-optimization phase attempts to improve the intermediate code so that better target code will result. Usually better means faster, but other objectives may be desired, such as shorter code, or target code that consumes less power.

###### Code Generation
The code generator takes as input an intermediate representation of the source program and maps it into the target language. If the target language is machine code, registers or memory locations are selected for each of the variables used by the program. Then, the intermediate instructions are translated into sequences of machine instructions that perform the same task. A crucial aspect of code generation is the judicious assignment of registers to hold variables.

##### Symbol Table
A data structure called symbol table is generally used to store information about various source language constructs. Lexical analyzer stores information in the symbol table for the subsequent phases of the compilation process. The symbol table routines are concerned primarily with saving and retrieving lexemes. When a lexeme is saved, we also save the token associated with the lexeme. As an interface to the symbol table, we have two functions

* *Insert( s , t )*: Saves and returns index of new entry for string s , token t .

* *Lookup( s )* : Returns index of the entry for string s , or 0 if s is not found.

![Stages of Compiler](/images/stages_compiler_1.png "Stages of 'compiler")
Source : Compilers-Principles, Techniques and Tools

#### Reference
* Compilers-Principles, Techniques and Tools (Second Edition) By Aho, Lam, Sethi and Ullman
* [Compiler Design Course by NPTEL IIT Kanput](https://nptel.ac.in/content/storage2/courses/106104072/ui/TOC.htm)
 