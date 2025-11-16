# C++ Moules Demo
## /!\ THIS IS A WORK IN PROGRESS!

This repo is made as an introduction to the use of the [C++20 modules](https://en.cppreference.com/w/cpp/language/modules.html).
Although modules are a part of the standards since years now, their production-ready implementation on main compilers is quite recent due to the huge rework of compiling needed. 

Considering the very few existing resources online on how to use them as of today, I made this simple tutorial/demo to guide anyone who woud want to quick-start their new project using modules.

This tutorial expects that you're already familiar with the pre-modules process of compilation in C++, especially the pre-processing part.

## I - What are modules?
Before starting using modules, it is important to know what they are, and why using it.

### Before modules
If you've already coded in C++, you know what are headers. Headers allows you to declare symbols to make the compiler aware of their existence and their type.
So what's the problem with headers? Well, there's a few:
 - EVERY time you ``#include`` a file, the content of this file is copy/pasted where the ``#include`` is. This makes the header compiles for each translation unit. This is slow.
 - You have no control over what symbol is publicly available and not. All macros and symbols will be imported by an ``#include``. Macros can have unexpected side effects.
 - Order of ``#include`` have an impact, especially with macros.
 - If you have two ``#includes`` declaring a symbol with the same name, they will conflict (can be avoided with namespace tho).
Modules will fix all of the above issues.
### So what is a module, exactly?
A module is kind of like a translation unit.
.ixx
.cppm

### II - Demo
As an example, we can create a simple program that will return a number from a function in a module.
We will start by 
```c++
// MyModule.ixx
export module MyModule;

namespace MyMod
{
  int number = 42;       // number is not exported, will not be available to code that imports this module.

  export int GetNumber() // We export GetNumber;
  {
    return number;
  }
}
```

```c++
import MyModule;

int main()
{
  return MyMod::GetNumber();
}
