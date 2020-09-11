---
title: "Learn about the size of compiled code (i.e. binary)"
excerpt: "A list of tests, observations and conclusions to learn \
about what affects the size of the compiled code aka binary in C and C++."

show_hero: false

categories:
  - learn
  - experiment

tags:
  - C
  - C++
  - Compiled code
  - Binary size
  - Learning
---

## System environment information

| Tools        | Version                |
| ------------ | ---------------------- |
| Compiler     | g++ 7.4.0              |
| CPU          | x86_64                 |
| Languages    | C++, C                 |
| Builder      | make, cmake            |
| OS           | Ubuntu 18.04.2 LTS     |
| IDE / Editor | Eclipse, Vim & VS Code |

## C++ binary code size

### Experiments

- Simple C++ code:

  ```cpp
    #include <iostream>

    using namespace std;

    int main(int argc, char **argv)
    {
        cout << "no macro" << endl;
        return 0;
    }
  ```
  
  1. Compiled with default option, i.e. `g++ file-name.cpp`.   
     **Test:** Compile with different file names.  
     **Observation:** Change in file name resulted in change in binary size.

     ```bash
     file name - binary size
     abcde.cpp - 8920
     abcdefghijklm.cpp - 8928
     abcdefghijklmfghijklm.cpp - 8936
     abcdefghijklmfghijklmfghijklm.cpp - 8944
     ```

     **Conclusion:** Changing file name by appending 8 chars starting from
     first five chars results an increase in 8 bytes in binary size.