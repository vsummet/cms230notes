# Chapter 5 - Representing Characters with Bit Patterns

Patterns of bits represent many types of things. This chapter shows how bit patterns are used to represent characters.

## Chapter Topics:
* ASCII
* Control characters
* Teletype Machines
* .asciiz and null terminated strings
* Disk files
* Text files
* Binary files
* Executable files

### Question: What else (besides characters and integers) can be represented with bit patterns?
Machine instructions. (Many others answers are correct too; anything symbolic can be represented with bit patterns: graphics, music, floating point numbers, internet locations, video, ...)


## 5.1 - Representing Characters

A group of 8 bits is a byte. Typically one character is represented with one byte. The agreement by the American Standards Committee on what pattern represents what character is called ASCII. (There are several ways to pronounce "ASCII". Frequently it is pronounced "ásk-ee"). Most microcomputers and many mainframes follow this standard.

![printer](./images/ch05-printer.gif)

When a printer built to print ASCII receives the ASCII pattern for "A" (along with some control signals), it prints an "A". Printers built to other specifications (typically for mainframe computers) might print some completely different character if sent the same pattern.

Most modern printers are much more complicated than the one illustrated above. Typically, a modern printer is sent an entire file of information at once. The file describes the layout and contents of an entire page. ASCII characters are just some of the information in the file.

### Question
Do some files contain bit patterns that represent things other than characters?
Of course.  Pure ASCII files are rare these days, but source code files (such as <tt>Hello.java</tt> or <tt>hello.c</tt> are a notable exception and are plain text files.


## 5.2 - Control Characters
Some ASCII patterns do not correspond to a printable character. For example, the pattern 0x00 (ie. 0000 0000) is the NUL character. NUL is often used as a marker in collections of data. The pattern 0x0A is the linefeed character (LF), sent to a printer to indicate that it should advance one line. The patterns 0x00 through 0x1F are called control characters and are used to control input and output devices. The exact use of a control character depends on the particular output device. Many control characters were originally used to control the mechanical functions of a Teletype machine.


