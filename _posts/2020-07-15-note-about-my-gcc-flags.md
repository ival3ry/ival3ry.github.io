---
title: '[C] GCC Flags'
published: true
---

It's a good practice to use GCC flags. My list of GCC's flags:

* Wanrning:
  * -Wall
  * -Wextra
  * -Wpedantic
  * -Wstrict-aliasing
* Threats warnings as a error:
  * -Werror 
* Enable optimization; Release version:
  * -O2
* Include debuging information:
  * -ggdb
* To detect memory leak/double free/use-after-free/...
  * -fsanitize=address
  * -fno-omit-frame-pointer
