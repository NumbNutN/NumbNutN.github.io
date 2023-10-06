---
layout: post
title: AddressSanitizer学习记录 - 内存安全检测大杀器
date: 2023-10-6
categories: blog
tags: [C,AddressSanitizer]
description: Segmentation Fault
---

**本文完全来源基于文章[工欲善其事必先利其器——AddressSanitizer - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/382994002)的总结。**



#### Asan插桩检测内存访问权限原理

```c
uint8_t memToShadow(void* addr){
	return *(addr >> 3 + offset)
}
```

以下结论在任何情况成立：

```c
//addr附近的实际可访问位置为
addr&~0x7 + memToshadow(addr)
//既    
addr + size  - 1 >= addr&~0x7 + memToShadow(addr) //表明访问越界
//化简
addr&0x7 + size - 1 >= memToShadow(addr)
```



#### Shadow Memory的标志值

```
Shadow byte legend (one shadow byte represents 8 application bytes):
  Addressable:           00
  Partially addressable: 01 02 03 04 05 06 07 
  Heap left redzone:       fa
  Freed heap region:       fd
  Stack left redzone:      f1
  Stack mid redzone:       f2
  Stack right redzone:     f3
  Stack after return:      f5
  Stack use after scope:   f8
  Global redzone:          f9
  Global init order:       f6
  Poisoned by user:        f7
  Container overflow:      fc
  Array cookie:            ac
  Intra object redzone:    bb
  ASan internal:           fe
  Left alloca redzone:     ca
  Right alloca redzone:    cb
  Shadow gap:              cc
```



#### 栈上对象检测

+ stack-buffer-overflow / stack-buffer-underflow

> 你可以查看google为这个实例提供的Example:  [AddressSanitizerExampleStackOutOfBounds · google/sanitizers Wiki (github.com)](https://github.com/google/sanitizers/wiki/AddressSanitizerExampleStackOutOfBounds)



+ Use after scope

​		栈上变量作用域失效后仍被使用



+ Use after return

​		栈上变量在函数返回后仍被使用



Google Address Sanitizer 机制

> Google Information: [AddressSanitizer · google/sanitizers Wiki (github.com)](https://github.com/google/sanitizers/wiki/AddressSanitizer)

如果需要查看GCC 关于Address Sanitizer的说明：

> [Instrumentation Options (Using the GNU Compiler Collection (GCC))](https://gcc.gnu.org/onlinedocs/gcc/Instrumentation-Options.html)

如果需要查看MSVC和Visual Studio关Address Sanitizer的说明：

> Microsoft information: [AddressSanitizer | Microsoft Learn](https://learn.microsoft.com/zh-cn/cpp/sanitizers/asan?view=msvc-170)

如果需要查看 Xcode 构建工具关于Address Sanitizer的说明：

>  [Diagnosing memory, thread, and crash issues early | Apple Developer Documentation](https://developer.apple.com/documentation/xcode/diagnosing-memory-thread-and-crash-issues-early)

如果需要查看Clang关于Address Sanitizer的说明：

> LLVM more information: [AddressSanitizer — Clang 18.0.0git documentation (llvm.org)](https://clang.llvm.org/docs/AddressSanitizer.html#more-information)

#### 





