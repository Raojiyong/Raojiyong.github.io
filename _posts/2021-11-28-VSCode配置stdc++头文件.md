---
title: Mac OS VSCode配置stdc++.h头文件
author: raojiyong
date: 2021-11-28 22:00:00 +0800
categories: ["2021","11"]
tags: [notes,vscode,mac]
math: true
---

### VSCode 配置万能头文件stdc++.h

mac自带的clang就没办法直接include bits/stdc++.h，苦恼了一下午，终于找到了解决方法。

解决方法就是在“includePath”中添加自己写的stdc++.h

1. 首先输入`gcc -v -E -x c++ -`找到地址

   >/Library/Developer/CommandLineTools/usr/include/c++/v1

2. 在访达中输入`shift+command+g`复制上述地址，并写文件stdc++.h，常用的头文件都可以加在`endif`前

   ```c++
   // C++ includes used for precompiling -*- C++ -*-
    
   // Copyright (C) 2003-2015 Free Software Foundation, Inc.
   //
   // This file is part of the GNU ISO C++ Library.  This library is free
   // software; you can redistribute it and/or modify it under the
   // terms of the GNU General Public License as published by the
   // Free Software Foundation; either version 3, or (at your option)
   // any later version.
    
   // This library is distributed in the hope that it will be useful,
   // but WITHOUT ANY WARRANTY; without even the implied warranty of
   // MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
   // GNU General Public License for more details.
    
   // Under Section 7 of GPL version 3, you are granted additional
   // permissions described in the GCC Runtime Library Exception, version
   // 3.1, as published by the Free Software Foundation.
    
   // You should have received a copy of the GNU General Public License and
   // a copy of the GCC Runtime Library Exception along with this program;
   // see the files COPYING3 and COPYING.RUNTIME respectively.  If not, see
   // <http://www.gnu.org/licenses/>.
    
   /** @file stdc++.h
    *  This is an implementation file for a precompiled header.
    */
    
   // 17.4.1.2 Headers
    
   // C
   #ifndef _GLIBCXX_NO_ASSERT
   #include <cassert>
   #endif
   #include <cctype>
   #include <cerrno>
   #include <cfloat>
   #include <ciso646>
   #include <climits>
   #include <clocale>
   #include <cmath>
   #include <csetjmp>
   #include <csignal>
   #include <cstdarg>
   #include <cstddef>
   #include <cstdio>
   #include <cstdlib>
   #include <cstring>
   #include <ctime>
    
   #if __cplusplus >= 201103L
   #include <ccomplex>
   #include <cfenv>
   #include <cinttypes>
   #include <cstdalign>
   #include <cstdbool>
   #include <cstdint>
   #include <ctgmath>
   #include <cwchar>
   #include <cwctype>
   #endif
    
   // C++
   #include <algorithm>
   #include <bitset>
   #include <complex>
   #include <deque>
   #include <exception>
   #include <fstream>
   #include <functional>
   #include <iomanip>
   #include <ios>
   #include <iosfwd>
   #include <iostream>
   #include <istream>
   #include <iterator>
   #include <limits>
   #include <list>
   #include <locale>
   #include <map>
   #include <memory>
   #include <new>
   #include <numeric>
   #include <ostream>
   #include <queue>
   #include <set>
   #include <sstream>
   #include <stack>
   #include <stdexcept>
   #include <streambuf>
   #include <string>
   #include <typeinfo>
   #include <utility>
   #include <valarray>
   #include <vector>
    
   #if __cplusplus >= 201103L
   #include <array>
   #include <atomic>
   #include <chrono>
   #include <condition_variable>
   #include <forward_list>
   #include <future>
   #include <initializer_list>
   #include <mutex>
   #include <random>
   #include <ratio>
   #include <regex>
   #include <scoped_allocator>
   #include <system_error>
   #include <thread>
   #include <tuple>
   #include <typeindex>
   #include <type_traits>
   #include <unordered_map>
   #include <unordered_set>
   #endif
   ```

3. 最后在$project/.vscode/目录下的c_cpp_properties.json文件中加上一条"includePath"，我的json文件：

```json
{
    "configurations": [
        {
            "name": "Mac",
            "includePath": [
                "${workspaceFolder}/**",
                "/Library/Developer/CommandLineTools/usr/include/c++/v1"
            ],
            "defines": [],
            "macFrameworkPath": [
                "/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk/System/Library/Frameworks"
            ],
            "compilerPath": "/usr/bin/clang",
            "cStandard": "c17",
            "cppStandard": "c++98",
            "intelliSenseMode": "macos-clang-arm64"
        }
    ],
    "version": 4
}
```

