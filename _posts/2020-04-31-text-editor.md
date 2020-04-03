---
layout: post
title: Design a text editor
description : text editor, system dev, system design
---

##### What's a text Editor ?
A text editor is used to create and edit documents. Text Editors provide a visual way to create, see and edit text documents on the computer. Common Examples are MS-Word, Sublime Text, Notepad++, Emacs, Atom etc.

Note: While they look easy, writing a text editor such as MS-Word is way harder problem as compared to our distributed systems.

##### Requirements and Goals of the system
1. User should be able to create new file and save file on disk.
2. User should be able to Edit,remove text in the file using a blinking cursor.
3. The editor should support Undo and Redo operations.
4. The Editor should provide text search and replace functionality.
5. User should be able to select text and performce various operation on it.
6. Supported Operations- Cut, Copy, Paste.  
7. System should be extensible and plugins based.

##### Optional Features
1. Support of multiple encodings.
2. Support of non-text content such as Images, fonts etc.
3. Printer support.

##### Non-functional Requirements
1. Efficient Memory usage
2. Fast performance for edits, copy, paste, undo operations.

##### Some Data Structures for Text Editors
1. Arrays
2. Rope
3. Gap Buffer
4. Piece Table

##### High level Design


##### References
